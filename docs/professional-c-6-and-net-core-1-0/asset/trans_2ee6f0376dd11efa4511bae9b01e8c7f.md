

非对称加密密钥。

使用对称密钥时，可以使用相同的密钥进行加密和解密。使用非对称加密时，加密和解密使用不同的密钥：公钥和私钥。用公钥加密的东西可以用对应的私钥解密。这也可以反过来使用：用私钥加密的东西可以用对应的公钥解密，但不能用私钥解密。从另一个密钥计算出私钥或公钥在实践中是不可能的。

公钥和私钥总是成对创建。公钥可以向所有人公开，甚至可以放在网站上，但私钥必须安全地锁好。以下是一些示例，演示公钥和私钥如何用于加密。

如果 Alice 向 Bob 发送消息（见图 24.1），并且她希望除了 Bob 之外的任何人都无法阅读该消息，她会使用 Bob 的公钥。消息使用 Bob 的公钥加密。Bob 打开消息并可以使用他秘密存储的私钥解密它。这种密钥交换保证了除了 Bob 之外没有人可以阅读 Alice 的消息。

![](img/3d365b72b289213a91ade7eb366b8f35_868_0.png)

## 图 24.1

然而，有一个问题：Bob 不能确定邮件来自 Alice。Eve 可以使用 Bob 的公钥加密发送给 Bob 的消息并假装是 Alice。我们可以使用公钥/私钥扩展这一原理。让我们再次从 Alice 向 Bob 发送消息开始。在 Alice 使用 Bob 的公钥加密消息之前，她添加自己的签名并使用自己的私钥加密签名。然后她使用 Bob 的公钥加密邮件。因此，可以保证除了 Bob 之外没有人可以阅读该消息。当

在 RSA 实验室开发，比 SHA1 更快。SHA1 对抗暴力攻击更强。SHA 算法由国家安全局（NSA）设计。MD5 使用 128 位哈希大小；SHA 使用 160 位。其他 SHA 算法在名称中包含哈希大小。SHA512 是这些算法中最强的，哈希大小为 512 位；它也是最慢的。RIPEMD160 使用 160 位哈希大小；它旨在替代 128 位 MD4 和 MD5。RIPEMD 是从名为 RIPE（Race Integrity Primitives Evaluation）的欧盟项目开发的。

对称

```
DES DESCryptoServiceProvider TripleDESTripleDESCryptoServiceProvider Aes AesCryptoServiceProvider AesManaged RC2 RC2CryptoServiceProvider Rijndael RijndaelManaged
```

对称密钥算法使用相同的密钥对数据进行加密和解密。数据加密

## 非对称

- DSA
- DSACryptoServiceProvider
- ECDsa
- ECDsaCng
- ECDiffieHellman
- ECDiffieHellmanCng
- RSA
- RSACryptoServiceProvider
- RSACng

标准（DES 现在被认为不安全，因为它仅使用 56 位作为密钥大小并且可以在不到 24 小时内被破解。Triple-DES 是 DES 的继任者，密钥长度为 168 位，但其提供的有效安全性仅为 112 位。高级加密标准（AES）具有 128、192 或 256 位的密钥大小。Rijndael 与 AES 非常相似，但提供更多密钥大小选项。AES 是美国政府采用的加密标准。

非对称算法使用不同的密钥进行加密和解密。Rivest、Shamir、Adleman（RSA）算法是第一个用于签名和加密的算法。该算法

在电子商务协议中广泛使用。RSACng 是 .NET 4.6 和 .NET 5 Core 的新类，基于 Cryptography Next Generation（CNG）实现。数字签名算法（DSA）是美国联邦政府的数字签名标准。椭圆曲线 DSA（ECDSA）和 EC Diffie-Hellman 使用基于椭圆曲线组的算法。这些算法更安全，密钥大小更短。例如，DSA 的 1024 位密钥大小与 ECDSA 的 160 位安全性相似。因此，ECDSA 快得多。EC Diffie-Hellman 是一种用于在

|  |  | 公共通道上安全地交换私钥的算法。 |

以下部分包括一些示例，演示如何以编程方式使用这些算法。

## 创建和验证签名

第一个示例演示使用前表中所述的 ECDSA 算法进行签名。Alice 创建一个用她的私钥加密的签名，可以使用她的公钥访问。这样可以保证签名来自 Alice。

示例应用程序 SigningDemo 使用以下依赖项和命名空间：

## 依赖项

- NETStandard.Library
- System.Security.Cryptography.Algorithms
- System.Security.Cryptography.Cng

## 命名空间

- System
- System.Security.Cryptography
- System.Text
- static System.Console

首先，查看 Main 方法中的主要步骤：Alice 的密钥被创建，并且字符串 "Alice" 被签名，然后通过使用公钥验证签名确实来自 Alice。被签名的消息通过使用 Encoding 类转换为字节数组。为了将加密的签名写入控制台，包含签名的字节数组通过 Convert.ToBase64String 方法转换为字符串（代码文件 SigningDemo/Program.cs）：

```
private CngKey _aliceKeySignature;
private byte[] _alicePubKeyBlob;
static void Main()
{
    var p = new Program();
    p.Run();
}
public void Run()
{
    InitAliceKeys();
    byte[] aliceData = Encoding.UTF8.GetBytes("Alice");
    byte[] aliceSignature = CreateSignature(aliceData, aliceKeySignature);
    WriteLine($"Alice created signature: {Convert.ToBase64String(aliceSignature)}");
    if (VerifySignature(aliceData, aliceSignature, alicePubKeyBlob))
```

```
```csharp
WriteLine("Alice signature verified successfully");
}
}
```
```

> **警告** *永远不要使用 `Encoding` 类将加密数据转换为字符串。`Encoding` 类会验证并转换 Unicode 中不允许的无效值；因此，将字符串转换回字节数组可能会产生不同的结果。*

`InitAliceKeys` 是为 Alice 创建新密钥对的方法。此密钥对存储在静态字段中，因此可以从其他方法访问。`CngKey` 的 `Create` 方法将算法作为参数，以为算法定义密钥对。通过 `Export` 方法，密钥对的公钥被导出。此公钥可以交给 Bob 以验证签名。Alice 保留私钥。除了使用 `CngKey` 类创建密钥对外，您还可以打开存储在密钥存储中的现有密钥。通常 Alice 会在她的私有存储中拥有包含密钥对的证书，并且可以通过 `CngKey.Open` 访问存储：

```
```csharp
private void InitAliceKeys()
{
    _aliceKeySignature = CngKey.Create(CngAlgorithm.ECDsaP521);
    _alicePubKeyBlob = aliceKeySignature.Export(CngKeyBlobFormat.GenericPublicBlob);
}
```
```

有了密钥对，Alice 可以使用 `ECDsaCng` 类创建签名。此类的构造函数接收来自 Alice 的 `CngKey`——包含公钥和私钥。私钥用于通过 `SignData` 方法签名数据。`SignData` 方法在 .NET Core 中略有不同。.NET Core 需要算法：

```
```csharp
public byte[] CreateSignature(byte[] data, CngKey key)
{
    byte[] signature;
    using (var signingAlg = new ECDsaCng(key))
    {
#if NET46
        signature = signingAlg.SignData(data);
        signingAlg.Clear();
#else
        signature = signingAlg.SignData(data,
            HashAlgorithmName.SHA512);
#endif
    }
    return signature;
}
```
```

为了验证签名确实来自 Alice，Bob 通过使用来自 Alice 的公钥检查签名。包含公钥 blob 的字节数组可以通过静态 `Import` 方法导入到 `CngKey` 对象。`ECDsaCng` 类随后用于通过调用 `VerifyData` 验证签名：

