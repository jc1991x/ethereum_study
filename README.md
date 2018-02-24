
## create private blockchain network

下载[geth](https://geth.ethereum.org/downloads/)
创建一个genesis.json起源文件

```javascript

{
    "config": {
        "chainId": 15,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
    "difficulty": "10000",
    "gasLimit": "2100000",
    "alloc": {
        "7df9a875a174b3bc565e6424a0050ebc1b2d1d82": {
            "balance": "300000"
        },
        "f41c74c9ae680c1aa78f42e5647a62f353b7bdde": {
            "balance": "400000"
        }
    }
}

```

进入genesis.json所在目录，执行


```
geth init ./genesis.json --datadir mychaindata
geth --datadir ./mychaindata --port "30304" --nodiscover

```

## 在创建的私有网络中挖矿 

```
先利用rpc连上以创建的区块链,rpc endpoint可以服务的时候找到
geth attach rpc:/Users/joe/Workspace/blockchain/private_network/mychaindata/geth.ipc

连接成功后，可以发现这是一个javascript客户端，可以命令和服务端交互。


首先挖坑之前需要创建账户：
personal.newAccount()
输入密码，账户创建成功。
eth.accounts
查看现有账户
miner.setEtherbase(eth.accounts[0])
miner.start(1)

查看余额，利用web3
web3.eth.getBalance(eth.accounts[0])
或者
eth.getBalance(eth.accounts[0])

可以看到 balance增加的很快，每一次有新的block生成，balance就增加

转换格式
web3.fromWei(eth.getBalance(eth.accounts[0]),"ether"). //finne
```


## 区块链技术的运用案例
除了熟知的比特币，还有什么其他方面的运用？
资产交易方式: ShapeShift ： https://shapeshift.io/#/coins
smart contract: 智能合约：rootstock  https://www.rsk.co/  一个智能合约平台
cloud storage: https://storj.io/.  区块链本质为数据库，所以这是云存储技术的革命，数据将不再存储在某一个地方，而是可以存在任何一个地方。从官网的介绍可以了解到，我甚至可以出租我的硬盘空间。这种存储方式，完全的不同于现在的所有云盘，iclound等方式。数据是存在于世界上任何一台电脑上的，而非某个机构某个组织。而访问权，确保只有自己。至于下载速度，由于是分布式无数节点的下载，所以极快Blazing Fast。



## 四个基于以太坊Ethereum建立的项目

augur： http://www.augur.net/  市场预测网站

slock.it : 此项目目标是允许互联网的一切可以进行租、买卖、分享

ujo: https://ujomusic.com/.  一个音乐相关的项目，此项目目标在于解决音乐版权问题，让艺术家能够直接获得用户的付费。 这实在是保护版权的很好方式。 

akasha ： https://akasha.world/  此项目的目标宏伟，试图构建一个行星级别的文件系统。



## tools of ethereum ecosystem

what is geth ,parity , solidity , remix, truffke, webpack, angular, etc...?

* blockchain noods : geth/parity/CPP-Ethereum.  简单来说，这相当于客户端，在我们的机器上，跑一个节点，将这个节点联网加入集群。 它们的共同点是都实现了以太网协议（Ethereum Protocol）,只是用不同的编程语言实现。

* browser：  MetaMask/MIST.  它们是一种可以连接浏览器和区块链的应用程序. MetaMask是浏览器插件，MIST是web应用

* solidity： 高级编程语言，编写完的代码，需要用solc编译成字节码，跑在EVM里面。语法和javascript类似

* remix： IDE in the cloud : remix.ethereum.org , 网页版的编辑器，可以写代码，编译，调试。但国内访问速度很慢。

* web3.js、 ethjs ： 框架、库，它可以使浏览器能够和区块链（的http-rpc）进行连接通讯。

* thuffle, embbark: solidity开发框架，加速开发、测试、管理智能合约


* angular,vuejs,react,redux: 接触过web开发的都很熟悉，这是一些前端SPA框架。它们之所以被归到这个生态系统，是因为它们可以开发web应用，然后在web应用中使用web3库与区块链进行交互。

* webpack, browserify, node: 都是javascript相关的东西。

## 什么是smart contracts 
这是区块链技术里的核心关键字，智能合约。

所谓智能合约（Smart Contract），是密码学家Nick Szabo在1994年首次提出以数字形式定义的一系列承诺（promises） ，包括合约参与方可以在上面执行这些承诺的协议。智能合约一旦设立指定后，能够无需中介的参与自动执行，并且没有人可以阻止它的运行。

区块链为智能合约提供可信执行环境，智能合约为区块链扩展应用。

智能合约的关键字：

1. autonomy： 智能合约一旦设立指定后，能够无需中介的参与自动执行，并且没有人可以阻止它的运行。
2. trust：智能合约运行在区块链中，这意味着你的文档被加密存储在区块链的分布式总帐本里，你永远不用担心会丢失。无需保管在任何人任何组织那里。
3. back-ups: 文档不止一个备份，而是会被复制到每一个节点。所以无需但心，某一个节点损坏了你的文件会丢失。
4. safety： 安全性是互联网应用中很重要的一部分，很多时候你要防止各种黑客攻击。而智能合约运行在区块链上，没人可以修改。
5. speed： 执行速度快。
6. saving： 没有中间人省事省钱。

个人理解，区块链里的“智能合约”就是用solidity写的代码，而这段代码运行在以太坊上时表现出来的特性符合“智能合约”的概念，所以把这些代码叫做智能合约。



## 创造自己的数字货币
数字货币在以太坊中可以代表一切可交易的东西。

根据官网指南：https://www.ethereum.org/token
很容易就能达成区块链之旅的第一个成就，发行自己的数字货币。


## 安装MetaMask，获取以太币
MetaMask是一个浏览器插件，
从官网 https://metamask.io/ 安装这个chrome插件。
MetaMask可以连接到以太坊主网络以及多个测试网络，甚至是自己搭建的本地网络。这里的网络指的是运行的blockchain。

安装完后，设置密码，创建account，然后左上角选择连接到Ropsten Test Net。接下来就可以搞一些测试以太币来玩了。为什么不连主网？因为主网的以太币已经天价了，不适合玩。

从[coincap](http://coincap.io/)可以实时查看当前币圈的币价如何。看了下，目前比特币一枚10478美元，以太币一枚878美元。


所以如何开始搞一些测试网的币：

打开https://faucet.metamask.io/
网页会读取metamask中当前帐号信息。界面中可以看到faucet的帐号和自己的帐号，
可以选择索取，或捐赠。
点击索取1ether , 确认过后生成一单交易，在transactions下面可以点击通过etherscan追踪交易状态，通常10几秒就交易完成了。然后自己的帐号下，就多了1ether。多点几次就多几个。

有了以太币之后，接下来体验转账，也就是把以太币转移到别的账户。上面的获取以太币，其实也是一次转账，把测试网的faucet帐号的币转到自己的号中。 

可以在metamask中创建account2，体验下自己的两个号之间互转。只需点send，然后输入收取方的account地址就行。

## 在remix上写solidity代码
[solidity官方文档](https://solidity.readthedocs.io/en/develop/)
[solidity中文文档](http://wiki.jikexueyuan.com/project/solidity-zh/)
毕竟有多种语言基础，瞄几眼就差不多了。语法不复杂。
反正先从helloworld的开始写。

![](/media/15192412166392.jpg)


在remix的代码编辑器里写代码，然后点compile下面点start to compile按钮。编译成功就可以切换到旁边的Run tab了。

![](/media/15192413226957.jpg)


run下面有Environment，acoount等选项，其中的account就是metamask当前的account，默认填好了。
点击create。 metamask很灵敏的捕捉到了这一操作，并弹窗询问是否同意创建新的“智能合约”。弹窗的信息里，可以了解到，创建新的合约要花费0.000197的以太币。点击submit，成功创建。

![](/media/15192417773150.jpg)


但这个helloworld智能合约，没啥用。

接下来写点有用的。

开始写之前，先设置环境，
![](/media/15192425002524.jpg)



* Javascript VM ： 这个环境内置了一个基于内存的blockchain node，关闭浏览器，一切都会重置，方便测试。
* Injected Web： 这个环境会和metamask发生交互。metamask的原理其实是连接了一个远程的blockchain node。metamask在浏览器和blockchain之间扮演一个中间人角色。
* Web3 provider： 这个环境要自己输入一个运行中的blockchain node的http rpc链接，让web3能连上。


先选择javascript VM ，这个环境，预置了5个拥有100个以太币的账户，最方便做开发环境。

![](/media/15192434654841.jpg)


这是一个有操作的合约， 输入一个数字，返回这个数字*10的结果。

编译，然后在create前面输入20，点create，合约就创建了。生成了一个合约的地址：

0x692a70d2e424a56d2c6c27aa97d1a86395877b3a

这个地址很关键。它是可以被访问并调用的。

用传统程序的角度理解这个流程，就是点create的时候，发布了一个可供远程调用的程序，返回一个api地址，
通过api地址，可以执行这段程序里的代码。

窗口下面有个模拟操作，点击getMyVar，也就是智能合约里面暴露的public方法，输出200。

可见getMyVar成了一个可以远程调用的入口，能执行代码，并返回结果。


## 深度理解去中心化
如果不理解”去中心化“，就不能理解区块链的价值。毕竟区块链是去中心化的代表。
于是有必要深入理解下什么是去中心化。
[通读此文足矣](https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274)




## web3
* 一个纯javascript的库
* 能够连接到blockchain node的 json-RPC

阅读[github wiki](https://github.com/ethereum/wiki/wiki/JavaScript-API) 可以了解全部用法




## 部署合约

下载安装 [mist](https://github.com/ethereum/mist/releases
)

部署合约，需要把solidity文件编译成字节码，调用创建合约函数，等矿工确认，然后部署到区块链中，这些操作用代码实现有些繁琐。 [代码方式看wiki](https://github.com/ethereum/wiki/wiki/JavaScript-API#web3ethcontract)

利用mist部署合约是个比较简单的方式，界面可视化操作，轻松愉快。

![](/media/15193498092202.jpg)




## 通过浏览器访问blockchain，调用合约

开启私网（本地区块链）：

```
geth --datadir ./mychaindata  --rpc --rpccorsdomain "*"  --rpcapi eth,web3,personal

开私网需要加的参数。 
--rpc ： 允许开启jsonrpc端口，这样浏览器才能通过web3连接上来
--rpccorsdomain: 允许连接的域名
--rpcapi:  允许web3调用的api

```

## 更加方便的创建私人区块链的两种方式

前面采用geth命令创建是一种方式，但是geth创建的私有链，环境和主网一致，一旦有交易、新的block产生，需要等矿工开采确认，对于开发环境来说，耗时且不够方便。于是社区推出两种方式。

* testrpc： 安装和创建私有链只需两行命令

```
npm install ethereumjs-testrpc -g
testrpc
``` 
testrpc 内置了10个account方便测试。

* ganache ： [ganache](http://truffleframework.com/ganache/)也是一个 “ONE CLICK BLOCKCHAIN” ,但这个比起testrpc，还多了可视化用户界面，同样内置模拟account，可以随时查看account的状态，查看log，交易等信息。

## truffle

[truffle](http://truffleframework.com/)不仅是最受欢迎的ethereum开发框架，它真正能做到让区块链开发更简单。它集成了remix, geth, web3等一大堆常用工具，使的写代码、测试、部署都更加方便。

truffle已经出了npm版本，在linux、mac、window下都能使用，安装超简单：

```
npm install truffle -g

一键初始化一个带前端的区块链项目
truffle unpack webpack

初始化的项目，可以直接运行npm命令打开应用的前端
npm run dev 

但是要使应用成功连接区块链，需要先在app.js里配置好区块链的json-rpc地址。

使用truffle命令进行合约的操作：

首先配置truffle.js 连接到区块链的json-rpc

编译合约：
truffle compile
部署合约：
truffle migrate
运行测试：
truffle test
```


