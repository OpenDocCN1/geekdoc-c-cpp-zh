

通过发送消息（例如转账指令），让其他人相信这些消息来自 Alice，从而冒充她。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_611_0.png)

**图 10.9** 使用 DSA 的公钥签名交换

### 10.4.3 验证签名

JDK 自带 keytool 程序，这是一个用于生成和管理一组证书的命令行工具。我们期望最终该工具的功能会嵌入到其他更友好的程序中。但现在，我们将使用 keytool 来演示 Alice 如何对文档签名并将其发送给 Bob，以及 Bob 如何验证该文档确实是由 Alice 而非冒名顶替者签名的。

keytool 程序管理密钥库——即证书和私钥/公钥对的数据库。密钥库中的每个条目都有一个别名。下面展示了 Alice 如何创建密钥库 alice.certs，并生成别名为 alice 的密钥对：

```text
keytool -genkeypair -keystore alice.certs -alias alice
```

创建或打开密钥库时，系统会提示你输入密钥库口令。在本例中，直接使用 secret 即可。如果你使用由 keytool 生成的

如果 Bob 想检查自己拿到的证书是否正确，他可以打电话给 Alice，在电话中核对证书指纹。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_613_0.png)

> **注意：** 一些证书颁发机构会在其网站上公布证书指纹。例如，要检查 `jre/lib/security/cacerts` 目录中的 DigiCert 证书，可使用 `-list` 选项：

```text
keytool -list -v -keystore jre/lib/security/cacerts
```

此密钥库的口令是 changeit。该密钥库中的其中一张证书是：

```text
Owner: CN=DigiCert Assured ID Root G3, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer: CN=DigiCert Assured ID Root G3, OU=www.digicert.com, O=DigiCert Inc, C=US
Serial number: ba15afa1ddfa0b54944afdc24a06cec
Valid from: Thu Aug 01 14:00:00 CEST 2013 until: Fri Jan 15 13:00:00 CET 2038
Certificate fingerprints:
         SHA1:  F5:17:A2:4F:9A:48:C6:C9:F8:A2:00:26:9F:DC:0F:48:2C:AB:30:89
         SHA256: 75:37:CB:88:4C:47:09:0C:AB:36:55:1B:A6:F4:5D:B8:40:68:0F:BA:
                 16:6A:95:2D:B1:00:71:7A:35:3F:C2
```

你可以访问网站 www.digicert.com/digicert-root-certificates.htm 来检查你的证书是否有效。

一旦 Bob 信任了该证书，他就可以将其导入自己的密钥库。

```text
keytool -importcert -keystore bob.certs -alias alice -file alice.cer
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_613_1.png)

> **警告：** 永远不要将你不完全信任的证书导入密钥库。一旦证书被添加到密钥库中，任何使用该密钥库的程序都会认定该证书可用于验证签名。

现在，Alice 可以开始向 Bob 发送已签名的文档了。jarsigner 工具用于对 JAR 文件进行签名和验证。Alice 只需将要签名的文档添加到一个 JAR 文件中。

```text
jar cvf document.jar document.txt
```

然后，她使用 jarsigner 工具向文件添加签名。她需要指定密钥库、JAR 文件以及要使用的密钥别名。

```text
jarsigner -keystore alice.certs document.jar alice
```

Bob 收到文件后，使用 jarsigner 程序的 -verify 选项。

```text
jarsigner -verify -keystore bob.certs document.jar
```

Bob 无需指定密钥别名。jarsigner 程序会在数字签名中找到密钥所有者的 X.500 名称，并在密钥库中查找匹配的证书。

如果 JAR 文件未被破坏且签名匹配，jarsigner 程序会输出：

```text
jar verified.
```

否则，程序会显示一条错误消息。

### 10.4.4 身份验证问题

假设你收到了朋友 Alice 发来的一条消息，它使用我们刚刚展示的方法，用她的私钥签名。你可能已经有她的公钥，或者可以轻松地向她要一份副本，或从她的网页上获取。然后，你可以验证这条消息确实是由 Alice 撰写且未被篡改。现在，假设你收到一个陌生人的消息，他声称代表一家知名软件公司，敦促你运行消息附带的程序。这个陌生人甚至把他的公钥副本发给你，以便你验证消息确实是他撰写的。你检查后发现签名有效。这证明该消息是用匹配的私钥签名的，且未被破坏。

小心：*你仍然不知道消息是谁写的。* 任何人都可以生成一对公私钥，用私钥对消息签名，然后将签名后的消息和公钥发送给你。确定发送者身份的问题被称为*身份验证问题*。

解决身份验证问题的通常方法很简单。假设陌生人和你有一个你们都信任的共同熟人。假设陌生人当面与你的熟人见面，并交给他一张存有公钥的磁盘。你的熟人后来见到你，向你保证他见过那个陌生人，而且那个陌生人确实在那家知名软件公司工作，然后把磁盘交给你（见图 10.10）。这样，你的熟人就为陌生人的真实性做了担保。

事实上，你的熟人并不需要真的见到你。他可以用自己的私钥对陌生人的公钥文件签名（见图 10.11）。

当你拿到公钥文件时，你可以验证朋友的签名；因为你信任他，所以你有理由相信他在签名之前确实核实过陌生人的身份凭证。

然而，你也许没有这样的共同熟人。某些信任模型假定总是存在一条“信任链”——一条由相互熟识的人组成的链——因此你信任该链中的每一个成员。当然，在实践中，

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_616_0.png)

图 10.11  通过受信任中间人的签名进行身份验证

### 10.4.5 证书签名

在 10.4.3 节“验证签名”（第 589 页）中，你看到了 Alice 如何使用自签名证书向 Bob 分发公钥。然而，Bob 需要与 Alice 核对指纹，以确保证书有效。

假设 Alice 想给同事 Cindy 发送一条签名消息，但 Cindy 不想费心去验证大量的签名指纹。现在假设有一个 Cindy 信任的实体来验证签名。在本例中，Cindy 信任 ACME 软件公司的信息资源部（Information Resources Department）。

该部门运营着一个*证书颁发机构*（CA）。ACME 的每位员工的密钥库中都有 CA 的公钥，这些公钥由系统管理员安装，管理员仔细核对了密钥指纹。CA 会对 ACME 员工的密钥进行签名。当他们安装彼此的密钥时，密钥库会隐式信任这些密钥，因为它们是由受信任的密钥签名的。

下面你可以模拟这个过程。创建一个密钥库 `acmesoft.certs`。生成密钥对并导出公钥：

```text
keytool -genkeypair -keystore acmesoft.certs -alias acmeroot
keytool -exportcert -keystore acmesoft.certs -alias acmeroot -file acmeroot.cer
```

公钥被导出到一张“自签名”证书中。然后，将它添加到每个员工的密钥库中：

```text
keytool -importcert -keystore cindy.certs -alias acmeroot -file acmeroot.cer
```

为了让 Alice 能向 Cindy 以及 ACME 软件公司的其他所有人发送消息，她需要将自己的证书带到信息资源部并请其签名。遗憾的是，`keytool` 程序缺少这一功能。在本书的配套代码中，我们提供了一个 CertificateSigner 类来弥补这一空缺。ACME 软件公司的一名授权工作人员会验证 Alice 的身份，并生成一张已签名的证书，如下所示：

```text
java CertificateSigner -keystore acmesoft.certs -alias acmeroot \
  -infile alice.cer -outfile alice_signedby_acmeroot.cer
```

证书签名程序必须能够访问 ACME 软件公司的密钥库，并且工作人员必须知道密钥库口令。显然，这是一项敏感操作。

Alice 将文件 `alice_signedby_acmeroot.cer` 交给 Cindy 以及 ACME 软件公司的其他任何人。或者，ACME 软件公司可以直接将该文件存放在公司目录中。请记住，此文件包含 Alice 的公钥，以及 ACME 软件公司关于该密钥确实属于 Alice 的声明。

现在，Cindy 将已签名的证书导入她的密钥库：

```text
keytool -importcert -keystore cindy.certs -alias alice -file alice_signedby_acmeroot.cer
```

密钥库会验证该密钥是否由密钥库中已有的受信任根密钥签名。系统*不会*要求 Cindy 验证证书指纹。

一旦 Cindy 添加了根证书以及那些经常给她发送文档的人的证书，她就再也不必为密钥库操心了。

