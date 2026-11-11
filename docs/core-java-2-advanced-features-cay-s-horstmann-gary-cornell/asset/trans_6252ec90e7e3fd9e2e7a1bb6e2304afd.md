
```java
    putData(bytes, inLength); // put data to destination
    inLength = in.read(bytes);
}
```

加密流类会透明地处理对 `update` 和 `doFinal` 的调用，这显然提供了便利。

## javax.crypto.CipherInputStream 1.4

- `CipherInputStream(InputStream in, Cipher cipher)`
  构造一个输入流，它从 `in` 读取数据，并使用给定的加密器对其解密或加密。
- `int read()`
- `int read(byte[] b, int off, int len)`
  从输入流读取数据，这些数据会自动解密或加密。

## javax.crypto.CipherOutputStream 1.4

- `CipherOutputStream(OutputStream out, Cipher cipher)`
  构造一个输出流，它把数据写入 `out`，并使用给定的加密器对其加密或解密。
- `void write(int ch)`
- `void write(byte[] b, int off, int len)`
  把数据写入输出流，这些数据会自动加密或解密。
- `void flush()`
  刷新加密器缓冲区，并在必要时执行填充。

### 9.5.4 公钥密码

你在上一节看到的 AES 密码是一种*对称密码*。加密和解密使用同一个密钥。对称密码的致命弱点是密钥分发。如果爱丽丝向鲍勃发送加密消息，鲍勃需要爱丽丝使用的同一密钥。如果爱丽丝更换了密钥，她需要把消息以及新密钥通过安全信道发送给鲍勃。但也许她并没有通往鲍勃的安全信道——这正是她一开始要给他加密消息的原因。

公钥密码学解决了这个问题。在公钥密码中，鲍勃拥有一对密钥，由公钥和匹配的私钥组成。鲍勃可以把公钥发布到任何地方，但必须严密保管私钥。爱丽丝只需使用公钥加密她发给鲍勃的消息。

实际上，事情并没有那么简单。所有已知的公钥算法都比 DES 或 AES 等对称密钥算法*远远*慢。使用公钥算法加密大量信息并不实际。不过，通过将公钥密码与快速对称密码结合，可以轻松克服这个问题，如下所示：

1. 爱丽丝生成一个随机对称加密密钥。她用该密钥加密自己的明文。
2. 爱丽丝用鲍勃的公钥加密该对称密钥。
3. 爱丽丝把加密后的对称密钥和加密后的明文都发送给鲍勃。
4. 鲍勃用他的私钥解密对称密钥。
5. 鲍勃用解密后的对称密钥解密消息。

除了鲍勃，没有人能解密该对称密钥，因为只有鲍勃拥有用于解密的私钥。因此，昂贵的公钥加密只应用于少量密钥数据。

最常用的公钥算法是由 Rivest、Shamir 和 Adleman 发明的 RSA 算法。直到 2000 年 10 月，该算法一直受一项专利保护，该专利转让给了 RSA Security, Inc.。许可证并不便宜——通常要支付 3% 的版税，且每年最低支付 50,000 美元。现在该算法已进入公有领域。

要使用 RSA 算法，你需要一对公钥/私钥。像这样使用 `KeyPairGenerator`：

```java
KeyPairGenerator pairgen = KeyPairGenerator.getInstance("RSA");
SecureRandom random = new SecureRandom();
pairgen.initialize(KEYSIZE, random);
KeyPair keyPair = pairgen.generateKeyPair();
Key publicKey = keyPair.getPublic();
Key privateKey = keyPair.getPrivate();
```

代码清单 9.20 中的程序有三个选项。`-genkey` 选项生成一个密钥对。`-encrypt` 选项生成一个 AES 密钥，并用公钥将其*包装*。

```java
Key key = ...; // an AES key
Key publicKey = ...; // a public RSA key
Cipher cipher = Cipher.getInstance("RSA");
cipher.init(Cipher.WRAP_MODE, publicKey);
byte[] wrappedKey = cipher.wrap(key);
```

然后它生成一个文件，其中包含

- 被包装密钥的长度
- 被包装的密钥字节
- 用 AES 密钥加密的明文

`-decrypt` 选项解密这样的文件。要试用该程序，首先生成 RSA 密钥：

```
java rsa.RSATest -genkey public.key private.key
```

然后加密一个文件：

```
java rsa.RSATest -encrypt plaintextFile encryptedFile public.key
```

最后，解密它并验证解密后的文件与明文一致：

```
java rsa.RSATest -decrypt encryptedFile decryptedFile private.key
```

### 代码清单 9.20 `rsa/RSATest.java`

```java
package rsa;

import java.io.*;
import java.security.*;
import javax.crypto.*;

/**
 * This program tests the RSA cipher. Usage:<br>
 * java rsa.RSATest -genkey public private<br>
 * java rsa.RSATest -encrypt plaintext encrypted public<br>
 * java rsa.RSATest -decrypt encrypted decrypted private<br>
 * @author Cay Horstmann
 * @version 1.01 2012-06-10
 */
public class RSATest
{
   private static final int KEYSIZE = 512;

   public static void main(String[] args)
      throws IOException, GeneralSecurityException, ClassNotFoundException
   {
      if (args[0].equals("-genkey"))
      {
         KeyPairGenerator pairgen = KeyPairGenerator.getInstance("RSA");
         SecureRandom random = new SecureRandom();
         pairgen.initialize(KEYSIZE, random);
         KeyPair keyPair = pairgen.generateKeyPair();
         try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(args[1])))
         {
            out.writeObject(keyPair.getPublic());
         }
         try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(args[2])))
         {
            out.writeObject(keyPair.getPrivate());
         }
      }
      else if (args[0].equals("-encrypt"))
      {
         KeyGenerator keygen = KeyGenerator.getInstance("AES");
         SecureRandom random = new SecureRandom();
         keygen.init(random);
         SecretKey key = keygen.generateKey();

         // wrap with RSA public key
         try (ObjectInputStream keyIn = new ObjectInputStream(new FileInputStream(args[3]));
              DataOutputStream out = new DataOutputStream(new FileOutputStream(args[2]));
              InputStream in = new FileInputStream(args[1]))
         {
            Key publicKey = (Key) keyIn.readObject();
            Cipher cipher = Cipher.getInstance("RSA");
            cipher.init(Cipher.WRAP_MODE, publicKey);
            byte[] wrappedKey = cipher.wrap(key);
            out.writeInt(wrappedKey.length);
            out.write(wrappedKey);

            cipher = Cipher.getInstance("AES");
            cipher.init(Cipher.ENCRYPT_MODE, key);
            Util.crypt(in, out, cipher);
         }
      }
      else
      {
         try (DataInputStream in = new DataInputStream(new FileInputStream(args[1]));
              ObjectInputStream keyIn = new ObjectInputStream(new FileInputStream(args[3]));
              OutputStream out = new FileOutputStream(args[2]))
         {
            int length = in.readInt();
            byte[] wrappedKey = new byte[length];
            in.read(wrappedKey, 0, length);

            // unwrap with RSA private key
            Key privateKey = (Key) keyIn.readObject();

            Cipher cipher = Cipher.getInstance("RSA");
            cipher.init(Cipher.UNWRAP_MODE, privateKey);
            Key key = cipher.unwrap(wrappedKey, "AES", Cipher.SECRET_KEY);

            cipher = Cipher.getInstance("AES");
            cipher.init(Cipher.DECRYPT_MODE, key);

            Util.crypt(in, out, cipher);
         }
      }
   }
}
```

你现在已经了解了 Java 安全模型如何允许受控的代码执行，这是 Java 平台一个独特且日益重要的方面。你还了解了 Java 库提供的身份验证和加密服务。我们没有涵盖一些高级和专门的问题，其中包括：

- 用于“通用安全服务”的 GSS-API，它为 Kerberos 协议（原则上还包括用于安全消息交换的其他协议）提供支持。教程位于 http://docs.oracle.com/javase/7/docs/technotes/guides/security/jgss/tutorials。
- 对简单认证与安全层（SASL）的支持，LDAP 和 IMAP 使用它。如果需要在应用程序中实现 SASL，请参阅 http://docs.oracle.com/javase/7/docs/technotes/guides/security/sasl/sasl-refguide.html。
- 对 SSL 的支持。在 HTTP 上使用 SSL 对应用程序员是透明的；只需使用以 https 开头的 URL。如果要将 SSL 添加到应用程序，请参阅 Java 安全套接字扩展（JSSE）参考文档：http://java.sun.com/javase/6/docs/technotes/guides/security/jsse/JSSERefGuide.html。

在下一章中，我们将深入探讨高级 Swing 编程。
