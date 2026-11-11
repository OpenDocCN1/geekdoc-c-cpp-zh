

如果没有为随机数生成器设置种子，它就会通过启动线程、让线程休眠，并测量线程被唤醒的精确时间来计算自己的 20 字节种子。

> **注意：** 该算法*不*被认为是安全的。过去，依赖计算机某些组件（例如硬盘访问时间）计时的算法已被证明并非完全随机。

本节末尾的示例程序将使用 AES 密码（见代码清单 10.17）。代码清单 10.18 中的 crypt 工具方法将在其他示例中复用。要使用该程序，首先需要生成一个秘密密钥。运行

```java
java aes.AESTest -genkey secret.key
```

秘密密钥保存在文件 secret.key 中。

现在可以使用以下命令进行加密：

```java
java aes.AESTest -encrypt plaintextFile encryptedFile secret.key
```

使用以下命令解密：

```java
java aes.AESTest -decrypt encryptedFile decryptedFile secret.key
```

该程序很直接。-genkey 选项会生成一个新的秘密密钥，并将其序列化到给定文件中。该操作耗时较长，因为安全随机数生成器的初始化很耗时。-encrypt 和 -decrypt 选项都会调用同一个 crypt 方法，而该方法会调用密码的 update 和 doFinal 方法。请注意，只要输入块具有完整长度，就会调用 update 方法；而 doFinal 方法要么在输入块不完整时被调用（随后会进行填充），要么在没有额外数据时被调用（以生成一个填充块）。

## 代码清单 10.17 `aes/AESTest.java`

```java
1  package aes;
2
3  import java.io.*;
4  import java.security.*;
5  import javax.crypto.*;
6
```

## 代码清单 10.18 `aes/Util.java`

```java
package aes;

import java.io.*;
import java.security.*;
import java.security.spec.*;

public class Util
{
    /**
     * Uses a cipher to transform the bytes in an input stream and sends the transformed bytes
     * to an output stream.
     * @param in the input stream
     * @param out the output stream
     * @param cipher the cipher that transforms the bytes
     */
    public static void crypt(InputStream in, OutputStream out, Cipher cipher)
        throws IOException, GeneralSecurityException
    {
        int blockSize = cipher.getBlockSize();
        int outputSize = cipher.getOutputSize(blockSize);
        var inBytes = new byte[blockSize];
        var outBytes = new byte[outputSize];

        int inLength = 0;
        var done = false;
        while (!done)
        {
            inLength = in.read(inBytes);
            if (inLength == blockSize)
            {
                int outLength = cipher.update(inBytes, 0, blockSize, outBytes);
                out.write(outBytes, 0, outLength);
            }
            else done = true;
        }
        if (inLength > 0) outBytes = cipher.doFinal(inBytes, 0, inLength);
        else outBytes = cipher.doFinal();
        out.write(outBytes);
    }
}
```

| javax.crypto.KeyGenerator 1.4（续） |
| --- |
| • `SecretKey generateKey()`<br>生成一个新密钥。 |

| javax.crypto.spec.SecretKeySpec 1.4 |
| --- |
| • `SecretKeySpec(byte[] key, String algorithmName)`<br>构造一个密钥规范。 |

### 10.5.3 密码流

JCE 库提供了一组方便的流类，可以自动加密或解密流数据。例如，下面是将数据加密到文件的方法：

```java
Cipher cipher = . . .;
cipher.init(Cipher.ENCRYPT_MODE, key);
var out = new CipherOutputStream(new FileOutputStream(outputFileName), cipher);
var bytes = new byte[BLOCK_SIZE];
int inLength = getData(bytes); // get data from data source
while (inLength != -1)
{
    out.write(bytes, 0, inLength);
    inLength = getData(bytes); // get more data from data source
}
out.flush();
```

类似地，你可以使用 CipherInputStream 从文件中读取并解密数据：

```java
Cipher cipher = . . .;
cipher.init(Cipher.DECRYPT_MODE, key);
var in = new CipherInputStream(new FileInputStream(inputFileName), cipher);
var bytes = new byte[BLOCK_SIZE];
int inLength = in.read(bytes);
while (inLength != -1)
{
    putData(bytes, inLength); // put data to destination
    inLength = in.read(bytes);
}
```

密码流类会透明地处理对 update 和 doFinal 的调用，这显然很方便。

| `javax.crypto.CipherInputStream` | 1.4 |
| --- |
| • `CipherInputStream(InputStream in, Cipher cipher)`<br>构造一个输入流，该流从 *in* 读取数据，并使用给定密码对其进行解密或加密。<br><br>• `int read()`<br>• `int read(byte[] b, int off, int len)`<br>从输入流读取数据，数据会被自动解密或加密。 | |

| `javax.crypto.CipherOutputStream` | 1.4 |
| --- |
| • `CipherOutputStream(OutputStream out, Cipher cipher)`<br>构造一个输出流，该流将数据写入 *out*，并使用给定密码对其进行加密或解密。<br><br>• `void write(int ch)`<br>• `void write(byte[] b, int off, int len)`<br>将数据写入输出流，数据会被自动加密或解密。<br><br>• `void flush()`<br>刷新密码缓冲区，并在必要时执行填充。 | |

### 10.5.4 公钥密码

上一节中见到的 AES 密码是一种*对称*密码。加密和解密使用同一个密钥。对称密码的致命弱点在于密钥分发。如果 Alice 向 Bob 发送加密消息，Bob 就需要 Alice 使用的同一个密钥。如果 Alice 更改了密钥，她需要把消息以及新密钥（通过安全通道）都发送给 Bob。但也许她根本没有通往 Bob 的安全通道——而这正是她一开始要加密发给他的消息的原因。

公钥密码学解决了这个问题。在公钥密码中，Bob 拥有一对密钥，由一个公钥和一个匹配的私钥组成。Bob 可以把公钥发布到任何地方，但必须严密保管私钥。Alice 只需使用公钥来加密她发给 Bob 的消息。

实际上，事情并没有那么简单。所有已知的公钥算法都比 DES 或 AES 等对称密钥算法*慢得多*。使用公钥算法加密大量信息并不实际。不过，通过将公钥密码与快速对称密码结合，可以轻松克服这个问题，如下所示：

1. Alice 生成一个随机对称加密密钥。她用该密钥加密自己的明文。
2. Alice 用 Bob 的公钥加密该对称密钥。
3. Alice 将加密后的对称密钥和加密后的明文都发送给 Bob。
4. Bob 使用自己的私钥解密对称密钥。
5. Bob 使用解密后的对称密钥解密消息。

除 Bob 之外，没有人能解密该对称密钥，因为只有 Bob 拥有用于解密的私钥。因此，昂贵的公钥加密只应用于少量密钥数据。

最常用的公钥算法是由 Rivest、Shamir 和 Adleman 发明的 RSA 算法。直到 2000 年 10 月，该算法一直受一项专利保护，该专利转让给了 RSA Security, Inc.。许可证并不便宜——通常是 3% 的版税，每年最低支付 50,000 美元。现在该算法已进入公有领域。

要使用 RSA 算法，你需要一个公钥/私钥对。像这样使用 KeyPairGenerator：

```java
KeyPairGenerator pairgen = KeyPairGenerator.getInstance("RSA");
var random = new SecureRandom();
pairgen.initialize(KEYSIZE, random);
KeyPair keyPair = pairgen.generateKeyPair();
Key publicKey = keyPair.getPublic();
Key privateKey = keyPair.getPrivate();
```

代码清单 10.19 中的程序有三个选项。-genkey 选项生成一个密钥对。-encrypt 选项生成一个 AES 密钥，并用公钥将其包装。

```java
Key key = . . .; // an AES key
Key publicKey = . . .; // a public RSA key
Cipher cipher = Cipher.getInstance("RSA");
cipher.init(Cipher.WRAP_MODE, publicKey);
byte[] wrappedKey = cipher.wrap(key);
```

然后它会生成一个文件，其中包含

- 被包装密钥的长度
- 被包装密钥的字节
- 用 AES 密钥加密后的明文

-decrypt 选项用于解密这样的文件。要试用该程序，首先生成 RSA 密钥：

