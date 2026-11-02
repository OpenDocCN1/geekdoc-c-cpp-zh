
Java 会根据你计算机的区域设置来塑造其输入和输出。例如，假设你的计算机运行的是在法国销售的 Windows 版本。那么就 Java 而言，你计算机的区域设置是 Locale.FRANCE，而清单 18-7 中代码的运行情况看起来像图 18-11 所示。

**图 18-11：** 清单 18-7 在法国计算机上的运行。

![](img/6d9dcff12e52b997f3ad31445b712549_379_0.png)

事实上，你可以为许多国家/地区自定义代码，而且不必为此买飞机票！我的计算机配置为在美国运行。但在清单 18-8 中，我使用 Java 的 Locale 类来获得图 18-11 所示的运行结果。

**清单 18-8：使用 Java 本地化**

```java
import java.text.NumberFormat;
import java.util.Locale;
import java.util.Scanner;

class MieuxTraiterLesDonnées {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        keyboard.useLocale(Locale.FRANCE);

        double amount;
        boolean taxable;
        double total;
        NumberFormat currency = NumberFormat.
            getCurrencyInstance(Locale.FRANCE);
        String niceTotal;

        System.out.print("Amount: ");
        amount = keyboard.nextDouble();
        System.out.print("Taxable? (true/false) ");
        taxable = keyboard.nextBoolean();

        if (taxable) {
            total = amount * 1.05;
        } else {
            total = amount;
        }

        niceTotal = currency.format(total);
        System.out.print("Total: ");
        System.out.println(niceTotal);
        keyboard.close();
    }
}
```

## 理解整体大局

在本节中，我回答了我在整本书中提出的某些迫切问题。"java.util 代表什么？" "为什么在代码的某些地方需要 static 这个词？" "园艺学学位如何帮助你整理已作废的支票？"

我还以一些独特而有趣的方式解释 "static"。毕竟，静态方法和变量并不容易理解。从几个角度阅读有关 Java 静态特性的内容会有所帮助。

### 包和 import 声明

在 Java 中，你可以将一堆类分组到称为包的东西中。事实上，Java 标准 API 中的类被分为大约 200 个包。本书的示例大量使用了三个包——名为 java.util、java.lang 和 java.io 的包。

### 类 java.util.Scanner

包 java.util 包含大约 50 个类，包括非常有用的 Scanner 类。与大多数其他类一样，这个 Scanner 类有两个名称——完全限定名和简化的简单名。该类的完全限定名是 java.util.Scanner，而该类的简单名是 Scanner。你可以通过将包名添加到类的简单名来获得完全限定名。（也就是说，你将包名 java.util 添加到简单名 Scanner。你得到 java.util.Scanner。）

import 声明让你可以缩写类的名称。声明如下

```
import java.util.Scanner;
```

Java 编译器会据此确定在何处查找 Scanner 类。因此，你不必在代码中到处写 java.util.Scanner，只需写 Scanner 即可。

### 类 `java.lang.System`

包 `java.lang` 包含大约 35 个类，包括备受欢迎的 `System` 类。（该类的完全限定名是 `java.lang.System`，而该类的简单名是 `System`。）不必在代码中到处写 `java.lang.System`，只需写 `System` 即可。你甚至不需要一个 `import` 声明。

在 Java 的所有包中，`java.lang` 包是特殊的。有无 import 声明，编译器都会导入 `java.lang` 包中的所有内容。你可以用 `import java.lang.System` 开始程序。但如果你不这样做，编译器会自动添加此声明。

![](img/6d9dcff12e52b997f3ad31445b712549_381_0.png)

### 静态 `System.out` 变量

为了缩写 `System.out.println`，你必须做哪种导入？如何将其缩短为 `out.println`？import 声明让你可以缩写类的名称。但在表达式 `System.out` 中，单词 `out` 并不是一个类。单词 `out` 是一个静态变量。（`out` 变量指的是 Java 程序发送文本输出的位置。）因此你不能写

```java
//This code is bogus. Don't use it:
import java.lang.System.out;
```

那你该怎么做呢？你写

```java
import static java.lang.System.out;
```

要了解有关 `out` 变量是静态变量的更多信息，请阅读下一节。

### 你需要知道的一切

我可以用几句话概括 Java 的大部分复杂性。

- Java API 包含许多包。
- 一个包包含类。
- 从一个类，你可以创建对象。
- 一个对象可以有自己的方法。对象也可以有自己的变量。
- 一个类可以有自己的静态方法。类也可以有自己的静态变量。

## 拨开静态的黑暗

我喜欢引用我自己。当我引用自己的话时，我不需要书面许可。我不必考虑版权侵权，也永远不会接到律师的电话。最重要的是，我可以改变和歪曲我说的任何内容。当我转述自己的想法时，就不会被断章取义。

考虑到这一点，这里是上一节中的一段引文：

> "Anything that's static belongs to a whole class, not to any particular instance of the class. . . To call a static method, you use a class's name along with a dot."

多么深刻啊！在清单 18-6 中，我介绍了一个名为 parseInt 的静态方法。以下是同一引文应用于静态 parseInt 方法：

> The static parseInt method belongs to the whole Integer class, not to any particular instance of the Integer class. . . To call the static parseInt method, you use the Integer class's name along with a dot. You write something like Integer.parseInt(reply).

很不错！那我在第 3 章中介绍的 System.out 业务呢？我也可以将我的引文应用到那上面。

> The static out variable belongs to the whole System class, not to any particular instance of the System class. . . To refer to the static out variable, you use the System class's name along with a dot. You write something like System.out.println().

如果你思考 System.out 的含义，这个静态的事情就说得通了。毕竟，名称 System.out 指的是 Java 程序发送文本输出的位置。（当你使用 Eclipse 时，名称 System.out 指的是 Eclipse 的 Console 视图。）典型的程序只有一个地方发送其文本输出。因此 Java 程序只有一个 out 变量。不管你创建多少个对象——三个、十个或零个——你只有一个 out 变量。而当你将某物设为静态时，你确保程序只有一个这样的东西。

好吧！那么 out 变量就是静态的。

要缩写静态变量（或静态方法）的名称，你不使用普通的 import 声明。相反，你使用静态 import 声明。这就是为什么在第 9 章及以后，我使用 static 这个词来导入 out 变量：

```java
import static java.lang.System.out;
```

## Barry 兑现了一个古老的承诺

在第 6 章中，我将变量声明移出 main 方法。我从清单 18-9 中的代码转变为清单 18-10 中的代码。

**清单 18-9：在 main 方法内部声明变量**

```java
class SnitSoft {
    public static void main(String args[]) {
        double amount = 5.95;
        amount = amount + 25.00;
        System.out.println(amount);
    }
}
```

**清单 18-10：将变量移出 main 方法之外**

```java
class SnitSoft {
    static double amount = 5.95;
    public static void main(String args[]) {
        amount = amount + 25.00;
        System.out.println(amount);
    }
}
```

在第 6 章中，我承诺解释为什么清单 18-10 需要额外的单词 static（在 static double amount = 5.95 中）。好吧，有了本章关于静态方法的种种讨论，我终于可以解释一切了。

参考图 18-7。在该图中，你有支票，还有一个 sort 方法。每张单独的支票都有自己的号码、金额和收款人。但整个 Check 类只有一个 sort 方法。

我不知道你是否如此，但为了整理我的已作废支票，我把它们挂在我的异国情调的 Yucca Elephantipes 树上。我把号码较高的支票固定在上部的叶子上，把号码较低的支票放在下部的叶子上。当我找到一张号码介于另外两张支票之间的支票时，我会选择一片空闲的叶子（一片位于上部和下部叶子之间的叶子）。
