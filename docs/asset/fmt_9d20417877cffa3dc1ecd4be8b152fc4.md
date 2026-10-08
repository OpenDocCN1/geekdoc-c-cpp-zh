
```java
/**
 * 加密一个值。
 * @param b 要加密的值（0 到 255 之间）
 * @return 加密值
 */
public int encrypt(int b) {
    return (b + key) % 256;
}
```

### section_2/CaesarEncryptor.java

```java
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.util.Scanner;

/**
 * 该程序使用凯撒密码加密文件。
 */
public class CaesarEncryptor {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        try {
            System.out.print("Input file: ");
            String inputFile = in.next();
            System.out.print("Output file: ");
            String outputFile = in.next();
            System.out.print("Encryption key: ");
            int key = in.nextInt();

            InputStream inputStream = new FileInputStream(inputFile);
            OutputStream outputstream = new FileOutputStream(outputFile);

            CaesarCipher cipher = new CaesarCipher(key);
            cipher.encrypt(inputStream, outputstream);

            inputStream.close();
            outputstream.close();
        } catch (IOException exception) {
            System.out.println("Error processing file: " + exception);
        }
    }
}
```

## 1.3 随机访问

### 负字节值

`InputStream`类的方法返回 `-1` 或读取到的字节（0 到 255 之间的值）。人们很容易将此值放入 `byte` 类型变量中，但事实并不是好主意。在 Java 中，`byte` 类型是有符号的，范围从 -128 到 127。当将 128 到 255 之间的 `int` 值转换为 `byte` 时，结果是一个负值。这很不方便。解决方法是使用 `int` 值。不要使用 `byte` 类型。

### 1.3 随机访问

从头到顺序读取文件是无效的。在本节中，你将学习如何访问文件的任意位置。考虑一个包含银行账户的文件。我们想要处理某些账户的余额。我们可以将所有账户数据读取到数组中，更新更改的信息，然后保存数据。但如果文件中的数据量很大，我们可能会进行大量的读写操作来产生少量记录。

在顺序文件访问中，文件一次处理一个字节。这与你在第 7 章中编写的文件完全不同，那时你从开始读取整个内容直到结束。那种模式被称为顺序访问。现在我们想要访问文件的特定位置并仅更改这些位置。这种访问模式被称为随机访问（见图 3）。随机访问并没有“随机”——该术语意味着你可以读取和修改存储在文件中任何位置的字节。

## 846 第 19 章 流与二进制输入/输出

图 3 顺序访问与随机访问

随机访问允许访问文件的任意位置，而无需经过之前的字节。

只有磁盘文件支持随机访问；连接键盘和终端窗口的系统流不支持。每个磁盘文件都有特殊的文件指针位置。通常，文件指针位于文件末尾，任何输出都会附加到末。然而，如果你将文件指针移动到文件中间并写入，它将覆盖已有的内容。下一个命令从文件指针位置开始读取输入。你可以将文件指针移动到文件中最后一个字节的之后，但不能更远。

在 Java 中，你使用 `RandomAccessFile` 对象来访问文件并移动文件指针。打开随机访问文件，你需要指定文件名和一个指定打开模式的字符串。你可以以读取“r”或读写“rw”的模式打开文件。例如，以下命令以读写方式打开 `bank` 文件：

```
RandomAccessFile f = new RandomAccessFile("bank.dat", "rw");
```

方法

```
f.seek(position);
```

将文件指针移动到指定的位置，从文件开始计数。文件的第一个字节位置为 0。要查找到文件指针的当前位置（从文件开始计数），使用

```
long position = f.getFilePointer();
```

由于文件可能很大，文件指针值是整数。要确定文件中的字节数，使用 `length` 方法：

```
long fileLength = f.length();
```

在本节末尾的示例中，我们使用随机访问文件存储一组账户，每个账户都有一个账户号码和一个当前余额。测试程序允许你选择一个账户并存入资金。如果你想操作文件中的数据集，你必须特别注意数据的格式。将数据保存为文本。假设账户 1001 的余额为 900 元，账户 1015 的余额为 0。

文件指针是随机访问文件中的位置。由于文件可能很大，文件指针的类型是 `long`。

| 1 0 0 1 | 9 0 0 | 1 0 1 5 | 0 |

我们想要向账户 1001 存入 100 元。假设我们将文件指针移动到旧值的第一个字符：

| 1 0 0 1 | 9 0 0 | 1 0 1 5 | 0 |

# 19.3 随机访问 847

如果我们直接写出新值，结果如下：

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_882_0.png)

这种效果并不好。数据覆盖了分隔值之间的空间。

为了能够更新文件中的值，你必须给每个值分配一个足够大的固定大小。这样，快速跳到某条记录（例如第 50 条记录）就会变得容易得多，而不需要先读取前 49 条记录。将文件指针设置为 `x * 记录大小`。

在具有固定记录大小的文件中存储数字时，以二进制或文本格式访问它们更为方便。例如，`RandomAccessFile` 存储二进制数据。`readInt` 和 `writeInt` 方法以四字节为单位读取和写入整数。`readDouble` 和 `writeDouble` 方法以八字节为单位处理双精度点数。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_882_1.png)

```java
double x = f.readDouble();
f.writeDouble(x);
```

如果我们将账户号码保存为整数和双精度值，那么每个账户就包含 12 字节：4 字节用于整数，8 字节用于双精度浮点值。

现在我们已经确定了文件布局，就可以实现访问文件的方法了。在本节的程序中，我们使用 `BankData` 类在随机访问格式和银行账户对象之间进行转换。通过将文件长度除以记录大小来确定账户总数。

```java
public int size() throws IOException {
    return (int) (file.length() / RECORD_SIZE);
}
```

要读取文件中的第 n 个账户，`read` 方法将文件指针定位到偏移量 `n * RECORD_SIZE` 处，然后读取数据并构建一个银行账户：

写入账户的方法相同：

```java
public void write(int n, BankAccount account) throws IOException {
    file.seek(n * RECORD_SIZE);
    file.writeInt(account.getAccountNumber());
    file.writeDouble(account.getBalance());
}
```

测试程序要求用户输入账户号码和存款金额。如果该账户不存在，则会创建它。存入资金后，用户可以选择继续或退出。当程序再次运行时，银行数据将会被保存并重新加载。

# 848 第 19 章 流与二进制输入/输出

# section_3/BankSimulator.java

```java
import java.io.IOException;
import java.util.Scanner;
/**
* 此程序演示了随机访问。你可以访问
*现有账户并存款，或者创建新账户。
* 账户保存在随机访问文件中。
 */
public class BankSimulator {
    public static void main(String[] args) throws IOException {
        Scanner in = new Scanner(System.in);
        BankData data = new BankData();
        try {
            data.open("bank.dat");
            boolean done = false;
            while (done) {
                System.out.print("Account number: ");
                int accountNumber = in.nextInt();
                System.out.print("Amount to deposit: ");
                double amount = in.nextDouble();
                int position = data.find(accountNumber);
                BankAccount account;
                if (position >= 0) {
                    account = data.read(position);
                    account.deposit(amount);
                    System.out.println("New balance: " + account.getBalance());
                } else {
                    // 添加账户
                    account = new BankAccount(accountNumber, amount);
                    position = data.size(); // 注意：此处原文逻辑似乎有误，按原文翻译
                    data.write(position, account);
                }
                System.out.print("Done? (Y/N) ");
                String input = in.next();
                if (input.equalsIgnoreCase("Y")) done = true;
            }
        } finally {
            data.close();
        }
    }
}
```

# section_3/BankData.java

```java
import java.io.IOException;
import java.io.RandomAccessFile;
/**
* 此类是随机访问文件的句柄，
* 包含银行账户记录。
 */
public class BankData {
    private RandomAccessFile file;
    public static final INT_SIZE = 4;
    public static final DOUBLE_SIZE = 8;
    public static final int RECORD_SIZE = INT_SIZE + DOUBLE_SIZE;

    public BankData() {
        file = null;
    }

    /**
     * 打开文件。
     * @param filename 文件名
     */
    public void open(String filename) throws IOException {
        file = new RandomAccessFile(filename, "rw");
    }

    /**
     * 获取账户数量。
     * @return 账户数量
     */
    public int size() {
        return (int) (file.length() / RECORD_SIZE);
    }

    /**
     * 关闭文件。
     */
    public void close() throws IOException {
        if (file != null) file.close();
        file = null;
    }

    /**
     * 读取文件中的第 n 个账户。
     * @param n 索引
     * @return 账户对象
     */
    public BankAccount read(int n) throws IOException {
        file.seek(n * RECORD_SIZE);
        return new BankAccount(file.readInt(), file.readDouble());
    }

    /**
     * 写入账户。
     * @param n 索引
     * @param account 账户对象
     */
    public void write(int n, BankAccount account) throws IOException {
        file.seek(n * RECORD_SIZE);
        file.writeInt(account.getAccountNumber());
        file.writeDouble(account.getBalance());
    }

    /**
     * 在文件中查找账户的位置。
     * @param accountNumber 要查找的账户号码
     * @return 的位置，未找到返回 -1
     */
    public int find(int accountNumber) throws IOException {
        for (int i = 0; i < size(); i++) {
            file.seek(i * RECORD_SIZE);
            if (file.readInt() == accountNumber) {
                return i;
            }
        }
        return -1;
    }
}
```

# 19.4 对象流 851

在 19.3 中，我们通过逐个读取值来读取 `BankAccount` 对象。实际上，有一种更简单的方法。`ObjectOutputStream` 可以将整个对象保存到磁盘，而 `ObjectInputStream` 可以将它们读。对象是以二进制格式保存的；因此使用流而不是写入器。例如，你可以如下将 `BankAccount` 对象写入文件：

```java
BankAccount b = ...;
ObjectOutputStream out = new ObjectOutputStream(
new FileOutputStream("bank.dat"));
out.writeObject(b);
```

输出流会自动保存对象的所有实例变量。当我们回读对象时，使用 `ObjectInputStream` 类的 `readObject` 方法来记住保存的对象类型并进行强制转换：

```java
ObjectInputStream in = new ObjectInputStream(
new FileInputStream("bank.dat"));
BankAccount b = (BankAccount) in.readObject();
```

你可以做得更好，可以将许多对象存储在一个列表或其他对象中，然后保存该对象：

```java
ArrayList<BankAccount> a = new ArrayList<>();
// 现在向 a 中添加许多 BankAccount 对象
out.writeObject(a);
```

只需一条指令，就可以保存整个列表及其包含的所有对象。同样需一条指令即可读取所有内容：

```java
ArrayList<BankAccount> a = (ArrayList<BankAccount>) in.readObject();
```
