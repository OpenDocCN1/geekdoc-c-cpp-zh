
数据不足八个字节。当然，我们可以用 0 填充剩余字节，得到最后一个八字节块并加密。但在解密这些块后，结果末尾会附加若干 0 字节，因此会与原始输入文件略有不同。为避免这个问题，我们需要一种*填充方案*。一种常用的填充方案是 RSA Security, Inc. 在《公钥密码学标准》（PKCS）#5 中描述的方案（https://tools.ietf.org/html/rfc2898）。

在该方案中，最后一个块不是用零作为填充值来填充，而是用等于填充字节数的填充值来填充。换言之，如果 L 是最后一个（不完整的）块，则按如下方式填充：

```
L 01                         if length(L) = 7
L 02 02                      if length(L) = 6
L 03 03 03                   if length(L) = 5
. . . .
L 07 07 07 07 07 07 07      if length(L) = 1
```

最后，如果输入长度实际上能被 8 整除，则一个块

```
08 08 08 08 08 08 08 08
```

会被追加到输入中并加密。解密后，明文的最后一个字节是要丢弃的填充字符数。

## 9.5.2 密钥生成

要加密，需要生成密钥。每种密码的密钥格式不同，并且需要确保密钥生成是随机的。请按以下步骤操作：

- 1. 为你的算法获取一个 `KeyGenerator`。
- 2. 用随机性来源初始化生成器。如果密码的块长度可变，还要指定所需的块长度。
- 3. 调用 `generateKey` 方法。

例如，下面展示如何生成 AES 密钥：

```java
KeyGenerator keygen = KeyGenerator.getInstance("AES");
SecureRandom random = new SecureRandom(); // see below
keygen.init(random);
Key key = keygen.generateKey();
```

或者，你可以从一组固定的原始数据（也许派生自密码或击键时序）生成密钥。像这样构造一个 `SecretKeySpec`（它实现了 `SecretKey` 接口）：

```java
byte[] keyData = ...; // 16 bytes for AES
SecretKey key = new SecretKeySpec(keyData, "AES");
```

生成密钥时，请确保使用*真正随机*的数字。例如，`Random` 类中的常规随机数生成器以当前日期和时间为种子，随机性不够。假设计算机时钟精确到 1/10 秒，那么每天最多有 864,000 个种子。如果攻击者知道密钥签发的日期（这通常可以从消息日期或证书到期日期推断出来），那么生成该日期所有可能的种子就是一件容易的事。

`SecureRandom` 类生成的随机数远比 `Random` 类生成的随机数安全。你仍然需要提供一个种子，以便在随机位置开始数字序列。最好的方法是从硬件设备（例如白噪声生成器）获取随机输入。另一个合理的随机输入来源是让用户在键盘上漫无目的地敲击，每次击键只向随机种子贡献一两个比特。一旦你在一个字节数组中收集了这样的随机比特，就把它传给 `setSeed` 方法：

```java
SecureRandom serand = new SecureRandom();
byte[] b = new byte[20];
// fill with truly random bits
serand.setSeed(b);
```

如果你不播种随机数生成器，它会通过启动线程、让线程休眠并测量线程被唤醒的精确时间来计算自己的 20 字节种子。

> **注意：** 该算法*并非*已知是安全的。过去，依赖计算机某些组件时序（例如硬盘访问时间）的算法已被证明并非完全随机。

本节末尾的示例程序将 AES 密码投入使用（见代码清单 9.18）。代码清单 9.19 中的 crypt 工具方法将在其他示例中复用。要使用该程序，首先需要生成一个秘密密钥。运行

```bash
java aes.AESTest -genkey secret.key
```

秘密密钥保存在文件 `secret.key` 中。

现在可以用以下命令加密

```bash
java aes.AESTest -encrypt plaintextFile encryptedFile secret.key
```

用以下命令解密

```bash
java aes.AESTest -decrypt encryptedFile decryptedFile secret.key
```

该程序简单明了。-genkey 选项生成一个新的秘密密钥，并将其序列化到给定文件中。该操作耗时较长，因为安全随机生成器的初始化很耗时。-encrypt 和 -decrypt 选项都会调用同一个 crypt 方法，该方法调用密码的 update 和 doFinal 方法。注意，只要输入块具有完整长度，就会调用 update 方法；而 doFinal 方法要么用部分输入块调用（随后会填充该块），要么不带额外数据调用（以生成一个填充块）。

### 代码清单 9.18 `aes/AESTest.java`

```java
package aes;

import java.io.*;
import java.security.*;
import javax.crypto.*;

/**
 * This program tests the AES cipher. Usage:<br>
 * java aes.AESTest -genkey keyfile<br>
 * java aes.AESTest -encrypt plaintext encrypted keyfile<br>
 * java aes.AESTest -decrypt encrypted decrypted keyfile<br>
 * @author Cay Horstmann
 * @version 1.01 2012-06-10
 */
public class AESTest
{
   public static void main(String[] args)
      throws IOException, GeneralSecurityException, ClassNotFoundException
   {
      if (args[0].equals("-genkey"))
      {
         KeyGenerator keygen = KeyGenerator.getInstance("AES");
         SecureRandom random = new SecureRandom();
         keygen.init(random);
         SecretKey key = keygen.generateKey();
         try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(args[1])))
         {
            out.writeObject(key);
         }
      }
      else
      {
         int mode;
         if (args[0].equals("-encrypt")) mode = Cipher.ENCRYPT_MODE;
         else mode = Cipher.DECRYPT_MODE;

         try (ObjectInputStream keyIn = new ObjectInputStream(new FileInputStream(args[3]));
              InputStream in = new FileInputStream(args[1]);
              OutputStream out = new FileOutputStream(args[2]))
         {
            Key key = (Key) keyIn.readObject();
            Cipher cipher = Cipher.getInstance("AES");
            cipher.init(mode, key);
            Util.crypt(in, out, cipher);
         }
      }
   }
}
```

### 代码清单 9.19 `aes/Util.java`

```java
package aes;

import java.io.*;
import java.security.*;
import javax.crypto.*;

public class Util
{
    /**
     * Uses a cipher to transform the bytes in an input stream and sends the transformed bytes to
     * an output stream.
     * @param in the input stream
     * @param out the output stream
     * @param cipher the cipher that transforms the bytes
     */
    public static void crypt(InputStream in, OutputStream out, Cipher cipher)
        throws IOException, GeneralSecurityException
    {
        int blockSize = cipher.getBlockSize();
        int outputSize = cipher.getOutputSize(blockSize);
        byte[] inBytes = new byte[blockSize];
        byte[] outBytes = new byte[outputSize];

        int inLength = 0;
        boolean more = true;
        while (more)
        {
```

| `javax.crypto.KeyGenerator` | `1.4` |
|---|---|
| • `static KeyGenerator getInstance(String algorithmName)`<br>返回一个实现指定算法的 KeyGenerator 对象。如果未提供该算法，则抛出 `NoSuchAlgorithmException`。<br><br>• `void init(SecureRandom random)`<br>• `void init(int keySize, SecureRandom random)`<br>初始化密钥生成器。<br><br>• `SecretKey generateKey()`<br>生成一个新密钥。 | |

| `javax.crypto.spec.SecretKeySpec` | `1.4` |
|---|---|
| • `SecretKeySpec(byte[] key, String algorithmName)`<br>构造一个密钥规范。 | |

## 9.5.3 密码流

JCE 库提供了一组方便的流类，可自动加密或解密流数据。例如，下面展示如何将数据加密到文件：

```java
Cipher cipher = ... ;
cipher.init(Cipher.ENCRYPT_MODE, key);
CipherOutputStream out = new CipherOutputStream(new FileOutputStream(outputFileName), cipher);
byte[] bytes = new byte[BLOCKSIZE];
int inLength = getData(bytes); // get data from data source
while (inLength != -1)
{
    out.write(bytes, 0, inLength);
    inLength = getData(bytes); // get more data from data source
}
out.flush();
```

类似地，你可以使用 CipherInputStream 从文件读取并解密数据：

```java
Cipher cipher = ... ;
cipher.init(Cipher.DECRYPT_MODE, key);
CipherInputStream in = new CipherInputStream(new FileInputStream(inputFileName), cipher);
byte[] bytes = new byte[BLOCKSIZE];
int inLength = in.read(bytes);
while (inLength != -1)
{
```
