## Ontology CLI 用户指南
* [CLI Account 命令](#cli-account-命令)

* [CLI Info Show 命令](#cli-info-show-命令)

* [CLI ASSET 命令](#cli-aSSET-命令)

* [CLI Setting 命令](#cli-setting-命令)

* [CLI Contract 命令](#cli-contract-命令)

```
用户可以使用以下命令直接启动ontology：
$./ontology

如果想了解ontology更多的命令选项，可以使用--help：
$./ontology --help
```

## CLI Account 命令

### 添加账户
创建一个包含秘钥对和地址的账户。
首先，选择秘钥类型，这可以通过使用-t选项实现。
```
$ ontology account add

Select a signature algorithm from the following:

  1  ECDSA
  2  SM2
  3  Ed25519

[default is 1]: 
```

如果选择的是EdDSA或者SM2，秘钥参数将会自动设置，因为这两种签名方法只支持一种设置。
```
SM2 is selected.
Use curve sm2p256v1 with key length of 256 bits and SM3withSM2 as the signature scheme.
```
或者
```
Ed25519 is selected.
Use curve 25519 with key length of 256 bits and Ed25519 as the signature scheme.
```
如果选择的是ECDSA，则下一步是选择曲线参数：
```
Select a curve from the following:

    | NAME  | KEY LENGTH (bits)
 ---|-------|------------------
  1 | P-224 | 224
  2 | P-256 | 256
  3 | P-384 | 384
  4 | P-521 | 521

This determines the length of the private key [default is 2]: 
```
这些曲线决定秘钥长度是224、256、385、521四种中的一种。这个参数可以通过-b选项来设置。
接下来，选择签名方式：
```
Select a signature scheme from the following:

  1  SHA224withECDSA
  2  SHA256withECDSA
  3  SHA384withECDSA
  4  SHA512withECDSA
  5  SHA3-224withECDSA
  6  SHA3-256withECDSA
  7  SHA3-384withECDSA
  8  SHA3-512withECDSA
  9  RIPEMD160withECDSA

This can be changed later [default is 2]: 
```
以上的选择可以使用--default选项来跳过，这将会使用默认设置。

私钥需要被加密，这要求有一个密码：
```
Enter a password for encrypting the private key:
Re-enter password:
```
可以使用encrypt命令重新加密私钥。

在选择完所有参数后，将会生成秘钥对。

公钥会被转换成通用地址，然后会输出账户可以公开的信息：
```
Create account successfully.
Address: `base58-address-string`
Public key: `hex-string`
Signature scheme: SHA256withECDSA
```
### 展示已存在的账户
```
$ ontology account list
*1  xxxxx
 2  xxxxx
```
*指示默认的账户。

可以使用-v选项查看账户的完整信息：
```
$ ontology account list -v
* 1 xxxxx
    Signature algorithm: ECDSA
    Curve: P-256
    Key length: 256 bits
    Public key: xxxx
    Signature Scheme: SHA256withECDSA

  ...
```
### 修改账户
修改账户设置，例如签名方法。可以通过list命令显示的序号来选择账户。

### 删除账户
通过list命令显示的序号来删除账户。

### 重新加密账户
修改账户密码
```
$ ontology account encrypt 1

Please enter the original password:
```
按照提示输入原来的密码，如果正确则输入新密码：
```
Enter a password for encrypting the private key:
Re-enter password:
```
## CLI Info Show 命令
使用 --help查看命令的具体用法：
```
Usage:
    ontology info [command options] [args]

Description:
    With ontology info, you can look up blocks, transactions, etc.

Command:
    version
    block
        --hash value                  block hash value
        --height value                block height value
    tx
        --hash value                  transaction hash value
```
### 查看版本号：
```
$ ./ontology info version
Result will show as follow:
Node version: 653c-dirty
```
### 查看某个高度对应的的区块信息：
```
$ ./ontology info block --height 12
将会显示如下结果：
{
	"Action": "getblockbyheight",
	"Desc": "SUCCESS",
	"Error": 0,
	"Result": {
		"Hash": "805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2",
		"Header": {
			"BlockRoot": "1ff293c1e15e1a37d449bba5aebda52280ceee645547f9f219ea903f7ad18386",
			"Bookkeepers": [
				"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
			],
			"ConsensusData": 5922267418785983000,
			"Hash": "805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2",
			"Height": 12,
			"NextBookkeeper": "TACATSTXT4E6UJHY57Ccv2TNBPGjbD9hfU",
			"PrevBlockHash": "bdbe264712d38f6d46bffdea8f6a9ab3ef73d343b043d31a0a0594758b73da1d",
			"SigData": [
				"016f3669a1998f2716e91093ca7946263433f92605ae9e6bf2b695145dbe24de5b38c93f8e91ae1d1f89626a4e87ac101f4344fb312c3e482b105a94f7d15f3fe9"
			],
			"Timestamp": 1524280951,
			"TransactionsRoot": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
			"Version": 0
		},
		"Transactions": [
			{
				"Attributes": [],
				"Fee": [],
				"Hash": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
				"NetworkFee": 0,
				"Nonce": 0,
				"Payload": {
					"Nonce": 1524280951763615000
				},
				"Sigs": [
					{
						"M": 1,
						"PubKeys": [
							"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
						],
						"SigData": [
							"01885e3078fe398987c5d89d650714d4e4ab9432ea5bcb98505cf4913d224920203c2f98b1ea24857e6af0f06b3bdf72d862bbe3b0989937cbe06c91775e2aa6e8"
						]
					}
				],
				"TxType": 0,
				"Version": 0
			}
		]
	},
	"Version": "1.0.0"
}

注意：
如果给出的区块高度无效，将会出现如下结果:
{
	"Action": "getblockbyheight",
	"Desc": "UNKNOWN BLOCK",
	"Error": 44003,
	"Result": "",
	"Version": "1.0.0"
}
```
### 查看某个hash值对应的区块信息：
```
$ ./ontology info block --hash 805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2
将会显示如下结果：
{
	"Action": "getblockbyheight",
	"Desc": "SUCCESS",
	"Error": 0,
	"Result": {
		"Hash": "805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2",
		"Header": {
			"BlockRoot": "1ff293c1e15e1a37d449bba5aebda52280ceee645547f9f219ea903f7ad18386",
			"Bookkeepers": [
				"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
			],
			"ConsensusData": 5922267418785983000,
			"Hash": "805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2",
			"Height": 12,
			"NextBookkeeper": "TACATSTXT4E6UJHY57Ccv2TNBPGjbD9hfU",
			"PrevBlockHash": "bdbe264712d38f6d46bffdea8f6a9ab3ef73d343b043d31a0a0594758b73da1d",
			"SigData": [
				"016f3669a1998f2716e91093ca7946263433f92605ae9e6bf2b695145dbe24de5b38c93f8e91ae1d1f89626a4e87ac101f4344fb312c3e482b105a94f7d15f3fe9"
			],
			"Timestamp": 1524280951,
			"TransactionsRoot": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
			"Version": 0
		},
		"Transactions": [
			{
				"Attributes": [],
				"Fee": [],
				"Hash": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
				"NetworkFee": 0,
				"Nonce": 0,
				"Payload": {
					"Nonce": 1524280951763615000
				},
				"Sigs": [
					{
						"M": 1,
						"PubKeys": [
							"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
						],
						"SigData": [
							"01885e3078fe398987c5d89d650714d4e4ab9432ea5bcb98505cf4913d224920203c2f98b1ea24857e6af0f06b3bdf72d862bbe3b0989937cbe06c91775e2aa6e8"
						]
					}
				],
				"TxType": 0,
				"Version": 0
			}
		]
	},
	"Version": "1.0.0"
}

注意：
如果给出的区块hash无效，将会出现如下结果:
{
	"Action": "getblockbyhash",
	"Desc": "UNKNOWN BLOCK",
	"Error": 44003,
	"Result": "",
	"Version": "1.0.0"
}
```
### 查看交易信息：
```
$ ./ontology info tx --hash 805e8ad8de2b28884656a393143dc07fea1cc83ddd849e1bbab814c476c26bb2
将会显示如下结果：
{
	"Action": "gettransaction",
	"Desc": "SUCCESS",
	"Error": 0,
	"Result": {
		"Attributes": [],
		"Fee": [],
		"Hash": "a750c36fca5922a6d4fe22d6b8664faa06f37d4c79c4624a91b10198322adf0e",
		"NetworkFee": 0,
		"Nonce": 0,
		"Payload": {
			"Nonce": 1524280951763615000
		},
		"Sigs": [
			{
				"M": 1,
				"PubKeys": [
					"12020352f5ea426d333bd4c0f174fc93e84348513a8d3778ac0c3beaca579cf1937696"
				],
				"SigData": [
					"01885e3078fe398987c5d89d650714d4e4ab9432ea5bcb98505cf4913d224920203c2f98b1ea24857e6af0f06b3bdf72d862bbe3b0989937cbe06c91775e2aa6e8"
				]
			}
		],
		"TxType": 0,
		"Version": 0
	},
	"Version": "1.0.0"
}

注意：
如果给出的交易hash无效，将会出现如下结果:
{
	"Action": "gettransaction",
	"Desc": "UNKNOWN TRANSACTION",
	"Error": 44001,
	"Result": "",
	"Version": "1.0.0"
}
```

## CLI Asset 命令
使用 --help查看命令的具体用法：
```
Usage:
    ontology asset [command options] [args]

Description:
    With this command, you can control assert through transaction.

Command:
    transfer
        --caddr     value                 smart contract address
        --from      value                 wallet address base58, which will transfer from
        --to        value                 wallet address base58, which will transfer to
        --value     value                 how much asset will be transfered
        --password  value                 use password who transfer from
    status
        --hash     value                  transfer transaction hash
```
### 转账：
```
$ ./ontology asset transfer --caddr=ff00000000000000000000000000000000000001 --value=500 --from TA6VvtGekMfinP97CTL9SH5WTowChUungL   --to TA7bRMkjMbP4JHhAVASN1fwpB56bi8aYUK  --password passwordtest
如果转账成功，将会显示如下结果：
[
	{
		"ContractAddress": "ff00000000000000000000000000000000000001",
		"TxHash": "e0ba3d5807289eac243faceb1a2ac63e8dee4eba208ceac193b0bd606861b729",
		"States": [
			"transfer",
			"TA6VvtGekMfinP97CTL9SH5WTowChUungL",
			"TA7bRMkjMbP4JHhAVASN1fwpB56bi8aYUK",
			500
		]
	}
]

否则，不会显示任何值。
```

### 查看资产状态：
```
$ ./ontology asset status --hash e0ba3d5807289eac243faceb1a2ac63e8dee4eba208ceac193b0bd606861b729
如果查询成功，将会显示如下结果：
[
	{
		"ContractAddress": "ff00000000000000000000000000000000000001",
		"TxHash": "e0ba3d5807289eac243faceb1a2ac63e8dee4eba208ceac193b0bd606861b729",
		"States": [
			"transfer",
			"TA6VvtGekMfinP97CTL9SH5WTowChUungL",
			"TA7bRMkjMbP4JHhAVASN1fwpB56bi8aYUK",
			500
		]
	}
]

否则，不会显示任何值。
```
## CLI Setting 命令：
使用 --help查看命令的具体用法：
```
Usage:
    ontology set [command options] [args]

Description:
    With ontology set, you can configure the node.

Command:
    --debuglevel value                 debug level(0~6) will be set
    --consensus value                  [ on / off ]
```
### 设置debuglevel：
```
$ ./ontology set --debuglevel 1
当设置成功，将会显示如下结果：
map[desc:SUCCESS error:0 id:0 jsonpc:2.0 result:true]
```
### 设置consensus：
```
$ ./ontology set --consensus on
当设置成功，将会显示如下结果：
map[desc:SUCCESS error:0 id:0 jsonpc:2.0 result:true]
```
## CLI Contract 命令
```
使用 --help查看命令的具体用法：
Usage:
    ontology contract [command options] [args]

Description:
    With this command, you can invoke a smart contract

Command:
    invoke
        --caddr      value               smart contract address that will be invoke
        --params     value               params will be

    deploy
        --type       value               contract type ,value: 1 (NEOVM) | 2 (WASM)
        --store      value               does this contract will be stored, value: true or false
        --code       value               directory of smart contract that will be deployed
        --cname      value               contract name that will be deployed
        --cversion   value               contract version which will be deployed
        --author     value               owner of deployed smart contract
        --email      value               owner email who deploy the smart contract
        --desc       value               contract description when deploy one
```
### 发布合约：
```
$ ./ontology contract deploy --type=1 --store=true --code=./deploy.txt --cname=testContract --cversion=0.0.1 --author=Yihen --desc="this is my first test contract" --email="name@emailaddr.com"
用户需要输入密码，当发布成功后，将会出现如下结果：
Deploy smartContract transaction hash: b68307e7659a53a10d3061a3e4721b5a152bd4e6e80b75002f5cc8b5294be493
```

### 调用合约：
```
$ ./ontology contract invoke --caddr TA6VvtGekMfinP97CTL9SH5WTowChUungL --params contract-params-need
用户需要输入密码，当调用成功后，将会出现如下结果：
invoke transaction hash:64976014daec682f8e3a4fc62c26f4636ac7be6bd548f67f24f62211394f8923
```
