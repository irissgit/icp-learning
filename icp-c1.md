### 一、本地部署

#### （1）To download the DFINITY Canister SDK, run the above command in your terminal

```
sh -ci "$(curl -fsSL https://smartcontracts.org/install.sh)"
```

​	DFINITY Canister SDK 下载完成：

```
bc20010540004@localehost:~/Desktop$ sh -ci "$(curl -fsSL https://smartcontracts.org/install.sh)"
info: Executing dfx install script, commit: 6faa80cb336e2f9392fbcbd3a0cfd2b6f3bce4d3
info: Version found: 0.8.4
info: Creating uninstall script in ~/.cache/dfinity
info: uninstall path=/home/bc20010540004/.cache/dfinity/uninstall.sh
info: Checking for latest release...
Will install in: /usr/local/bin
info: Installed /usr/local/bin/dfx
```



#### （2）添加环境变量，并检查dfx路径

```
bc20010540004@localehost:~/Desktop$ export PATH=/usr/local/bin:$PATH
bc20010540004@localehost:~/Desktop$ which dfx
Command 'which' is available in the following places
 * /bin/which
 * /usr/bin/which
The command could not be located because '/usr/bin:/bin' is not included in the PATH environment variable.
which: command not found

bc20010540004@localehost:~/Desktop$ dfx --version
dfx 0.8.4

bc20010540004@localehost:~/Desktop$ export PATH=/usr/bin:$PATH
bc20010540004@localehost:~/Desktop$ which dfx
/usr/local/bin/dfx
```



#### （3）创建新项目/目录/文件

```
bc20010540004@localehost:~/Desktop$ dfx new mysite
Fetching manifest https://sdk.dfinity.org/manifest.json
⠒ Checking for latest dfx version...
You seem to be running an outdated version of dfx.

You are strongly encouraged to upgrade by running 'dfx upgrade'!
  Version v0.8.4 installed successfully.
Creating new project "mysite"...
CREATE       mysite/src/mysite/main.mo (107B)...
CREATE       mysite/src/mysite_assets/assets/sample-asset.txt (24B)...
CREATE       mysite/README.md (2.25KB)...
CREATE       mysite/dfx.json (486B)...
⠒ Checking for latest dfx version...
CREATE       mysite/src/mysite_assets/src/index.js (529B)...
CREATE       mysite/src/mysite_assets/src/index.html (626B)...
CREATE       mysite/src/mysite_assets/assets/main.css (537B)...
CREATE       mysite/src/mysite_assets/assets/favicon.ico (15.04KB)...
CREATE       mysite/src/mysite_assets/assets/logo.png (24.80KB)...
CREATE       mysite/package.json (1.12KB)...
CREATE       mysite/webpack.config.js (3.52KB)...
⠒ Checking for latest dfx version...
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.3.2 (node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.3.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN mysite_assets@0.1.0 No repository field.
npm WARN mysite_assets@0.1.0 No license field.

⠋ Checking for latest dfx version...

86 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
  Done.
Creating git repository...

===============================================================================
        Welcome to the internet computer developer community!
                        You're using dfx 0.8.4

            ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄                ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄       
          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄    
        ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄  
       ▄▄▄▄▄▄▄▄▄▄▀▀▀▀▀▄▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄▄▀▀▀▀▀▀▄▄▄▄▄▄▄▄▄▄ 
      ▄▄▄▄▄▄▄▄▀         ▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀         ▀▄▄▄▄▄▄▄▄▄
     ▄▄▄▄▄▄▄▄▀            ▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀             ▄▄▄▄▄▄▄▄
     ▄▄▄▄▄▄▄▄               ▀▄▄▄▄▄▄▄▄▄▄▄▄▀                ▄▄▄▄▄▄▄
     ▄▄▄▄▄▄▄▄                ▄▄▄▄▄▄▄▄▄▄▄▄                 ▄▄▄▄▄▄▄
     ▄▄▄▄▄▄▄▄               ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄              ▄▄▄▄▄▄▄▄
      ▄▄▄▄▄▄▄▄           ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄          ▄▄▄▄▄▄▄▄▀
      ▀▄▄▄▄▄▄▄▄▄▄     ▄▄▄▄▄▄▄▄▄▄▄▄▀ ▀▄▄▄▄▄▄▄▄▄▄▄▄    ▄▄▄▄▄▄▄▄▄▄▄ 
       ▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀     ▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀  
         ▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀         ▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄    
           ▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀▀             ▀▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀      
              ▀▀▀▀▀▀▀▀▀▀▀                    ▀▀▀▀▀▀▀▀▀▀▀         
     


To learn more before you start coding, see the documentation available online:

- Quick Start: https://sdk.dfinity.org/docs/quickstart/quickstart-intro.html
- SDK Developer Tools: https://sdk.dfinity.org/docs/developers-guide/sdk-guide.html
- Motoko Language Guide: https://sdk.dfinity.org/docs/language-guide/motoko.html
- Motoko Quick Reference: https://sdk.dfinity.org/docs/language-guide/language-manual.html

If you want to work on programs right away, try the following commands to get started:

    cd mysite
    dfx help
    dfx new --help

===============================================================================

bc20010540004@localehost:~/Desktop$ ls
fabriclab123  mysite
bc20010540004@localehost:~/Desktop$ cd mysite/
bc20010540004@localehost:~/Desktop/mysite$ ls
dfx.json  node_modules  package.json  package-lock.json  README.md  src  webpack.config.js

```

主要有三个文件：①`README.md`；②`dfx.json` dfx项目配置；③`src` 源代码

```
bc20010540004@localehost:~/Desktop/mysite$ cat dfx.json 
{
  "canisters": {
    "mysite": {
      "main": "src/mysite/main.mo",
      "type": "motoko"
    },
    "mysite_assets": {
      "dependencies": [
        "mysite"
      ],
      "frontend": {
        "entrypoint": "src/mysite_assets/src/index.html"
      },
      "source": [
        "src/mysite_assets/assets",
        "dist/mysite_assets/"
      ],
      "type": "assets"
    }
  },
  "defaults": {
    "build": {
      "args": "",
      "packtool": ""
    }
  },
  "dfx": "0.8.4",
  "networks": {
    "local": {
      "bind": "127.0.0.1:8000",
      "type": "ephemeral"
    }
  },
  "version": 1
}

bc20010540004@localehost:~/Desktop/mysite$ ls -R src/
src/:
mysite  mysite_assets

src/mysite:
main.mo

src/mysite_assets:
assets  src

src/mysite_assets/assets:
favicon.ico  logo.png  main.css  sample-asset.txt

src/mysite_assets/src:
index.html  index.js
```

`src`（源代码）下有两个子目录，对应两个canister（轻量级容器）：

① `mysite`  有 `.mo` motoko程序

② `mysite_assets`  没有程序 有一些资源 （资源会被打包上传到前端canister里面）



#### （4）如何提供网站服务

##### A. 创建简单网页

```
bc20010540004@localehost:~/Desktop/mysite$ echo '<html><body><h1> Hello World! I am iris. </h1></body></html>' > src/mysite_assets/assets/irisindex.html
bc20010540004@localehost:~/Desktop/mysite$ cat  src/mysite_assets/assets/irisindex.html
<html><body><h1> Hello World! I am iris. </h1></body></html>
```

##### B. 怎么运行该网页

###### 	a. `dfx start --background` 跑在后台，这里用`dfx start` 

```
bc20010540004@localehost:~/Desktop/mysite$ dfx start
Starting webserver for /_/
binding to: 127.0.0.1:34999
Feb 23 07:02:43.861 INFO ic-starter. Configuration: ValidatedConfig { replica_path: Some("/home/bc20010540004/.cache/dfinity/versions/0.8.4/replica"), replica_version: "0.8.0", log_level: Warning, cargo_bin: "cargo", cargo_opts: "", state_dir: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state", http_listen_addr: 127.0.0.1:0, http_port_file: Some("/home/bc20010540004/Desktop/mysite/.dfx/replica-configuration/replica-1.port"), metrics_addr: None, provisional_whitelist: Some(All), artifact_pool_dir: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/ic_consensus_pool", crypto_root: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/crypto", state_manager_root: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/state", registry_local_store_path: "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/ic_registry_local_store", unit_delay: None, initial_notary_delay: Some(600ms), detect_consensus_starvation: None, consensus_pool_backend: Some("rocksdb"), state_dir_holder: None }, Application: starter
Feb 23 07:02:43.862 INFO Initialize replica configuration "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/ic.json5", Application: starter
Feb 23 07:02:44.906 INFO Executing "/home/bc20010540004/.cache/dfinity/versions/0.8.4/replica" "--replica-version" "0.8.0" "--config-file" "/home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/ic.json5", Application: starter
Feb 23 07:02:59.733 WARN s:5eszt-luiwz-oo7lb-muagu-afix3-r3ee2-3aoc2-qsevh-yzbyp-7xdph-yae/n:jcvhe-ndgle-taky6-2cmnk-w2eie-lftxv-uupda-cdzyz-3if3c-23qux-eqe/ic_p2p/download_management PeerManagerImpl::new(): relay_config = None
version: 0.7.0
 Feb 23 15:02:59.835 INFO Log Level: INFO
 Feb 23 15:02:59.839 INFO Starting server. Listening on http://127.0.0.1:8000/
Feb 23 07:04:02.143 WARN s:5eszt-luiwz-oo7lb-muagu-afix3-r3ee2-3aoc2-qsevh-yzbyp-7xdph-yae/n:jcvhe-ndgle-taky6-2cmnk-w2eie-lftxv-uupda-cdzyz-3if3c-23qux-eqe/ic_state_layout/utils StateManager runs on a filesystem not supporting reflinks (attempted to reflink /home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/state/tip/system_metadata.pbuf => /home/bc20010540004/Desktop/mysite/.dfx/state/replicated_state/node-100/state/fs_tmp/scratchpad_0000000000000064/system_metadata.pbuf), running big canisters can be very slow


//环境创建成功，在本地跑起来了
//切换到一个新的终端（另一个canister），部署该网页
```

​	创建了`.dfx`隐藏的子目录，等；

​	看到`Listening on http://127.0.0.1:8000/`说明成功了；

###### 	b. 在另一个terminal窗口，部署该网页

```
bc20010540004@localehost:~/Desktop/mysite$ dfx deploy
Creating the "default" identity.
  - generating new key at /home/bc20010540004/.config/dfx/identity/default/identity.pem
Created the "default" identity.
Creating a wallet canister on the local network. //在本地创建了一个wallet canister
The wallet canister on the "local" network for user "default" is "rwlgt-iiaaa-aaaaa-aaaaa-cai"
Deploying all canisters.
Creating canisters...
Creating canister "mysite"...
"mysite" canister created with canister id: "rrkah-fqaaa-aaaaa-aaaaq-cai"
Creating canister "mysite_assets"...
"mysite_assets" canister created with canister id: "ryjl3-tyaaa-aaaaa-aaaba-cai"
Building canisters... //把canister在本地编译
Building frontend...
Installing canisters... //把canister在本地安装
Creating UI canister on the local network. //第一次装会先装个ui canister,分了两个canister_id分别给mysite和mysite_assets
The UI canister on the "local" network is "r7inp-6aaaa-aaaaa-aaabq-cai"
Installing code for canister mysite, with canister_id rrkah-fqaaa-aaaaa-aaaaq-cai
Installing code for canister mysite_assets, with canister_id ryjl3-tyaaa-aaaaa-aaaba-cai
Authorizing our identity (default) to the asset canister...
Uploading assets to asset canister... //将本地资源上传到asset canister
Starting batch.
Staging contents of new and changed assets:
  /main.css 1/1 (537 bytes)
  /main.css (gzip) 1/1 (297 bytes)
  /irisindex.html 1/1 (50 bytes)	//刚刚写的网页	
  /index.html 1/1 (664 bytes)
  /index.html (gzip) 1/1 (381 bytes)
  /index.js.map 1/1 (653722 bytes)
  /index.js.map (gzip) 1/1 (149005 bytes)
  /favicon.ico 1/1 (15406 bytes)
  /logo.png 1/1 (25397 bytes)
  /sample-asset.txt 1/1 (24 bytes)	//创建项目时的样例
  /index.js 1/1 (604263 bytes)
  /index.js (gzip) 1/1 (144724 bytes)
Committing batch.
Deployed canisters.
```

###### C. 怎样访问前端？

打开浏览器，输入`http://<mysite_assets_canister_id>.localhost:8000/` 即可访问。

​	a. 如果输入`http://localhost:8000/`，会显示 `Could not find a canister id to forward to.`

​	b. 注意上一步，`ui canister`分了两个`canister_id`分别给`mysite`和`mysite_assets`

```
http://ryjl3-tyaaa-aaaaa-aaaba-cai.localhost:8000/
```



<img src="C:\Users\Administrator.DESKTOP-3E455V4\AppData\Roaming\Typora\typora-user-images\image-20220223175111509.png" alt="image-20220223175111509" style="zoom: 50%;" />



### 二、主网账户和Cycles

每个安装好的SDK都会在本地产生一对公钥私钥；

这对密钥，对应的是 开发者principal id；

Principal ID用来获得部署权限，在本地还是在主网部署，id一样、但需要的wallet不同；

**（所以需要到主网上获得钱包、关联钱包。）**



#### （1）查看principal id：

```
bc20010540004@localehost:~/Desktop/mysite$ dfx identity get-principal 
7g3u7-sqvj7-yp73c-lmlih-ovnd2-ovb2g-x62e3-xgcoe-g7553-6w4yn-nqe
```

#### （2）查看密钥

```
bc20010540004@localehost:~/Desktop/mysite$ ls -l ~/.config/dfx/identity/default/
total 8
-r-------- 1 bc20010540004 bc20010540004 176 2月  23 15:09 identity.pem
-rw-rw-r-- 1 bc20010540004 bc20010540004  90 2月  23 17:18 wallets.json
```

​	`.pem`存着私钥，`.json`由私钥算出的公钥

#### （3）调用主网合约，获得自己的主网钱包：

```
bc20010540004@localehost:~/Desktop/mysite$ dfx canister --network=ic --no-wallet call fg7gi-vyaaa-aaaal-qadca-cai redeem '("x-x-x")' 
(principal "upiwr-waaaa-aaaal-qahva-cai")
```

​	调用主网合约 `fg7gi-vyaaa-aaaal-qadca-cai`

​	个人优惠码 `x-x-x`

​	返回的principal是（什么的？主网）canister id `upiwr-waaaa-aaaal-qahva-cai`

#### （4）关联主网钱包

```
bc20010540004@localehost:~/Desktop/mysite$ dfx identity --network=ic set-wallet upiwr-waaaa-aaaal-qahva-cai
Setting wallet for identity 'default' on network 'ic' to id 'upiwr-waaaa-aaaal-qahva-cai'
Wallet set successfully.
```

​	主网default身份、主网canister id、主网钱包，三者绑定

#### （5）查看主网钱包的余额

```
bc20010540004@localehost:~/Desktop/mysite$ dfx wallet --network=ic balance
14899987409418 cycles.
```

​	15TC左右（trillion cycles）



### 三、使用cycles在主网上部署合约

#### （1）部署

​	`--network=ic`是在主网上常有的命令；

​	设置每个canister可以使用0.4tc，（在主网上创建了两个canisters）

```
bc20010540004@localehost:~/Desktop/mysite$ dfx deploy --network=ic --with-cycles=400000000000
Deploying all canisters.
Creating canisters...
Creating canister "mysite"...
"mysite" canister created on network "ic" with canister id: "u2ph4-xiaaa-aaaal-qahwq-cai"
Creating canister "mysite_assets"...
"mysite_assets" canister created on network "ic" with canister id: "utmma-baaaa-aaaal-qahxa-cai"
Building canisters...
Building frontend...
Installing canisters...
Installing code for canister mysite, with canister_id u2ph4-xiaaa-aaaal-qahwq-cai
Installing code for canister mysite_assets, with canister_id utmma-baaaa-aaaal-qahxa-cai	//访问https://该id.ic0.app
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
  /index.js.map 1/1 (653722 bytes)
  /index.js.map (gzip) 1/1 (149005 bytes)
  /favicon.ico 1/1 (15406 bytes)
  /logo.png 1/1 (25397 bytes)
  /sample-asset.txt 1/1 (24 bytes)
  /index.js 1/1 (242077 bytes)
  /index.js (gzip) 1/1 (83698 bytes)
Committing batch.
Deployed canisters.

//这里可以查一下余额 //忘了！
//dfx wallet --network=ic balance
```

#### 	（2）访问前端（部署到主网上的程序）

```
https://utmma-baaaa-aaaal-qahxa-cai.ic0.app/
```

​	先是装一个service worker（一个很简短的程序，通过chainkey验证今后所有与icp区块链之间交互的内容）

<img src="C:\Users\Administrator.DESKTOP-3E455V4\AppData\Roaming\Typora\typora-user-images\image-20220223175252298.png" alt="image-20220223175252298" style="zoom:50%;" />

​	然后会下载index.html（为什么不是我写的hello world。原项目写好的？）（你本地应该有npm命名，dfx自动给你创建了前端资产。？）

<img src="C:\Users\Administrator.DESKTOP-3E455V4\AppData\Roaming\Typora\typora-user-images\image-20220223175346776.png" alt="image-20220223175346776" style="zoom:50%;" />

​	应该使用 `dfx new --no-frontend`



#### 四、回收未用完的cycles

#### 	（1）停止

```
bc20010540004@localehost:~/Desktop/mysite$ dfx canister --network=ic stop --all
Stopping code for canister mysite, with canister_id u2ph4-xiaaa-aaaal-qahwq-cai
An error happened during communication with the replica: error sending request for url (https://ic0.app/api/v2/canister/upiwr-waaaa-aaaal-qahva-cai/read_state): http2 error: protocol error: not a result of an error

//再试一次

bc20010540004@localehost:~/Desktop/mysite$ dfx canister --network=ic stop --all
Stopping code for canister mysite, with canister_id u2ph4-xiaaa-aaaal-qahwq-cai
Stopping code for canister mysite_assets, with canister_id utmma-baaaa-aaaal-qahxa-cai

```

#### 	（2）删除（提取回剩余的cycles）

```
bc20010540004@localehost:~/Desktop/mysite$ dfx canister --network=ic delete --all
Beginning withdrawl of 289993877266 cycles to canister upiwr-waaaa-aaaal-qahva-cai.
Setting the controller to identity princpal.
Installing temporary wallet in canister mysite to enable transfer of cycles.
Transfering 289993877266 cycles to canister upiwr-waaaa-aaaal-qahva-cai.
Deleting code for canister mysite, with canister_id u2ph4-xiaaa-aaaal-qahwq-cai
Beginning withdrawl of 287598958490 cycles to canister upiwr-waaaa-aaaal-qahva-cai.
Setting the controller to identity princpal.
Installing temporary wallet in canister mysite_assets to enable transfer of cycles.
Transfering 287598958490 cycles to canister upiwr-waaaa-aaaal-qahva-cai.
Deleting code for canister mysite_assets, with canister_id utmma-baaaa-aaaal-qahxa-cai
```

#### 	（3）查询余额

```
bc20010540004@localehost:~/Desktop/mysite$ dfx wallet --network=ic balance
14675662624345 cycles.
```



### 五、知识拓展

#### （1）使用ICP的技术优势：

​	48字节ChainKey公钥验证，毫秒级查询响应，两秒交易最终确认 ...

#### （2）Dapp架构：其他区块链 vs ICP的简化架构

- cryptokitties
- icp

#### （3）ICP白皮书（中文）



