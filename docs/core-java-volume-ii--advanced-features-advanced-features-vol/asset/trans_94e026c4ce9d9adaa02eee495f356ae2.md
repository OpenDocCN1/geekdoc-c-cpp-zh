

java rsa.RSATest -genkey public.key private.key

然后加密一个文件：

```text
java rsa.RSATest -encrypt plaintextFile encryptedFile public.key
```

最后，解密该文件并验证解密后的文件与明文匹配：

```text
java rsa.RSATest -decrypt encryptedFile decryptedFile private.key
```

### 清单 10.19 `rsa/RSATest.java`

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
 * @version 1.02 2018-05-01
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
            var random = new SecureRandom();
            pairgen.initialize(KEYSIZE, random);
            KeyPair keyPair = pairgen.generateKeyPair();
            try (var out = new ObjectOutputStream(new FileOutputStream(args[1])))
            {
                out.writeObject(keyPair.getPublic());
            }
            try (var out = new ObjectOutputStream(new FileOutputStream(args[2])))
            {
                out.writeObject(keyPair.getPrivate());
            }
        }
        else if (args[0].equals("-encrypt"))
        {
            KeyGenerator keygen = KeyGenerator.getInstance("AES");
            var random = new SecureRandom();
            keygen.init(random);
            SecretKey key = keygen.generateKey();

            // wrap with RSA public key
            try (var keyIn = new ObjectInputStream(new FileInputStream(args[3]));
                 var out = new DataOutputStream(new FileOutputStream(args[2]));
                 var in = new FileInputStream(args[1]))
            {
                var publicKey = (Key) keyIn.readObject();
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
            try (var in = new DataInputStream(new FileInputStream(args[1]));
                 var keyIn = new ObjectInputStream(new FileInputStream(args[3]));
                 var out = new FileOutputStream(args[2]))
            {
                int length = in.readInt();
                var wrappedKey = new byte[length];
                in.read(wrappedKey, 0, length);

                // unwrap with RSA private key
                var privateKey = (Key) keyIn.readObject();

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

你现在已经看到了 Java 安全模型如何允许对代码进行受控执行，这是 Java 平台一个独特且日益重要的方面。你也看到了 Java 库提供的认证和加密服务。

在下一章中，我们将深入探讨高级 Swing 和图形编程。

## 高级 Swing 和图形

### 本章内容

- 11.1 表格，第 613 页
- 11.2 树，第 652 页
- 11.3 高级 AWT，第 693 页
- 11.4 光栅图像，第 744 页
- 11.5 打印，第 772 页

在本章中，我们将继续第一卷中关于 Swing 用户界面工具包和 AWT 图形的讨论。我们重点介绍既适用于客户端用户界面，也适用于服务器端图形和图像生成的技术。Swing 拥有用于渲染表格和树的复杂组件。借助 2D 图形 API，你可以生成任意复杂度的矢量图。ImageIO API 允许你操作光栅图像。最后，你可以使用打印 API 生成打印输出和 PostScript 文件。

### 11.1 表格

JTable 组件显示对象的二维网格。表格在用户界面中很常见，Swing 团队在表格控件上投入了大量精力。表格本质上很复杂，但——也许比其他 Swing 类更成功——JTable 组件隐藏了大部分复杂性。你只需编写几行代码，就能生成功能齐全、行为丰富的表格。你也可以编写更多代码，为你的特定应用定制显示和行为。

在接下来的几节中，我们将解释如何创建简单的表格、用户如何与其交互，以及如何进行一些最常见的调整。与其他复杂的 Swing 控件一样，不可能完整地涵盖所有方面。欲了解更多信息，请参阅 David M. Geary 所著的 *Graphic Java™, Third Edition*（Prentice Hall, 1999），或 Kim Topley 所著的 *Core Swing*（Prentice Hall, 1999）。

### 11.1.1 简单表格

JTable 不存储自身的数据，而是从*表格模型*中获取这些数据。JTable 类有一个构造函数，可以把对象的二维数组包装到默认模型中。这就是我们在第一个例子中使用的策略；在本章后面，我们将讨论表格模型。

图 11.1 显示了一个典型表格，描述了太阳系行星的属性。（如果一颗行星主要由氢和氦组成，那么它就是*气态的*。对于“Color”列中的条目，你不必太当真——该列之所以被添加，是因为它将在后面的代码示例中用到。）

如清单 11.1 的代码所示，表格数据以 Object 值的二维数组形式存储：

```java
Object[][] cells =
{
    { "Mercury", 2440.0, 0, false, Color.YELLOW },
    { "Venus", 6052.0, 0, false, Color.YELLOW },
    . . .
}
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_636_0.png)

图 11.1 简单表格

> **注意：** 这里我们利用了自动装箱。第二、三、四列中的条目会自动转换为类型为 `Double`、`Integer` 和 `Boolean` 的对象。

表格只是简单地对每个对象调用 `toString` 方法来显示它。这就是为什么颜色会显示为 `java.awt.Color[r=...,g=...,b=...]`。

在一个单独的字符串数组中提供列名：

```java
String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous", "Color" };
```

然后，根据单元格数组和列名数组构造一个表格：

```java
var table = new JTable(cells, columnNames);
```

你可以用通常的方式添加滚动条——将表格包装在 `JScrollPane` 中：

```java
var pane = new JScrollPane(table);
```

滚动表格时，表头不会滚出视野。接下来，单击某个列标题并将其向左或向右拖动。你会看到整个列脱离（见图 11.2）。你可以将其放到其他位置。这仅在*视图*中重新排列列，数据模型不受影响。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_637_0.png)

**图 11.2** 移动列

要调整列的大小，只需将光标放在两列之间，直到光标形状变为箭头。然后，将列边界拖到所需位置（见图 11.3）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_638_0.png)

**图 11.3** 调整列大小

你应该让单元格不可编辑，或者处理单元格编辑事件并更新模型。我们将在本节后面讨论这些主题。

最后，单击列标题。行会自动排序。再次单击，排序顺序反转。此行为由以下调用激活：

```java
table.setAutoCreateRowSorter(true);
```

你可以通过以下调用打印表格：

```java
table.print();
```

> **警告：** 如果你没有将表格包装到滚动窗格中，则需要显式添加表头：
>
> ```java
> add(table.getTableHeader(), BorderLayout.NORTH);
> ```

### 清单 11.1 `table/TableTest.java`

```java
package table;

import java.awt.*;
import java.awt.print.*;

import javax.swing.*;

/**
 * This program demonstrates how to show a simple table.
 * @version 1.14 2015-05-01
 * @author Cay Horstmann
 */
```

