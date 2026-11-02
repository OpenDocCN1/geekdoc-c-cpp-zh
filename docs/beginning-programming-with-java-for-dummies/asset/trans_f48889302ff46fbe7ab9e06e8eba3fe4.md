

## 第17章
## 使用对象和类进行编程
### 本章内容
- 使用类进行编程（并兼具风格与技巧）
- 从类创建对象
- 加入“我懂类和对象”的精英圈

第6、7、8章介绍了Java的原始类型——比如int、double、char和boolean。这很好，但现实世界中的问题有多少只涉及如此简单的值呢？想想商家和顾客之间的交易。顾客进行购买，这涉及商品名称、型号、信用卡信息、销售税率以及许多其他东西。

在较老的计算机编程语言中，你把整个购买过程当成一大堆未打包的衣物来处理。想象一堆袜子、衬衫和其他衣服。你没有篮子，所以只能尽量多拿。当你走向洗衣机时，会掉几样东西——这里掉一只袜子，那里掉一块抹布。这就像老式语言中存储购买值的方式。在较老的语言中，没有“购买”这个概念。只有double值、char值和其他零散的东西。你把购买金额放在一个变量中，顾客姓名放在另一个变量中，销售税数据放在其他地方。但这很糟糕。你很容易在通往编译器的路上掉东西。程序中只要有一点小错误，你就可能在这里丢掉一个金额，在那里丢掉一个顾客姓名。

因此，无论是洗衣服还是计算机编程，有篮子总是更好的。较新的编程语言（如Java）允许你组合各种值，创造出新的、更有用的值。例如，在Java中，你可以组合double值、boolean值以及其他类型的值，创建出一种称为“Purchase”（购买）的东西。因为你的购买信息全部打包在一起，跟踪购买的各个部分就更容易了。这就是一个重要的计算机编程概念——面向对象编程——的开端。

## 创建类

我先从一个“传统”的例子开始。清单17-1中的程序处理简单的购买数据。程序两次运行的结果如图17-1所示。

### 清单17-1：用老式方法完成

```java
import java.util.Scanner;

class ProcessData {

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        double amount;
        boolean taxable;
        double total;

        System.out.print("Amount: ");
        amount = keyboard.nextDouble();
        System.out.print("Taxable? (true/false) ");
        taxable = keyboard.nextBoolean();

        if (taxable) {
            total = amount * 1.05;
        } else {
            total = amount;
        }

        System.out.print("Total: ");
        System.out.println(total);

        keyboard.close();
    }
}
```

![](img/f938eba5f15e231d828a6255e7ec5523_349_0.png)

如果图17-1中的输出看起来有点奇怪，那是因为我没有在代码中控制小数点后的位数。所以在输出中，$20.00看起来像是20.0。没关系。我将在第18章告诉你如何解决这个问题。

## 引用类型和Java类

清单17-1中的代码涉及几个简单的值——amount、taxable和total。所以本章的重点是：通过组合几个简单的值，你可以得到一个单独的、更有用的值。就是这样运作的。你取一些Java的原始类型，把它们搅拌在一起做成一道原始类型炖菜，结果如何？你得到一种更有用的类型，称为引用类型。清单17-2中有一个例子。

### 清单17-2：成为Purchase意味着什么

```java
class Purchase {
    double amount;
    boolean taxable;
    double total;
}
```

清单17-2中的代码没有main方法，所以Eclipse可以编译这段代码，但你不能运行它。当你在Eclipse的主菜单中选择Run→Run As时，弹出的上下文菜单中没有Java Application条目。你可以点击Eclipse工具栏上的小Run As按钮，然后选择Java Application。但随后你会看到如图17-2所示的消息框。因为清单17-2没有main方法，就没有地方开始执行。（实际上，清单17-2中的代码根本没有任何语句。没有什么可执行的。）

图17-2：
清单17-2中的代码没有main方法。

![](img/f938eba5f15e231d828a6255e7ec5523_350_0.png)

## 使用新定义的类

要想用清单17-2中的代码做些有用的事情，你需要一个main方法。你可以把main方法放在另一个单独的文件中。清单17-3展示了这样一个文件。

### 清单17-3：使用你的Purchase类

```java
import java.util.Scanner;

class ProcessPurchase {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        Purchase onePurchase = new Purchase();

        System.out.print("Amount: ");
        onePurchase.amount = keyboard.nextDouble();
        System.out.print("Taxable? (true/false) ");
        onePurchase.taxable = keyboard.nextBoolean();

        if (onePurchase.taxable) {
            onePurchase.total = onePurchase.amount * 1.05;
        } else {
            onePurchase.total = onePurchase.amount;
        }

        System.out.print("Total: ");
        System.out.println(onePurchase.total);

        keyboard.close();
    }
}
```

理解清单17-3中代码的最佳方式，是把它与清单17-1中的代码逐行进行比较。实际上，有一个机械化的公式可以把清单17-1中的代码转换为清单17-3中的代码。表17-1描述了这个公式。

### 表17-1 将代码转换为使用类

| 清单17-1 | 清单17-3 |
|---|---|
| double amount; boolean taxable; double total; | Purchase onePurchase = new Purchase(); |
| amount | onePurchase.amount |
| taxable | onePurchase.taxable |
| total | onePurchase.total |

这两个程序（清单17-1和清单17-3）本质上做的是相同的事，但一个使用原始类型变量，另一个依赖于清单17-2中的Purchase代码。两个程序的运行结果都如图17-1所示。

## 从类到对象

清单17-2中的代码定义了一个类。类是设计方案；它描述了你打算如何组合和使用数据片段。例如，清单17-2中的代码声明了你打算组合double、boolean和double值来创建新的Purchase值。

类是所有Java编程的核心。但Java被称为面向对象的语言。Java并不叫面向类的语言。事实上，没有人使用“面向类的语言”这个术语。为什么？

嗯，你无法把类捧在手心里。类不是真实的。没有对象的类就像没有巧克力的日子。如果你现在正坐在一个房间里，看看房间里所有的椅子。房间里有几把椅子？两把？五把？二十把？在一个有五把椅子的房间里，你有五个椅子对象。每把椅子（每个对象）都是真实的东西，你可以使用的东西，你可以坐上去的东西。

像Java这样的语言有类和对象。那么类和对象之间有什么区别呢？

- 对象是具体的事物。
- 类是这类事物的设计方案。

例如，你会如何描述什么是椅子？嗯，椅子有座面、靠背和腿。在Java中，你可能会编写清单17-4中的内容。

### 清单17-4：成为椅子意味着什么

```java
/*
 * This is real Java code, but this code
 * cannot be compiled on its own:
 */

class Chair {
    FlatHorizontalPanel seat;
    FlatVerticalPanel back;
    LongSkinnyVerticalRods legs;
}
```

前面的代码是椅子的设计方案。代码告诉你每把椅子有三样东西。代码给这些东西命名（seat、back和legs），并告诉你每样东西的一些信息。（例如，座面是一个FlatHorizontalPanel。）同样，清单17-2中的代码告诉你每次购买有三样东西。代码给这些东西命名（amount、taxable和total），并告诉你每样东西的原始类型。

所以想象一个位于宇宙边缘的宏伟工厂。每晚当你入睡时，这个工厂会制造出有形的对象——你在接下来醒着的一天中会遇到的对象。明天你要去Sloshy Shoes公司面试。所以今晚，工厂为公司的办公室制造椅子。工厂根据清单17-4中几乎真实的代码制造椅子对象，如图17-3所示。

### 图17-3：来自Chair类的椅子对象。

![](img/f938eba5f15e231d828a6255e7ec5523_354_0.png)

在清单17-3中，这一行

```java
Purchase onePurchase = new Purchase();
```

表现得就像那个宇宙边缘的宏伟工厂。清单17-3中的这一行不是创建椅子对象，而是创建一个购买对象，如图17-4所示。清单17-3中的那一行是一个带初始化的声明。正如这行

```java
int count = 0;
```

声明了count变量并将count设置为0，清单17-3中的那一行声明了onePurchase变量并使onePurchase指向一个全新的对象。这个新对象包含三个部分：一个amount部分、一个taxable部分和一个total部分。

