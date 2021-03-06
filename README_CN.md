<div align="center">
  <img src="https://raw.githubusercontent.com/punicasuite/punica-python/master/punica.png" height="200" width="200"><br><br>
</div>

<!-- TOC -->

# Punica Cli

[English](./README.md) | 中文版

- [1. 概览](#1-概览)
- [2. 安装](#2-安装)
- [3. 快速开始](#3-快速开始)
- [4. 开始使用](#4-开始使用)
    - [4.1. 创建一个项目](#41-创建一个项目)
        - [4.1.1. 初始化一个新项目](#411-初始化一个新项目)
	    - [4.1.2. 创建一个Box项目](#412-创建一个Box项目)
    - [4.2. 编译](#42-编译)
    - [4.3. 部署](#43-部署)
    - [4.4. 调用](#44-调用)
    - [4.5. Node](#45-node)
    - [4.6. Scpm](#46-scpm)
    - [4.7. Smartx](#47-smartx)
    - [4.8. 测试](#48-测试)
    - [4.9. 钱包](#49-钱包)
- [5. 例子](#5-例子)
    - [5.1 检查版本号](#51-检查版本号)
    - [5.2 下载Box](#52-下载Box)
    - [5.3 编译合约](#53-编译合约)
    - [5.4 部署合约](#54-部署合约)
    - [5.5 调用合约](#55-调用合约)

## 1. 概览

[Punica Suite](https://punica.ont.io) 是基于[本体](https://ont.io)的第一个dApp开发框架， 为开发者提供了一整套开发工具，主要包括：

* [Punica Python CLI](https://github.com/punicasuite/punica-python) 和 [Punica TypeScript CLI](https://github.com/punicasuite/punica-ts) - 作为命令行工具，可以与主网、测试网或私网连接，能够让开发者便捷地使用本体智能合约，支持编译、部署、调用和测试功能。
* [Punica boxes](https://punica.ont.io/boxes/) - 提供多款dApp模板和应用案例。
* [Solo-chain](https://github.com/punicasuite/solo-chain/releases) - 本体的一键式（私有）区块链，便于开发者本地测试。 

Punica致力于提供完善的工具与整合的资源，让开发者快速上手dApp开发。

优势：
* Punica是本体第一套dApp开发框架，大大节省开发时间，让使用者事半功倍；
* 提供大量教材文档与教学视频，方便初学者快速上手并全面了解；
* 开发了智能合约测试框架，支持单元测试和功能测试，相比SDK测试更加容易便捷；
* 智能合约编译部署测试为一体，节省开发时间。SmartX中已集成debug功能，后续将支持命令行debug功能；
* Solo-chain方便用户实时查看链上数据，比在测试网或搭建本地网效率更高许多；
* 提供多种SDK和dAPI的案例，适用于各种用户群。



## 2. 安装

安装之前请先确保下面的工具已经安装

- [Python 3.7](https://www.python.org/downloads/release/python-370/)
- [Git](https://git-scm.com/)

然后，执行下面的命令进行安装

```shell
pip3 install punica
```
or

```shell
python setup.py install
```

## 3. 快速开始

如果想使用Punica更多的命令，请先创建一个Punica项目。


```shell
$ punica
Usage: punica [OPTIONS] COMMAND [ARGS]...

Options:
  -p, --project PATH  Specify a punica project directory.
  -v, --version       Show the version and exit.
  -h, --help          Show this message and exit.

Commands:
  compile  Compile the specified contracts to avm and...
  deploy   Deploys the specified contracts to specified...
  init     Initialize new and empty Ontology DApp...
  invoke   Invoke the function list in default-config or...
  node     Ontology Blockchain private net in test mode.
  scpm     Smart contract package manager，support...
  smartx   Ontology smart contract IDE,SmartX...
  test     Unit test with specified smart contract
  unbox    Download a Punica Box, a pre-built Ontology...
  wallet   Manager your ontid, account, asset.
```

## 4. 开始使用


### 4.1 创建一个项目

#### 4.1.1 初始化一个新项目

可以使用`punica init`命令创建一个空项目

```shell
$punica init --help
Usage: punica init [OPTIONS]

  Initialize new and empty Ontology DApp project.

Options:
  -h, --help  Show this message and exit.
```

使用下面的命令生成一个新项目

```shell
sss$ punica init
Downloading...
Unpacking...
Unbox successful. Enjoy it!
```

生成的项目结构如下：

```shell
sss:temp2 sss$ tree
.
├── LICENSE
├── README.md
├── contracts
│   ├── default-config.json
│   └── hello_ontology.py
├── punica-config.json
├── src
│   ├── hello.py
│   └── static
│       └── index.html
├── test
│   └── test_template.py
└── wallet
    └── wallet.json
```

- `contracts/`: 用于存放合约文件.
- `src/`: 用于存放dapp js和html等相关文件.
- `test/`: 合约代码测试文件.
- `wallet/`: 用于存放钱包文件.
- `punica-config.json` 用于配置区块链网络


#### 4.1.2 创建一个Box项目

Punica Box 是punica dapp模板库，你可以下载你感兴趣的项目，然后基于该项目进行创建你的dapp。

- 创建一个新文件夹

```shell
mkdir tutorialtoken
cd tutorialtoken
```

- 下载Box

```shell
punica unbox tutorialtoken
```


```shell
punica unbox --help
Usage: punica unbox [OPTIONS] BOX_NAME

  Download a Punica Box, a pre-built Ontology DApp project.

Options:
  -h, --help  Show this message and exit.
```

**Note**:

- 你可以使用`punica unbox <box-name>`免费下载任意的Box项目。
- 你可以在你的项目根目录使用punica的其他命令，也可以`-p` or `--project` 选项指定使用哪个项目。

### 4.2 编译

使用下面的命令编译你的合约


```shell
punica compile
```

如果执行成功，将会在contracts文件夹下生成build文件夹


```shell
contacts
    ├─build
    │      contract.avm
    │      contract_abi.json
```

如果你想使用punica更多的用法，你可以使用`punica compile --help`命令查看。

```shell
$ punica compile --help
Usage: punica compile [OPTIONS] CONTRACT_NAME

  Compile the specified contracts to avm and abi file.

Options:
  --contracts TEXT  Compile specified contracts files in contracts dir.
  --local BOOLEAN   Use local compiler.
  -h, --help        Show this message and exit.
```

- `--contracts`选项用于指定编译哪个合约文件

- `--local`选项用于指定使用哪个编译器


### 4.3 部署

部署之前，你要关心两个配置文件，一个是`punica-config.json`,该文件配置使用的区块链网络，另一个配置文件是contracts目录下面的default-config.json文件，
该文件用于配置部署合约的参数信息和调用合约中函数的参数。

部署命令

```shell
$ punica deploy
```

例子：
```shell
$ punica deploy
Using network 'privateNet'.

Running deployment: hello_ontology.avm
	Deploying...
	Deploy to: cb9f3b7c6fb1cf2c13a40637c189bdd066a272b4
Deploy successful to network...
	 Contract address is cb9f3b7c6fb1cf2c13a40637c189bdd066a272b4
	 Txhash is 041db938710e0c2977bbb8af1bdf97a3efae8256baa0ec74980c98734e25f650
```

如果你想知道更多的用法你可以使用

```shell
sss:punica-init-default-box sss$ punica deploy -h
Usage: punica deploy [OPTIONS]

  Deploys the specified contracts to specified chain.

Options:
  --network TEXT  Specify which network the contracts will be deployed.
  --avm TEXT      Specify which avm file will be deployed.
  --wallet TEXT   Specify which wallet file will be used.
  --config TEXT   Specify which deploy config file will be used.
  -h, --help      Show this message and exit.
```

- `--network TEXT` 用于指定使用的网络,默认使用punica-config.json里的配置文件
- `--avm TEXT` 用于指定使用的avm，默认使用defaul-config.json中配置的avm文件
- `--wallet TEXT`用于指定使用的钱包文件，默认使用wallet文件夹下的wallet.json文件
- `--config TEXT`用于指定使用的配置文件，默认使用defaul-config.json

### 4.4 调用

调用之前，请确保default-config.json文件中已经配好合约方法需要的参数。

`default-config.json`配置例子,省略了部分内容，完整内容请看[init box](https://github.com/punica-box/punica-init-default-box/blob/master/contracts/default-config.json)

```json
{
    "defaultWallet": "wallet.json",
    "password": {
        "AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ": "password",
        "AecaeSEBkt5GcBCxwz1F41TvdjX3dnKBkJ": "password",
        "AQvZMDecMoCi2y4V6QKdJBtHW1eV7Vbaof": "password"
    },
    "deployConfig": {
        "name": "contract name ",
        "version": "contract version",
        "author": "the author of contract",
        "email": "email address",
        "desc": "a description for your contract",
        "needStorage": true,
        "payer": "AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ",
        "gasPrice": 0,
        "gasLimit": 31000000
    },
    "invokeConfig": {
        "abi": "hello_ontology_abi.json",
        "defaultPayer": "AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ",
        "gasPrice": 0,
        "gasLimit": 20000,
        "functions": [
            {
                "operation": "testByteArrayListAndStr",
                "args": [
                    {
                        "bytearrayList": [
                            "ByteArray:Hello",
                            "ByteArray:world"
                        ]
                    },
                    {
                        "msgStr": "String:hello"
                    }
                ],
                "signers": {},
                "preExec": true
            },
            {
                "operation": "testStructList",
                "args": [
                  {
                      "structList": [
                        [
                          "String:hello",
                          1
                        ],
                        [
                          "String:hello2",
                          2
                        ]
                      ]
                  }
                ],
                "signers": {},
                "preExec": true
            },
            {
                "operation": "testStructListAndStr",
                "args": [
                  {
                      "structList": [
                          [
                            "String:hello",
                             1
                          ],
                          [
                            "String:hello2",
                             2
                          ]
                      ]
                  },
                  {
                    "msgStr": "String:test"
                  }
                ],
                "signers": {},
                "preExec": true
            }
        ]
    }
}
```

请注意参数值的配置，
- "String:test", "String"表示合约中的函数需要的参数类型是String。
- "ByteArry:test", "ByteArray"表示合约中的函数需要的参数类型是ByteArray。
- "Address:AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ",表示将参数`AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ`按照Address的格式转换成字节数组。
- "Hex:0a"表示将参数`0a`按照hex的形式转换成字节数组


`default-config.json`配置完成后，可以通过下面的命令查看可以调用的函数


```shell
punica invoke list
```

输出结果是

```shell
sss:punica-init-default-box sss$ punica invoke list
All Functions:
	 testHello
	 testNumList
	 testNumListAndStr
	 testStrListAndStr
	 testByteArrayListAndStr
	 testStructList
	 testStructListAndStr
```

使用下面的命令运行指定函数
```shell
sss$ punica invoke --functions testHello
Using network 'privateNet'.

Running invocation: hello_ontology_abi.json
Unlock default payer account...
Invoking  testHello
Invoke successful
Invoke result: ['01', '64', '74657374', '74657374', '0a', '8f651d459b4f146380dab28e7cfb9d4bb9c3fcd1']
```

如果你想查看invoke更多的信息，你可以执行下面的命令
```shell
$ punica invoke -h
Usage: punica invoke [OPTIONS] COMMAND [ARGS]...

  Invoke the function list in default-config or specify config.

Options:
  --network TEXT    Specify which network the contracts will be deployed.
  --wallet TEXT     Specify which wallet file will be used.
  --functions TEXT  Specify which function will be executed.
  --config TEXT     Specify which config file will be used.
  --preexec TEXT    preExec the function.
  -h, --help        Show this message and exit.

Commands:
  list  List all the function in default-config or...
```

- `--functions TEXT`表示指定要执行的函数，可以一次指定多个函数，例如：
`punica invoke --functions testHello,testNumList`

- `--preexec TEXT`表示预执行，预执行表示不会将状态更新到区块链，适合于查询的函数。
其他的配置信息请参看上面的讲解。


### 4.5 Node


```shell
$ punica node
Usage: punica node [OPTIONS]

   Ontology Blockchain private net in test mode. please download from
   https://github.com/punicasuite/solo-chain/releases

Options:
   -h, --help  Show this message and exit.
```

### 4.6 Scpm

```shell
$ punica scpm
Usage: punica scpm [OPTIONS]

   smart contract package manager，support download and publish.

Options:
   -h, --help  Show this message and exit.

```
### 4.7 Smartx

```shell
$ punica smartx

Please go to Smartx for debugging smart contracts:
http://smartx.ont.io/#/
```
### 4.8 测试

```shell
$ punica test -h
Usage: punica test [OPTIONS] COMMAND [ARGS]...

  Unit test with specified smart contract

Options:
  --file TEXT  Specify which test file will be used.
  -h, --help   Show this message and exit.

Commands:
  template  generate test template file
```

### 4.9 钱包

```shell
$ punica wallet
Usage: punica wallet [OPTIONS] COMMAND [ARGS]...

   Manager your asset, ontid, account.

Options:
   -h, --help  Show this message and exit.

Commands:
   account  Manager your account.
   asset    Manager your asset, transfer, balance,...
   ontid    Manager your ont_id, list or add.

```

## 5. 例子

### 5.1 检查版本号

```shell
$ punica -v
0.0.9
```

### 5.2 下载Box

```shell
$ punica unbox tutorialtoken
Downloading...
Unpacking...
Unbox successful. Enjoy it!
```

### 5.3 编译合约


```shell
$ tree
.
├─contracts
│     └─build
│
├─src
│  └─static
│      ├─css
│      │  └─fonts
│      ├─html
│      └─js
└─wallet
```

```shell
$ punica compile
Compile...
        Compile oep4_token.py...
        Generate abi file and avm file successful...
        Enjoy your contract:)
Now we are finished :)
```

```shell
$ tree
.
│
├─contracts
│     └─build
│
├─src
│  └─static
│      ├─css
│      │  └─fonts
│      ├─html
│      └─js
└─wallet
```

```shell
$ tree build /F
\TUTORIALTOKEN\BUILD
    oep4_token.avm
    oep4_token_abi.json
```


### 5.4 部署合约

编译成功后，可以部署合约到Ontology网络

```shell
$ punica deploy
Using network 'testNet'.

Running deployment: oep4_token.avm
        Deploying...
        ... 0x0131c56b6a00527ac46a51527ac46a00c3044e616d659c6409006599096c7566
        Please input payer account password:
        Deploy to: 0xe4d6db237a830ce10f7476e410e61aad41bf9244
Deploy successful to network...
        ... 0x05a2502f7b8283f02915ba3ec7f712304fcce83ed98360fa3193a0b9e19ef87f
Enjoy your contract!
```
如果合约已经部署过，将会得到下面的输出。

```shell
$ punica deploy
Using network 'testNet'.

Running deployment: oep4_token.avm
        Deploy failed...
        Contract has been deployed...
        Contract address is 0xcb9f3b7c6fb1cf2c13a40637c189bdd066a272b4...
Enjoy your contract:)
```

### 5.5 调用合约


```shell
$ punica invoke
Using network 'testNet'.

Running invocation: oep4_token_abi.json
Unlock default payer account...
        Unlock account: ANH5bHrrt111XwNEnuPZj6u95Dd6u7G4D6
        Please input account password:
        Unlock successful...
Invoking Name...
        Invoke successful...
                ... Invoke result: 4458546f6b656e
Invoking Symbol...
        Invoke successful...
                ... Invoke result: 4458
Invoking Decimal...
        Invoke successful...
                ... Invoke result: 08
Invoking TotalSupply...
        Invoke successful...
                ... Invoke result: 000080f64ae1c7022d15
Invoking BalanceOf...
        Invoke successful...
                ... Invoke result:
Invoking Transfer...
Unlock signers account...
        Unlock account: ANH5bHrrt111XwNEnuPZj6u95Dd6u7G4D6
        Please input account password:
        Unlock successful...
        Invoke successful...
                ... txHash: 0x8bfcebe076576bb35833d97ca0b80cffe82872a6545fccf36266702ba6b65c8b
Invoking TransferMulti...
Unlock signers account...
        Unlock account: ANH5bHrrt111XwNEnuPZj6u95Dd6u7G4D6
        Please input account password:
        Unlock successful...
        Unlock account: AazEvfQPcQ2GEFFPLF1ZLwQ7K5jDn81hve
        Please input account password:
        Unlock successful...
		            ... txHash: 0xc6c4fc178b3598ad329986782d8c6ffdc4858ae208d48c7ce429532cec39fc68
Invoking Allowance...
Unlock signers account...
        Unlock account: ANH5bHrrt111XwNEnuPZj6u95Dd6u7G4D6
        Please input account password:
        Unlock successful...
        Invoke successful...
                ... txHash: 0x05e78cf0d97d8b8f86ea934f051140bb840b728d8117b177d54d24ecceef3b8b
Invoking TransferFrom...
Unlock signers account...
        Unlock account: ANH5bHrrt111XwNEnuPZj6u95Dd6u7G4D6
        Please input account password:
        Unlock successful...
        Invoke successful...
                ... txHash: 0xc3e8bfe31321f27f6b0c49204bf94fc3c4715d4a5dc3e9e96b3c2cf21c5fa998

```
