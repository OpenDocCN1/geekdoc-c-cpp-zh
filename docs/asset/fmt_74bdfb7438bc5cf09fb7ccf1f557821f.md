
当然，如果一个类包含一个银行账户的 `ArrayList`，那么你就可以保存并恢复一个 `Bank` 对象。这时，它包含的所有 `BankAccount` 对象也会被自动保存和恢复。本节末的示例程序使用了这种方法。

要将特定类的对象放入对象流中，该类必须实现 `Serializable` 接口。该接口没有方法，因此实现它不需要任何精力：

```java
class BankAccount implements Serializable {
}
```

# 852 第 19 章 流与二进制输入/输出

将对象保存到流的过程被称为**序列化**，因为每个对象在流中都被分配了一个序列号。如果同一个对象被保存两次，则第二次只写入序列号。当对象被读回时，重复的序列号被视为同一个对象。

下面是一个展示序列化应用的示例程序。`Bank` 类管理银行账户集合。`Bank` 和 `Account` 类都实现了 `Serializable` 接口。运行该程序。当程序退出时，它会将银行对象（以及它包含的所有银行账户）保存到文件 `bank` 中。当程序再次启动时，文件会被加载，上一次程序运行的更改会自动反映。然而，如果程序是第一次运行，或者文件被删除了，程序将从一个新的银行开始。

## # section_4/Bank.java

```java
import java.io.Serializable;
import java.util.ArrayList;
/**
 * 此银行包含一个银行账户集合。
 */
public class Bank implements Serializable
{
    private ArrayList<BankAccount> accounts;
    /**
     * 构造一个没有银行账户的银行。
     */
    public Bank()
    {
        accounts = new ArrayList<>();
    }
    /**
     * 向此银行添加一个账户。
     * @param a 要添加的账户
     */
    public void addAccount(BankAccount a)
    {
        accounts.add(a);
    }
    /**
     * 根据给定的编号查找银行。
     * @param accountNumber 要查找的账号
     * @return 对应编号的账户，如果没有此类账户则返回 null
     */
    public BankAccount find(int accountNumber)
    {
        for (BankAccount a : accounts)
        {
            if (a.getAccountNumber() == accountNumber) // 找到了银行账户
                return a;
            }
        }
        return null; // 在整个列表中没有匹配项
    }
}
```

## 19.4 对象流 853

## # section_4/SerialDemo.java

```java
1 import java.io.File;
2 import java.io.IOException;
3 import java.io.FileInputStream;
4 import java.io.FileOutputStream;
5 import java.io.ObjectInputStream;
6 import java.io.ObjectOutputStream;

/**
* 此程序演示了 Bank 对象的的数据序列化。
* 如果存在带有序列化数据的文件，则加载它。
* 否则，程序将从一个新的银行开始。
* 将银行账户添加到银行中。然后保存
**对象。
*/

15 public class SerialDemo
16 {
17 public static void main(String[] args)
18 throws IOException, ClassNotFoundException
19 {
20 Bank firstBankJava;
21 File f = new File("bank.dat");
22 if (f.exists()) {
23 {
24 ObjectInputStream in = new ObjectInputStream(
25 new FileInputStream(f));
26 firstBankJava = (Bank) in.readObject();
27 in.close();
28 }
29 else
30 {
31 firstBankJava = new Bank();
32 firstBankJava.addAccount(new Account(1001, 20000));
33 firstBankJava.addAccount(new Account(1015, 10000));
34 }
35 
36 // 存款一些钱
37 BankAccount a = firstBankJava.find(1001);
38 a.deposit(100);
39 System.out.println(a.getAccountNumber() + ":" + a.getBalance());
40 a = firstBankJava.find(1015);
41 System.out.println(a.getAccountNumber() + ":" + a.getBalance());
42 {
43 ObjectOutputStream out = new ObjectOutputStream(
44 new FileOutputStream(f));
45 out.writeObject(firstBankJava);
46 out.close();
47 }
}
```

程序运行

1001:20100.0

1015:10000.0

# 第 19 章 流与二进制输入/输出

## 第二次程序运行

```
1001:20200.0
1015:10000.0
```

- 8. 为什么使用 `ObjectOutputStream` 比使用 `RandomAccessFile` 保存对象更简单简单？

- 9. 你需要对 9.6.2 节中的 `Country` 类做什么，以便使其对象可以被保存到 `ObjectOutputStream` 中？

现在就练习：你可以尝试章节末尾的练习：R19.8, R19.9, P19.9。

## 选择文件格式

许多程序允许用户将工作保存到文件中。程序用户以后可以加载这些文件并继续处理数据，或将文件发送给他人。当你开发程序时，你需要决定如何存储数据。`How To` 允许你选择合适的机制来保存和加载程序的数据。

### 步骤 1 选择一种数据格式。

你需要问自己的最重要的问题是关于用于保存数据的格式：

* 你的程序是否以纯文本形式处理文本？如果是，请使用读取器（readers）和写入器（writers）。

* 你的程序是否更新文件的部分部分？如果是，请使用随机访问（random access）。

* 你的程序是否读取或写入二进制数据？

# 编程练习 857

# 复习题

- R19.1 流（stream）和读取器（reader）之间的区别是什么？

- R19.2 向新的 `FileWriter("output.txt", "UTF-8")` 写入几行文本，并向新的 `FileWriter("output2.txt", "UTF-16")` 写入相同的文本。输出文件有什么不同？

- R19.3 在 Java 中如何打开一个读写的文件？

- R19.4 如果尝试向文件读取器（file reader）写入数据会发生什么？

- R19.5 如果尝试向一个仅以读打开的随机访问文件（random access file）写入数据会发生什么？如果没有试过，请尝试一下。

- R19.6 如何破解凯撒密码？换说，在不知道密钥的情况下，如何读取一个用凯撒密码加密的文档？

- R19.7 如果尝试在对象流中保存一个不可序列化的对象，会发生什么？请尝试一下并报告你的结果。

- R19.8 对于你已经在书中遇到的 `java.lang` 和 `java` 包中的类，请实现 `Serializable` 接口。

- R19.9 为什么将整个 `ArrayList` 保存到对象流中，比编写一个循环来写入每个元素更好？

- R19.10 顺序访问（sequential access）和随机访问（random access）之间的区别是什么？

- R19.11 文件中的文件指针是什么？你如何移动它？如何告知当前位置？为什么它是一个长整型（long integer）？

- R19.12 如何将文件指针移动到文件的第一个字节？到最后一个字节？到文件的正中间？

- R19.13 如果尝试将文件指针移动到文件末尾之后会发生什么？尝试一下并报告你的结果。

- R19.14 你能移动 `System.in` 的文件指针吗？

# 编程练习

- P19.1 随机单字母替换密码。凯撒密码通过固定偏移移动所有字母，太容易破解了。这里有一个更好的主意：密钥不要使用数字，而使用单词。假设密钥是 FE。然后删除重复字母，得到 FEATHR，并按反序添加字母表中的其他字母。现在按如下方式加密字母：

| A C D E F G H I J K L M N O P Q R S T U V W X Y Z |

|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

| F E A T H R Z Y X W V U S Q P O N L K J I G D C B | |

编写一个程序，使用这种密码加密或解密文件。密钥通过命令行选项 `-k` 指定。命令行选项 `-d` 指定解密。例如：

```
Java Encrypt -k FEATHER.txt output.txt
```

- P19.2 字母频率。如果你使用 P19.1 题中的密码加密文件，它所有的字母都会发生位移，看起来在不知道关键词的情况下没有希望解密。猜测答案似乎是徒劳无功，因为关键词太多了。然而，一个精通破译的人可以很快破解这种密码。英语字母的平均频率是众所周知的。最常见的字母是 E，出现概率为 13%。以下是英语字母的平均频率：

| A | 8% | V | 1% |

| B | <1% | W | 2% |

| C | 3% | X | <1% |

| D | 4% | R | 8% |

| E | 13% | S | 6% |

| F | 3% | T | 9% |

| G | 2% | U | 3% |

| H | N | 8% |

编写一个程序，读取输入文件并打印文件中字母的频率。这种工具将帮助破译者。如果加密文件中频率最高的字母是 H 和 K，那么它们极有可能是 E 和 T 的加密结果。

- P19.3 维吉尼亚密码（Vigenère cipher）。单字母替换密码的问题在于它可以被频率分析轻易破解。所谓的维吉尼亚密码通过根据字母在输入中的位置将其编码为几个密密字母之一，克服了这个问题。选择一个关键词，例如，将输入文本的第一个字母像 TIGER 的第一个字母一样编码：

```
A C D E F G H I J K L M N O P Q R S T U W X Y Z
↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓  ↓ ↓ ↓ ↓ ↓ ↓
T U W X Y Z A C D E F G H I J K L M N O P Q R S
```

也就是说，编码后的字母表只是从 T 开始偏移的普通字母表。第二个字母根据此映射加密：

```
A B D E F G H I J K L M N O P Q R S T U W X Y Z
↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓
I J K L M N O P Q R S T U W X Y Z A B C D E F H
```

输入文本中的第三、第四和第五个字母使用带有 G、E 和 R 字符的字母表加密。因为密钥只有五个字母，所以输入文本的第六个字母的加密方式与第一个相同。

# 编程练习 859

编写一个程序使用这种密码加密或解密输入文本。命令行参数与 P19.1 相同。

- P19.4 完美密码（fair cipher）。防止对加密文本进行简单字母分析的另一种方法是对字母对进行加密。实现此目的的一种简单方案是完美密码。你选择一个关键词并删除其中的重复字母。然后将关键词和字母表中剩余的字母填充到一个 5 x 5 的方格中（因为有 25 个格子，I 和 J 被视为同一个字母）。以下是使用关键词 FAIRPLAY 的布局：

```
P L A F
I R B C D
E G K M
O Q S T
U W X Z
```

要加密字母对（例如 AT），查看以 A 和 T 为顶点的矩形：

```
P L A F
I R B C D
E G K M
O Q S T
U W X Z
```

该对的编码通过查看矩形的两个顶点形成——在这种情况下，如果两个字母恰好在同一行或同一列（例如 GO），只需交换这两个字母。解密方法相同。编写一个程序使用这种密码加密或解密输入文本。命令行参数参考练习 P19.1。

- P19.5 编写一个程序打开一个二进制文件并打印该文件中所有值在 32 到 126 之间的 ASCII 字符。每 64 个字符打印一个换行符。当你用你的程序处理文字处理器文档时会发生什么？处理类文件时呢？

- P19.6 编写一个 BankSimulator 程序，使其能够删除账户。要从数据文件中删除记录，请将其填充为零。

- P19.7 P19.6 题中的数据文件末尾可能有许多占用空间的删除记录。编写一个程序压缩此类文件，将所有活动记录移动到开头并缩短文件长度。提示：使用 `RandomAccessFile` 类的 `setLength` 方法来截断文件。在 API 文档查询该方法的行为。

- P19.8 编写一个操作产品记录数据库的程序。记录存储在二进制文件中。每个记录包含：

* 产品名称：30 个字符，每个两个字节 = 60 字节

* 价格：一个 double = 8 字节

* 数量：一个 int = 8 字节

程序应允许用户添加记录、查找匹配产品名称的记录，并更改指定产品的价格和数量。

- P19.9 增强 Serializer 程序，以演示它可以保存和恢复银行账户。

- P19.10 为 BankSimulator 实现图形界面。使用序列化。当用户使用 Files->Save 时，保存选中的形状。

- P19.11 编写一个图形应用程序，用户可以通过点击面板在鼠标位置添加形状（矩形、椭圆等）。这些形状存储在一个数组列表中。

# 20 多线程

## 本章目标

理解多个线程如何能够并行执行

- 学习如何实现线程

- 理解竞态条件和死锁

- 学习使用锁（locks）和条件（conditions）来避免共享对象的损坏

- 使用线程进行动画编程

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_896_0.png)

## 本章目录

20.1 运行线程 W862

编程技巧 20.1: 使用 Runnable 接口 W866

特殊专题 20.1: 线程池 W866

20.2 终止线程 W867

编程技巧 20.2: 在 Thread 的 run 方法中检查线程中断 W869

20.3 竞态条件 W869

20.4 同步对象访问 W875

20.5 避免死锁 W877

常见错误 20.1: 在未调用 signalAll 的情况下调用 await W882

常见错误 20.2: 在未锁定对象的情况下调用 signalAll W883

特殊专题 20.2: 对象锁与同步方法 W883

特殊专题 20.3: Java 内存模型 W884

20.6 应用：算法动画 W884

随机知识 20.1: 嵌入式系统 W893

## 20.1 运行线程

线程是独立于程序其他部分执行的单元。Java 虚拟机会执行每个线程一小段时间，然后切换到其他线程。实际上，如果计算机有多个中央处理器（CPU），那么某些线程可以并行运行，每个处理器运行一个线程。在 Java 中运行线程非常简单——遵循以下步骤即可：

1. 编写一个实现 `Runnable` 接口的类。该接口有一个名为 `run` 的方法：

```
public interface Runnable {
    void run();
}
```

2. 将任务代码放入类的 `run` 方法中：

```java
public class MyRunnable implements Runnable {
    public void run() {
        // 任务语句
    }
}
```

3. 创建你的子类的对象：

`Runnable r = new MyRunnable();`

4. 从 `runnable` 对象构造 `Thread` 对象：

`Thread t = new Thread(r);`

5. 调用方法启动线程：

`t.start();`

让我们来看一个具体的例子。我们想打印十次“Hello, World!”问候，每秒打印一次。我们在打印问候语时添加一个时间戳。

```
Fri Dec 28 23:12:03 PST 2012 Hello, World!
Fri Dec 28 23:12:04 PST 2012 Hello, World!
Fri Dec 28 23:12:05 PST 2012 Hello, World!
Fri Dec 28 23:12:06 PST 2012 Hello, World!
Fri Dec 28 23:12:07 PST 2012 Hello, World!
```

Fri Dec 28 23:12:09 PST 2012 Hello, World!

Fri Dec 28 23:12:10 PST 2012 Hello, World!
