
## 第一部分：C# 基础

为了了解对称加密的工作原理，您将在下面的 SymmetricEncryption() 函数中使用 RijndaelManaged 类。需要三个参数——要加密的字符串、私钥和初始化向量（IV）。IV 是加密过程中使用的随机数，用于确保加密后没有两个字符串会产生相同的密文（加密后的文本）。在解密密文时，您稍后需要使用相同的 IV。

为了执行实际加密，您使用 MemoryStream 对象、对流执行的加密转换以及流的模式（加密时为 Write，解密时为 Read）初始化 CryptoStream 类的一个实例：

```csharp
static string SymmetricEncryption(string str, byte[] key, byte[] IV)
{
    MemoryStream ms = new MemoryStream();
    try
    {
        //---creates a new instance of the RijndaelManaged class---
        RijndaelManaged RMCrypto = new RijndaelManaged();

        //---creates a new instance of the CryptoStream class---
        CryptoStream cryptStream =
            new CryptoStream(
                ms, RMCrypto.CreateEncryptor(key, IV),
                CryptoStreamMode.Write);

        StreamWriter sWriter = new StreamWriter(cryptStream);

        //---encrypting the string---
        sWriter.Write(str);
        sWriter.Close();
        cryptStream.Close();

        //---return the encrypted data as a string---
        return System.Convert.ToBase64String(ms.ToArray());
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.ToString());
        return (String.Empty);
    }
}
```

加密后的字符串以 Base64 编码的字符串形式返回。您可以使用以下代码检查 RijndaelManaged 类允许的密钥大小：

```csharp
KeySizes[] ks;
RijndaelManaged RMCrypto = new RijndaelManaged();
ks = RMCrypto.LegalKeySizes;

//---print out the various key sizes---
Console.WriteLine(ks[0].MaxSize);   // 256
Console.WriteLine(ks[0].MinSize);   // 128
Console.WriteLine(ks[0].SkipSize);  // 64
```

有效的密钥大小为：16 字节（128 位）、24 字节（128 位 + 64 位）和 32 字节（256 位）。

您可以让系统自动生成随机密钥和 IV（您需要在当前示例中提供）：

```csharp
//---generate key---
RMCrypto.GenerateKey();
byte[] key = RMCrypto.Key;
Console.WriteLine("Key : " + System.Convert.ToBase64String(key));

//---generate IV---
RMCrypto.GenerateIV();
byte[] IV = RMCrypto.IV;
Console.WriteLine("IV : " + System.Convert.ToBase64String(IV));
```

如果使用时 IV 为 null，则会自动调用 GenerateIV() 方法。IV 的有效大小为 16 字节。

要解密使用 RijndaelManaged 类加密的字符串，您可以使用以下 SymmetricDecryption() 函数：

```csharp
static string SymmetricDecryption(string str, byte[] key, byte[] IV)
{
    try
    {
        //---converts the encrypted string into a byte array---
        byte[] b = System.Convert.FromBase64String(str);

        //---converts the byte array into a memory stream for decryption---
        MemoryStream ms = new MemoryStream(b);

        //---creates a new instance of the RijndaelManaged class---
        RijndaelManaged RMCrypto = new RijndaelManaged();

        //---creates a new instance of the CryptoStream class---
        CryptoStream cryptStream =
            new CryptoStream(
                ms,
                RMCrypto.CreateDecryptor(key, IV),
                CryptoStreamMode.Read);

        //---decrypting the stream---
        StreamReader sReader = new StreamReader(cryptStream);

        //---converts the decrypted stream into a string---
        String s = sReader.ReadToEnd();
        sReader.Close();
        return s;
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.ToString());
        return String.Empty;
    }
}
```

以下代码片段展示了如何使用 SymmetricEncryption() 和 SymmetricDecryption() 函数来加密和解密字符串：

```csharp
RijndaelManaged RMCrypto = new RijndaelManaged();

//---generate key---
RMCrypto.GenerateKey();
byte[] key = RMCrypto.Key;
Console.WriteLine("Key: " + System.Convert.ToBase64String(key));

//---generate IV---
RMCrypto.GenerateIV();
byte[] IV = RMCrypto.IV;
Console.WriteLine("IV: " + System.Convert.ToBase64String(IV));

//---encrypt the string---
string cipherText =
    SymmetricEncryption("This is a test string.", key, IV);
Console.WriteLine("Ciphertext: " + cipherText);

//---decrypt the string---
Console.WriteLine("Original string: " +
    SymmetricDecryption(cipherText, key, IV));
```

图 11-7 显示了输出。

![](img/a977a875c7c627b45d939729705a252e_373_0.png)

图 11-7

### 非对称加密

私钥加密要求加密过程中使用的密钥保持秘密。一种更有效的向预期收件人传输秘密消息的方式是使用非对称加密（也称为公钥加密），它涉及一对密钥。这对密钥由私钥和公钥组成，在数学上相关，使得使用公钥加密的消息只能用相应的私钥解密。反之亦然；使用私钥加密的消息只能用公钥解密。让我们看一下每个场景的示例。

在您向朋友 Susan 发送消息之前，Susan 需要生成包含私钥和公钥的密钥对。Susan 然后自由地将公钥分发给您（以及她所有的其他朋友），但将私钥保留给自己。当您想向 Susan 发送消息时，您使用她的公钥加密消息。收到加密消息后，Susan 用她的私钥对其进行解密。Susan 是唯一可以解密消息的人，因为密钥对的工作方式是只有使用公钥加密的消息才能用私钥解密。而且无需交换密钥，从而消除了密钥保密性受损的风险。

```csharp
//---Decrypts the string---
byte[] DecryptedStr =
    RSA.Decrypt(System.Convert.FromBase64String(str), false);

//---Converts the decrypted byte array to string---
return ASCIIEncoding.ASCII.GetString(DecryptedStr);
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
    return String.Empty;
}
```

以下代码片段展示了如何使用 AsymmetricEncryption() 和 AsymmetricDecryption() 函数来加密和解密字符串：

```csharp
string publicKey, privateKey;
RSACryptoServiceProvider RSA =
    new RSACryptoServiceProvider();

//---get public key---
publicKey = RSA.ToXmlString(false);
Console.WriteLine("Public key: " + publicKey);
Console.WriteLine();

//---get private and public key---
privateKey = RSA.ToXmlString(true);
Console.WriteLine("Private key: " + privateKey);
Console.WriteLine();

//---encrypt the string---
string cipherText =
    AsymmetricEncryption("C# 2008 Programmer's Reference", publicKey);
Console.WriteLine("Ciphertext: " + cipherText);
Console.WriteLine();

//---decrypt the string---
Console.WriteLine("Original string: " +
    AsymmetricDecryption(cipherText, privateKey));
Console.WriteLine();
```

您可以使用 RSACryptoServiceProvider 类中的 ToXmlString() 方法获取 RSA 算法生成的公钥和私钥。此方法接受一个 bool 变量，如果提供的值为 false，则返回公钥。如果提供的值为 true，则返回私钥和公钥。

图 11-8 显示了输出。

![](img/a977a875c7c627b45d939729705a252e_376_0.png)

图 11-8

### 流对象的压缩

System.IO.Compression 命名空间包含提供流基本压缩和解压缩服务的类。此命名空间包含两个用于数据压缩的类：DeflateStream 和 GZipStream。两者都支持无损压缩和解压缩，并设计用于处理流。

压缩对于减小数据大小很有用。例如，如果您有大量数据要存储在 SQL 数据库中，您可以在将其保存到表中之前压缩数据，从而节省磁盘空间。此外，由于您现在将较小的數據块保存到数据库中，执行磁盘 I/O 所花费的时间显著减少。压缩的缺点是它会占用机器的额外处理能力（并需要额外的处理时间），在决定在应用程序中使用压缩之前，您需要考虑这额外的時間。

在需要通过网络传输数据的情况下，压缩非常有用，尤其是通过通用分组无线服务 (GPRS) 等缓慢且昂贵的网络连接时。在这种情况下，使用压缩可以大幅减少数据大小并降低整体通信成本。Web Services 是另一个可以使用压缩获得巨大优势的领域，因为 XML 数据可以高度压缩。

但一旦您决定性能成本是值得的，您就需要帮助来解读这两个压缩类的使用方法，这正是本节要介绍的内容。

### 压缩

压缩类从字节数组读取数据（待压缩），对其进行压缩，并将结果存储在 Stream 对象中。对于解压缩，存储在 Stream 对象中的压缩数据将被解压缩，然后存储到另一个 Stream 对象中。

让我们看看如何执行压缩。首先，定义 Compress() 函数，它接受两个参数：algo 和 data。第一个参数指定要使用的算法（GZip 或 Deflate），
