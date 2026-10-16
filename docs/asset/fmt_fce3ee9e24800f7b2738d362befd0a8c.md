
```csharp
public async Task<byte[]> AliceSendsDataAsync(string message)
{
    WriteLine($"Alice sends message: {message}");
    byte[] rawData = Encoding.UTF8.GetBytes(message);
    byte[] encryptedData = null;

    using (var aliceAlgorithm = new ECDiffieHellmanCng(aliceKey))
    using (CngKey bobPubKey = CngKey.Import(bobPubKeyBlob,
            CngKeyBlobFormat.EccPublicBlob))
    {
        byte[] symmKey =
        aliceAlgorithm.DeriveKeyMaterial(bobPubKey);
        WriteLine("Alice creates this symmetric key with" +
            $"Bobs public key information:
{Convert.ToBase64String(symmKey)}");

        using (var aes = new AesCryptoServiceProvider())
        {
            aes.Key = symmKey;
            aes.GenerateIV();
            using (ICryptoTransform encryptor = aes.CreateEncryptor())
            using (var ms = new MemoryStream())
            {
                // create CryptoStream and encrypt data to send
                using (var cs = new CryptoStream(ms, encryptor,
                        CryptoStreamMode.Write))
                {
                    // write initialization vector not encrypted
                    await ms.WriteAsync(aes.IV, 0, aes.IV.Length);
                    cs.Write(rawData, 0, rawData.Length);
                }
                encryptedData = ms.ToArray();
            }
            aes.Clear();
        }
    }
    WriteLine("Alice: message is encrypted:"+
        "{Convert.ToBase64String(encryptedData)}");

    WriteLine();
    return encryptedData;
}
```

Bob 在 `BobReceivesDataAsync` 方法的参数中接收加密数据。首先，必须读取未加密的初始化向量。`AesCryptoServiceProvider` 类的 `BlockSize` 属性返回块的位数。字节数可以通过除以 8 计算出来，最快的方法是进行 3 位的位移（移位 1 位为除以 2，2 位为除以 4，3 位为除以 8）。使用 `for` 循环，将包含未加密 IV 的原始字节的前几个字节写入数组 `iv`。接下来，使用 Bob 的密钥对实例化 `ECDiffieHellmanCng` 对象。使用 Alice 的公钥，方法 `DeriveKeyMaterial` 返回对称密钥。

比较 Alice 和 Bob 创建的对称密钥可知，创建了相同的密钥值。使用此对称密钥和初始化向量，可以使用

### `AesCryptoServiceProvider` 类解密 Alice 的消息：

```csharp
public async Task BobReceivesDataAsync(byte[] encryptedData)
{
    WriteLine("Bob receives encrypted data");
    byte[] rawData = null;
    var aes = new AesCryptoServiceProvider();
    int nBytes = aes.BlockSize * 3;
    byte[] iv = new byte[nBytes];
    for (int i = 0; i < iv.Length; i++)
    {
        iv[i] = encryptedData[i];
    }
    using (var bobAlgorithm = new ECDiffieHellmanCng(bobKey))
    using (CngKey alicePubKey = CngKey.Import(alicePubKeyBlob,
        CngKeyBlobFormat.EccPublicBlob))
    {
        byte[] symmKey =
        bobAlgorithm.DeriveKeyMaterial(alicePubKey);
        WriteLine("Bob creates this symmetric key with" +
        $"Alice's public key information:
{Convert.ToBase64String(symmKey)}");
        aes.Key = symmKey;
        aes.IV = iv;
        using (ICryptoTransform decryptor = aes.CreateDecryptor())
        using (MemoryStream ms = new MemoryStream())
        {
            using (var cs = new CryptoStream(ms, decryptor,
                CryptoStreamMode.Write))
            {
                await cs.WriteAsync(encryptedData, nBytes,
                    encryptedData.Length - nBytes);
            }
            rawData = ms.ToArray();
            WriteLine("Bob decrypts message to:" +
            $" {Encoding.UTF8.GetString(rawData)}");
        }
    }
    aes.Clear();
}
```

运行应用程序返回的输出类似于以下内容。Alice 的消息被加密，然后 Bob 使用安全交换的对称密钥解密。

```
Alice sends message: this is a secret message for Bob
Alice creates this symmetric key with Bobs public key information:
q4D182m7lyev9Nlp6f0av2Jvc0+LmHF5zEjXw101I3Y=
Alice: message is encrypted:
WpOxvUoWH5XY31wC8aXcDWeDUWa6zaSObfGcQpKixzLTJ9exb
tkF5Hp2WPSZWLY9n13toBg7hgjPbrVzN2A==
Bob receives encrypted data
Bob creates this symmetric key with Alices public key information:
q4D182m7lyev9Nlp6f0av2Jvc0+LmHF5zEjXw101I3Y=
```

Bob 将消息解密为：这是给 Bob 的秘密消息

### 使用 RSA 进行签名和哈希

.NET 4.6 和 .NET Core 1.0 新增的一个密码算法类是 `RSACng`。RSA（该名称来自算法设计者 Ron Rivest、Adi Shamir 和 Leonard Adleman）是一种被广泛使用的非对称算法。虽然 .NET 中已经通过 `RSA` 和 `RSACryptoServiceProvider` 类提供了 RSA 算法，但 `RSACng` 是一个基于 CNG API 的类，在使用方式上类似于前面展示的 `ECDsaCng` 类。

在本节所示的示例应用程序中，Alice 创建一份文档，对其进行哈希以确保文档不被更改，并用签名对文档进行签名，以保证文档确实由 Alice 生成。Bob 收到文档后，会验证 Alice 的保证，以确保文档没有被篡改。

RSA 示例代码使用了以下依赖项和命名空间：

#### 依赖项

- `NETStandard.Library`

- `System.Security.Cryptography.Algorithms`

- `System.Security.Cryptography.Cng`

#### 命名空间

- `Microsoft.Extensions.DependencyInjection`

- `System`

- `System.IO`

- `System.Linq`

- `static System.Console`

```
class Program
{
  private CngKey _aliceKey;
  private byte[] _alicePubKeyBlob;

  static void Main()
  {
    var p = new Program();
    p.Run();
  }

  public void Run()
  {
    byte[] document;
    byte[] hash;
    byte[] signature;
    AliceTasks(out document, out hash, out signature);
    BobTasks(document, hash, signature);
  }
  //...
}
```

`AliceTasks` 方法首先创建 Alice 所需的密钥，将消息转换为字节数组，对字节数组进行哈希，然后添加签名：

```
public void AliceTasks(out byte[] data, out byte[] hash, out byte[] signature)
{
    InitAliceKeys();

    data = Encoding.UTF8.GetBytes("Best greetings from Alice");
    hash = HashDocument(data);
    signature = AddSignatureToHash(hash, _aliceKey);
}
```

与之前类似，Alice 所需的密钥使用 `CngKey` 类创建。由于现在使用的是 RSA 算法，因此将枚举值 `CngAlgorithm.Rsa` 传递给 `Create` 方法来创建公钥和私钥。只有公钥会提供给 Bob，因此通过 `Export` 方法提取公钥：

```
private void InitAliceKeys()
{
    _aliceKey = CngKey.Create(CngAlgorithm.Rsa);
    _alicePubKeyBlob = _aliceKey.Export(CngKeyBlobFormat.GenericPublicBlob);
}
```

`HashDocument` 方法从 Alice 的任务中调用，用于为文档创建哈希码。哈希码使用哈希算法类之一（`SHA384`）创建。无论文档有多长，哈希码的长度总是相同的。对同一文档再次创建哈希码，结果相同。Bob 需要对文档使用相同的算法。如果得到相同的哈希码，则说明文档未被更改。

```
private byte[] HashDocument(byte[] data)
{
    using (var hashAlg = SHA384.Create())
    {
        return hashAlg.ComputeHash(data);
    }
}
```

添加签名可以保证文档来自 Alice。这里使用 `RSACng` 类对哈希进行签名。Alice 的 `CngKey`（包括公钥和私钥）被传递给 `RSACng` 类的构造函数；签名通过调用 `SignHash` 方法创建。对哈希签名时，`SignHash` 方法需要知道哈希使用的算法；`HashAlgorithmName.SHA384` 就是用于创建该哈希的算法。此外，还需要 RSA 填充。`RSASignaturePadding` 枚举中可选的选项有 `Pss` 和 `Pkcs1`：

```
private byte[] AddSignatureToHash(byte[] hash, CngKey key)
{
    using (var signingAlg = new RSACng(key))
    {
        byte[] signed = signingAlg.SignHash(hash,
            HashAlgorithmName.SHA384, RSASignaturePadding.Pss);
        return signed;
    }
}
```

在 Alice 完成哈希和签名之后，Bob 的任务可以在 `BobTasks` 方法中开始。Bob 收到文档数据、哈希码和签名，并使用 Alice 的公钥。首先，使用 `CngKey.Import` 导入 Alice 的公钥，并将其赋值给 `aliceKey` 变量。接下来，Bob 使用辅助方法 `IsSignatureValid` 和 `IsDocumentUnchanged` 来验证签名是否有效以及文档是否未被更改。只有两个条件都满足时，文档才会被写入控制台：

```
public void BobTasks(byte[] data, byte[] hash, byte[] signature)
{
    CngKey aliceKey = CngKey.Import(_alicePubKeyBlob,
        CngKeyBlobFormat.GenericPublicBlob);
    if (!IsSignatureValid(hash, signature, aliceKey))
    {
        WriteLine("signature not valid");
        return;
    }
    if (!IsDocumentUnchanged(hash, data))
    {
        WriteLine("document was changed");
        return;
    }
    WriteLine("signature valid, document unchanged");
    WriteLine($"document from Alice: {Encoding.UTF8.GetString(data)}");
}
```

为了验证签名是否有效，使用 Alice 的公钥创建 `RSACng` 类的实例。使用该类时，通过 `VerifyHash` 方法传入哈希、签名以及之前使用的算法信息。这样 Bob 就能确认信息确实来自 Alice：

```
private bool IsSignatureValid(byte[] hash, byte[] signature, CngKey key)
{
    using (var signingAlg = new RSACng(key))
    {
        return signingAlg.VerifyHash(hash, signature,
            HashAlgorithmName.SHA384,
            RSASignaturePadding.Pss);
    }
}
```

为了验证文档数据未被更改，Bob 再次对文档进行哈希，并使用 LINQ 扩展方法 `SequenceEqual` 来验证哈希码是否与之前发送的相同。如果哈希相同，则可以认为文档没有被更改：

```
private bool IsDocumentUnchanged(byte[] hash, byte[] data)
{
    byte[] newHash = HashDocument(data);
    return newHash.SequenceEqual(hash);
}
```

当你运行该应用程序时，会看到类似于下面所示的输出。当你调试该应用程序时，可以在文档经过 Alice 的哈希之后修改文档数据，然后观察 Bob 是否会拒绝被修改的文档。要修改文档数据，你可以轻松地在调试器的“监视”窗口中更改该值。

```
signature valid, document unchanged
document from Alice: Best greetings from Alice
```

### 实现数据保护

.NET 中另一个与加密相关的特性是新的 .NET Core 库对 `数据保护` 的支持。命名空间 `System.Security.DataProtection` 包含一个 `DpapiDataProtector` 类，它封装了本机 Windows 数据保护 API（DPAPI）。这些类无法提供 Web 服务器所需的灵活性和功能，因此 ASP.NET 团队创建了 `Microsoft.AspNet.DataProtection` 命名空间下的类。
