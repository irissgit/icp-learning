# Motoko 语言简介



## 认识motoko

### 运行原理

ICP智能合约，封装在**Canister轻量级容器**里。

Canister的结构分为两部分，

- 1 	**WebAssembly**
  - web3标准,跑底层字节码
  - 所有主流浏览器支持
  - 也可以运行在服务器端
  - 有正规定义的语义 非常安全的语言
- canister合约被创建后，wasm有个初始化函数；该初始化函数开始运行、能够创建该合约的状态，状态包括内存、全局变量、消息队列(用于canister之间通信) 等；所有的状态在IC上自动持久化——智能合约通过运行函数（通常是经过远程的函数调用 即消息）使状态被修改，这一修改被记录并自动持久化；也因此IC没有读取数据库或者外部文件等操作。
- 2 	**状态(内存、全局变量、消息队列等)**



### 语言特性

- 静态类型（语法接近JS和TS）
- 面向对象（motoko不支持继承关系）
- 支持异步通信（await和async）
- 结构化类型推断（类似的有typescript是动态结构化类型检查）
- 安全的数值计算（和C/C++的区别也是安全性
- 没有null指针
- 自动GC



### motoko基础

https://smartcontracts.org/docs/language-guide/motoko-introduction.html

- 概念

- 语法

- 关键字

  

  注1：

  ```
  func f( x: Nat ): Nat { let y = x + 1; x + y }
  // func f( x:类型 ): 返回类型 { 函数体 }
  ```

  注2：

  `let` 声明变量 值不可改变，赋值用 `=`

  `var` 可变变量，赋值用 `:=`

  注3：`#` 字符串的拼接符

  

- 基础库：https://smartcontracts.org/docs/base-libraries/stdlib-intro.html （开源代码https://github.com/dfinity/motoko-base ）

- Motoko Canister：每个canister都是一个actor

  - IC的`public method`都是异步调用
  - 数据描述语言 `Candid`用来规范Canister所提供的数据类型，服务接口等



## VS Code 演示

### 安装motoko extension

检查vscode是否在路径中

```
bc20010540004@localehost:~$ ls
Desktop    ibmbce       Music       package-lock.json  snap
Documents  ibmtutorial  myworkshop  Pictures           Templates
Downloads  index.html   NewDisk     Public             Videos
bc20010540004@localehost:~$ cd Desktop/
bc20010540004@localehost:~/Desktop$ cd mysite/

bc20010540004@localehost:~/Desktop/mysite$ which code
/usr/bin/code
bc20010540004@localehost:~/Desktop/mysite$ export PATH='/usr/bin/code':$PATH
bc20010540004@localehost:~/Desktop/mysite$ which code
/usr/bin/code

//在vscode打开当前目录
bc20010540004@localehost:~/Desktop/mysite$ code .
```



下载extension:	

```
Error while fetching extensions. XHR failed
```

找原因：

```
https://code.visualstudio.com/docs/setup/network#_proxy-server-support
```

```
https://github.com/MicrosoftDocs/WSL/issues/937
```

> Try `sudo ping 8.8.8.8` inside your distro (Ubuntu).
> If you can not reach network, search for **network related issues** in wsl.
>
> If network is reachable, it's either **dns** problem or **host** being blocked by your network.
>
> To check dns try `sudo ping archive.ubuntu.com`.
> If only archive.ubuntu.com is not reachable, try **changing your apt sources to some other mirror.** There is plenty of info on how to do this in the web.



虚拟机换源：

```
/备份原来的源
sudo cp /etc/apt/sources.list /etc/apt/sources_init.list
更换源
sudo gedit /etc/apt/sources.list
```

复制阿里ubuntu源20.04

```
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

```

```
//更新源
sudo apt-get update
//复损坏的软件包，尝试卸载出错的包，重新安装正确版本的
sudo apt-get -f install
//更新软件
sudo apt-get upgrade
```

现在可以下载想要的库或软件了。

结果还是不行。

后来通过检查VMware两个地方的网络配置，搁置了两三天，重启，好了。

<img src="C:\Users\Administrator.DESKTOP-3E455V4\AppData\Roaming\Typora\typora-user-images\image-20220307212639894.png" alt="image-20220307212639894" style="zoom: 33%;" />



<img src="C:\Users\Administrator.DESKTOP-3E455V4\AppData\Roaming\Typora\typora-user-images\image-20220307212823935.png" alt="image-20220307212823935" style="zoom: 33%;" />



### 配置motoko language server

为motoko 配置 language server

```
which dfx
```

重启vscode；Motoko LS initialized

```
export PATH=~/bin:$PATH
which dfx
```

```
$ dfx cache --help

$ dfx cache show
/home/bc20010540004/.cache/dfinity/versions/0.8.4
 	//在这个路径里面，有一些我们dfx所需要用到的命令
 
$ export PATH=$(dfx cache show):$PATH

```

使用moc进行编译

```
$ which moc
/home/bc20010540004/.cache/dfinity/versions/0.8.4/moc
	//编译器
	
$ moc //直接开始解释 （解释环境）（互动的方式输入程序）
Motoko compiler 0.6.11 (source dskamx2f-i37ap368-kchqhbnw-hfjpbhm6)
> 1+2; 
3 : Nat
> let x = 1+2;
let x : Nat = 3
> x*2
  ;
6 : Nat
> 

$ moc -r src/mysite/main.mo
//-r，没有返回值，这种方式的解释运行需要打印出来
//需要引入一个debug模块： import Debug "mo:base/Debug";
//print需要字符串 不是自然数 类型不匹配
//引入nat module:		import Nat "mo:base/Nat" ;

```



单独用moc编译器，不知道base基础库在哪，所以需要指定一下

```
moc --package base $(dfx cache show)/base -r src/mysite/test.mo
```



### 写一个简单的test.mo

`test.mo` ：

```
import Debug "mo:base/Debug" ;
import Nat "mo:base/Nat" ;

func fib( n: Nat ): Nat{
    if( n <= 1 ){
        return 1;
        1; // 花括号返回最后一行的值，只写1不写return相当于这句是if的执行结果是1
    } else {
        fib(n-2) + fib(n-1) ;
    }
} ; // 声明和表达式,声明和声明之间,必须分开

// 也可以写成一行：
// if(n<=1) 1 else fib(n-2)+fib(n-1);

Debug.print( Nat.toText(1+2) );
Debug.print( Nat.toText( fib(10) ) );
```

​	返回：

```
3
89
```



### 写成 actor ，以便 用dfx部署到canister

```
/* actor {
    public func greet(name : Text) : async Text {
        return "Hello, " # name # "!";
    };
};
*/

import Debug "mo:base/Debug" ;
import Nat "mo:base/Nat" ;

actor {

    func fib( n: Nat ): Nat{
       let x= if( n <= 1 ) 1 else{
        	let y = fib( n-1 );
        	fib( n-2 ) + y
         }
    };

	public func fibonacci(x:Nat): async Nat{
		fib(x)
	}
	
}
```

actor需要是唯一的一个声明，func要写到actor里面

actor需要放到main.mo（？



### 部署main.mo

```
bc20010540004@localehost:~/Desktop/mysite$ dfx deploy
An error happened during communication with the replica: error sending request for url (http://127.0.0.1:8000/api/v2/status): error trying to connect: tcp connect error: Connection refused (os error 111)

//没有启动本地的生产环境
//终端 dfx start 
```

##### 如果deploy时，遇到

```
bc20010540004@localehost:~/Desktop/mysite$ dfx deploy
The replica returned an HTTP Error: Http Error: status 500 Internal Server Error, content type "", content: Internal Server Error
```

##### 则试一下本地重启dfx

```
$ dfx start --clean
Starting webserver for /_/
binding to: 127.0.0.1:43639
Mar 07 01:44:14.693 INFO ic-starter. Configuration: ValidatedConfig { replica_path: Some("/home/bc20010540004/.cache/dfinity/versions/0.8.4/replica"), replica_version: "0.8.0", log_level: Warning, cargo_bin: "cargo", cargo_opts: "", state_dir: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state", http_listen_addr: 127.0.0.1:0, http_port_file: Some("/home/bc20010540004/Desktop/mysite/.dfx/replica-configuration/replica-1.port"), metrics_addr: None, provisional_whitelist: Some(All), artifact_pool_dir: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/ic_consensus_pool", crypto_root: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/crypto", state_manager_root: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/state", registry_local_store_path: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/ic_registry_local_store", unit_delay: None, initial_notary_delay: Some(600ms), detect_consensus_starvation: None, consensus_pool_backend: Some("rocksdb"), state_dir_holder: None }, Application: starter
Mar 07 01:44:14.693 INFO Initialize replica configuration "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/ic.json5", Application: starter
Mar 07 01:44:15.822 INFO Executing "/home/bc20010540004/.cache/dfinity/versions/0.8.4/replica" "--replica-version" "0.8.0" "--config-file" "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/ic.json5", Application: starter
Mar 07 01:44:23.292 WARN s:g7zrx-k23fo-btdvp-dz7jx-dtbev-qlunp-ppgzt-zdhxw-r5hkd-o6gdj-jae/n:rht5x-y7aqj-s2coz-jvz6s-4xwy5-tsae4-pdygr-5ftrb-qnyhy-v4fg6-oqe/ic_p2p/download_management PeerManagerImpl::new(): relay_config = None
version: 0.7.0
 Mar 07 09:44:23.326 INFO Log Level: INFO
 Mar 07 09:44:23.326 INFO Starting server. Listening on http://127.0.0.1:8000/
Mar 07 01:45:27.205 WARN s:g7zrx-k23fo-btdvp-dz7jx-dtbev-qlunp-ppgzt-zdhxw-r5hkd-o6gdj-jae/n:rht5x-y7aqj-s2coz-jvz6s-4xwy5-tsae4-pdygr-5ftrb-qnyhy-v4fg6-oqe/ic_state_layout/utils StateManager runs on a filesystem not supporting reflinks (attempted to reflink /home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/state/tip/canister_states/00000000000000030101/stable_memory.bin => /home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/state/fs_tmp/scratchpad_0000000000000064/canister_states/00000000000000030101/stable_memory.bin), running big canisters can be very slow

```



##### 如果call函数时，遇到

```
bc20010540004@localehost:~/Desktop/mysite$ dfx canister call mysite fibonacci '(10)'
The Replica returned an error: code 3, message: "Canister rrkah-fqaaa-aaaaa-aaaaq-cai has no update method 'fibonacci'"
```

##### 则

把fibonacci写在main.mo文件（要求是actor在main.mo?还是函数需要能够在main找到？怎么解释？



#### 成功：deploy合约、call函数

```
bc20010540004@localehost:~/Desktop/mysite$ dfx deploy
Creating a wallet canister on the local network.
The wallet canister on the "local" network for user "default" is "rwlgt-iiaaa-aaaaa-aaaaa-cai"
Deploying all canisters.
Creating canisters...
Creating canister "mysite"...
"mysite" canister created with canister id: "rrkah-fqaaa-aaaaa-aaaaq-cai"
Creating canister "mysite_assets"...
"mysite_assets" canister created with canister id: "ryjl3-tyaaa-aaaaa-aaaba-cai"
Building canisters...
Building frontend...
Installing canisters...
Creating UI canister on the local network.
The UI canister on the "local" network is "r7inp-6aaaa-aaaaa-aaabq-cai"
Installing code for canister mysite, with canister_id rrkah-fqaaa-aaaaa-aaaaq-cai
Installing code for canister mysite_assets, with canister_id ryjl3-tyaaa-aaaaa-aaaba-cai
Authorizing our identity (default) to the asset canister...
Uploading assets to asset canister...
Starting batch.
Staging contents of new and changed assets:
  /index.js.LICENSE.txt 1/1 (413 bytes)
  /index.js.LICENSE.txt (gzip) 1/1 (274 bytes)
  /main.css 1/1 (537 bytes)
  /main.css (gzip) 1/1 (297 bytes)
  /irisindex.html 1/1 (61 bytes)
  /index.html 1/1 (664 bytes)
  /index.html (gzip) 1/1 (381 bytes)
  /index.js.map 1/1 (653724 bytes)
  /index.js.map (gzip) 1/1 (149011 bytes)
  /favicon.ico 1/1 (15406 bytes)
  /logo.png 1/1 (25397 bytes)
  /sample-asset.txt 1/1 (24 bytes)
  /index.js 1/1 (604265 bytes)
  /index.js (gzip) 1/1 (144729 bytes)
Committing batch.
Deployed canisters.
```

```
bc20010540004@localehost:~/Desktop/mysite$ dfx canister call mysite fibonacci '(10)'
(89 : nat)
bc20010540004@localehost:~/Desktop/mysite$ dfx canister call mysite fibonacci '(10 : nat)'
(89 : nat)
```



## Candid UI 演示

访问，(不可以是https)

```
http://r7inp-6aaaa-aaaaa-aaabq-cai.localhost:8000
```



<img src="C:\Users\Administrator.DESKTOP-3E455V4\AppData\Roaming\Typora\typora-user-images\image-20220307171712023.png" alt="image-20220307171712023" style="zoom:50%;" />





## Motoko Playground 演示

部署在IC的应用，在线编辑motoko

一键部署，免费提供cycles

右边显示candid ui



## 第二课作业：Qsort

用 motoko 实现一个快排函数：`quicksort : [var Int] -> ()`

1.用 moc 调试运行。
2.把函数封装在一个 canister 里面，要求提供以下接口：
`public func qsort(arr: [Int]): async [Int]`
3.部署到主网
4.使用主网的 Candid UI 调试运行https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app



#### 理解快排

[快速排序 wiki](https://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F)

[快排算法](https://baike.baidu.com/item/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/369842?fromtitle=%E5%BF%AB%E6%8E%92%E7%AE%97%E6%B3%95&fromid=15464901&fr=aladdin#reference-[2]-19016-wrap)

C语言版本

```
void quickSort(int *number, int first, int last) {
    int i, j, pivot;
    int temp;
    if (first<last) {
        pivot = first;
        i = first;
        j = last;
        while (i<j) {
            while (number[i] <= number[pivot] && i<last)
                i++;
            while (number[j]>number[pivot])
                j--;
            if (i<j) {
                temp = number[i];
                number[i] = number[j];
                number[j] = temp;
            }
        }
        temp = number[pivot];
        number[pivot] = number[j];
        number[j] = temp;
        quickSort(number, first, j - 1);
        quickSort(number, j + 1, last);
    }
}
```



#### Motoko实现

##### main.mo

```
import Int "mo:base/Int";
import Quicksort "Quicksort";

actor Main {

  // Sort an array of integers.
  public query func sort(xs : [Int]) : async [Int] {
    return Quicksort.sortBy(xs, Int.compare);
  };
};

/* //报错不会调 放弃
import Quicksort "Quicksort";

actor {
    public func qksort(n : [Int]) : async [Int] {
       Quicksort.qsort(n)
    };
};
*/
```

##### Quicksort.mo

```
import Array "mo:base/Array";
import Order "mo:base/Order";
import Int "mo:base/Int";

module Quicksort {

  type Order = Order.Order;

  // Sort the elements of an array using the given comparison function.
  public func sortBy<X>(xs : [X], f : (X, X) -> Order) : [X] {
    let n = xs.size();
    if (n < 2) {
      return xs;
    } else {
      let result = Array.thaw<X>(xs);
      sortByHelper<X>(result, 0, n - 1, f);
      return Array.freeze<X>(result);
    };
  };

  private func sortByHelper<X>(
    xs : [var X],
    l : Int,
    r : Int,
    f : (X, X) -> Order,
  ) {
    if (l < r) {
      var i = l;
      var j = r;
      var swap  = xs[0];
      let pivot = xs[Int.abs(l + r) / 2];
      while (i <= j) {
        while (Order.isLess(f(xs[Int.abs(i)], pivot))) {
          i += 1;
        };
        while (Order.isGreater(f(xs[Int.abs(j)], pivot))) {
          j -= 1;
        };
        if (i <= j) {
          swap := xs[Int.abs(i)];
          xs[Int.abs(i)] := xs[Int.abs(j)];
          xs[Int.abs(j)] := swap;
          i += 1;
          j -= 1;
        };
      };
      if (l < j) {
        sortByHelper<X>(xs, l, j, f);
      };
      if (i < r) {
        sortByHelper<X>(xs, i, r, f);
      };
    };
  };
};

/*
import Array "mo:base/Array";
import Int "mo:base/Int";
import Nat "mo:base/Nat";

module Quicksort {

    func sort(n:[var Int],first:Nat,last:Nat) {
        
        //check1
         if(first>=last) return;

        var pivot = n[first];
        var i = first;
        var j = last;
        
        while(i < j) {
            while(n[j] >= pivot and j > i){
                j -=1;
            };
            n[i] := n[j];    //swap1

            while(n[i] <= pivot and i < j){
                i +=1;
            };
            n[j] := n[i];    //swap2
        };
        n[j] := pivot;  //swap3
 
        //check2
        if(i >= 1) 
            sort(n,first,i-1);
        sort(n,i+1,last);

    };

    public func qsort(n: [Int]): async [Int]{
        var newArr:[var Int] = Array.thaw(n);
        sort(newArr, 0, newArr.size()-1);
        Array.freeze(newArr)
    };
    
};
*/
```



#### 调试运行

（作业要求的不是本地部署，是主网部署，做错了，但也记一下）

部署在本地

```
bc20010540004@localehost:~/Desktop/mysite$ dfx deploy
Deploying all canisters.
All canisters have already been created.
Building canisters...
Building frontend...
Installing canisters...
Creating UI canister on the local network.
The UI canister on the "local" network is "r7inp-6aaaa-aaaaa-aaabq-cai"
Installing code for canister mysite, with canister_id rrkah-fqaaa-aaaaa-aaaaq-cai
Installing code for canister mysite_assets, with canister_id ryjl3-tyaaa-aaaaa-aaaba-cai
Authorizing our identity (default) to the asset canister...
Uploading assets to asset canister...
Starting batch.
Staging contents of new and changed assets:
  /index.js.LICENSE.txt 1/1 (413 bytes)
  /index.js.LICENSE.txt (gzip) 1/1 (274 bytes)
  /main.css 1/1 (537 bytes)
  /main.css (gzip) 1/1 (297 bytes)
  /irisindex.html 1/1 (61 bytes)
  /index.html 1/1 (664 bytes)
  /index.html (gzip) 1/1 (381 bytes)
  /index.js.map 1/1 (653753 bytes)
  /index.js.map (gzip) 1/1 (149011 bytes)
  /favicon.ico 1/1 (15406 bytes)
  /logo.png 1/1 (25397 bytes)
  /sample-asset.txt 1/1 (24 bytes)
  /index.js 1/1 (604292 bytes)
  /index.js (gzip) 1/1 (144735 bytes)
Committing batch.
Deployed canisters.
```

![image-20220322205521520](C:\Users\Administrator.DESKTOP-3E455V4\AppData\Roaming\Typora\typora-user-images\image-20220322205521520.png)



部署到主网

```
bc20010540004@localehost:~/Desktop/mysite$ dfx deploy --network=ic --with-cycles=400000000000
Deploying all canisters.
Creating canisters...
Creating canister "mysite"...
"mysite" canister created on network "ic" with canister id: "uhkvx-xaaaa-aaaal-qataa-cai"
Creating canister "mysite_assets"...
"mysite_assets" canister created on network "ic" with canister id: "ualtd-2yaaa-aaaal-qataq-cai"
Building canisters...
Building frontend...
Installing canisters...
Installing code for canister mysite, with canister_id uhkvx-xaaaa-aaaal-qataa-cai
Installing code for canister mysite_assets, with canister_id ualtd-2yaaa-aaaal-qataq-cai
Authorizing our identity (default) to the asset canister...
Uploading assets to asset canister...
Starting batch.
Staging contents of new and changed assets:
  /index.js.LICENSE.txt 1/1 (413 bytes)
  /index.js.LICENSE.txt (gzip) 1/1 (274 bytes)
  /main.css 1/1 (537 bytes)
  /main.css (gzip) 1/1 (297 bytes)
  /irisindex.html 1/1 (61 bytes)
  /index.html 1/1 (529 bytes)
  /index.html (gzip) 1/1 (343 bytes)
  /index.js.map 1/1 (653753 bytes)
  /index.js.map (gzip) 1/1 (149011 bytes)
  /favicon.ico 1/1 (15406 bytes)
  /logo.png 1/1 (25397 bytes)
  /sample-asset.txt 1/1 (24 bytes)
  /index.js 1/1 (242095 bytes)
  /index.js (gzip) 1/1 (83702 bytes)
Committing batch.
Deployed canisters.
```

![image-20220322211501591](C:\Users\Administrator.DESKTOP-3E455V4\AppData\Roaming\Typora\typora-user-images\image-20220322211501591.png)

