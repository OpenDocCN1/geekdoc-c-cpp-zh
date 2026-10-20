

# 图 E.10 | 类 JButton 的构造函数详情部分。（Courtesy of Oracle Corporation）

方法详情会显示您可能感兴趣的其他方法（标记为 See Also）。如果方法重写了超类的方法，则会提供超类方法和超类名称，以便您可以链接到该方法或超类以获取更多信息。

构造函数详情部分描述每个构造函数

方法 read 抛出 IOException。单击 IOException 以加载 IOException 类信息页面并了解有关异常类型的更多信息（例如，为什么可能会抛出此类异常）

# 图 E.11 | 类 BufferedInputStream 的方法详情部分。（Courtesy of Oracle Corporation）

方法详情部分

方法 read 重写了 FilterInputStream 中的 read 方法。单击被重写方法名称以查看超类该方法版本的详细信息。

在浏览文档时，您会注意到经常有指向其他字段、方法、嵌套类和顶级类的链接。这些链接使您可以从正在查看的类跳转到文档的另一个相关部分。

# 使用调试器

> *And so shall I catch the fly.*
> —William Shakespeare

> *We are built to make mistakes, coded for error.*
> —Lewis Thomas

> *What we anticipate seldom occurs; what we least expect generally happens.*
> —Benjamin Disraeli

## Objectives

在本附录中您将学习：

- 设置断点以调试应用程序。
- 使用 `run` 命令通过调试器运行应用程序。
- 使用 `stop` 命令设置断点。
- 使用 `cont` 命令继续执行。
- 使用 `print` 命令计算表达式。
- 使用 `set` 命令在程序执行期间更改变量值。
- 使用 `step`、`step up` 和 `next` 命令控制执行。
- 使用 `watch` 命令查看字段在程序执行期间如何被修改。
- 使用 `clear` 命令列出断点或删除断点。

![](img/009e962758dcc71dbc43a493362e6dc0_1415_0.png)

## F.1 Introduction

在第 2 章中，您学习了有两种类型的错误——语法错误和逻辑错误，并且您学习了如何从代码中消除语法错误。逻辑错误不会阻止应用程序成功编译，但它们会导致应用程序运行时产生错误结果。JDK 包含名为调试器的软件，可让您监视应用程序的执行，以便您可以定位并删除逻辑错误。调试器将成为您最重要的应用程序开发工具之一。许多 IDE 提供了自己的调试器，类似于 JDK 中包含的调试器，或为 JDK 的调试器提供图形用户界面。

本附录使用不接收用户输入的命令行应用程序演示 JDK 调试器的关键功能。这里讨论的相同调试器功能可用于调试接收用户输入的应用程序，但调试此类应用程序需要稍复杂的设置。为了专注于调试器功能，我们选择使用不涉及用户输入的简单命令行应用程序来演示调试器。有关 Java 调试器的更多信息，请访问 download.oracle.com/javase/6/docs/technotes/tools/windows/jdb.html。

## F.2 Breakpoints and the run, stop, cont and print Commands

我们通过研究断点开始对调试器的研究，断点是可以在任何可执行代码行上设置的标记。当应用程序执行到达断点时，执行会暂停，让您可以检查变量的值以帮助确定是否存在逻辑错误。例如，您可以检查存储计算结果的变量的值，以确定计算是否正确执行。在不可执行行（如注释）上设置断点会导致调试器显示错误消息。

为了说明调试器的功能，我们使用应用程序 AccountTest（图 F.1），它创建并操作类 Account（图 3.13）的对象。AccountTest 的执行从 main 开始（第 7–24 行）。第 9 行使用初始余额 $50.00 创建一个 Account 对象。请记住，Account 的构造函数接受一个参数，指定 Account 的初始余额。第 12–13 行使用 Account 方法 getBalance 输出初始账户余额。第 15 行声明并初始化局部变量 depositAmount。然后第 17–19 行打印 depositAmount 并使用其 credit 方法将其添加到 Account 的余额中。最后，第 22–23 行显示新的余额。[注意：附录 F 示例目录包含与图 3.13 相同的 Account.java 副本。]

```
1  // Fig. F.1: AccountTest.java
2  // Create and manipulate an Account object.
3  
4  public class AccountTest
5  {
6      // main method begins execution
7      public static void main( String[] args )
8      {
9          Account account = new Account( 50.00 ); // create Account object
10 
11         // display initial balance of Account object
12         System.out.printf( "initial account balance: $%.2f\n",
13             account.getBalance() );
14 
15         double depositAmount = 25.0; // deposit amount
16 
17         System.out.printf( "\nadding %.2f to account balance\n\n",
18             depositAmount );
19         account.credit( depositAmount ); // add to account balance
20 
21         // display new balance
22         System.out.printf( "new account balance: $%.2f\n",
23             account.getBalance() );
24     } // end main
25 
26  } // end class AccountTest
```

initial account balance: $50.00
adding 25.00 to account balance
new account balance: $75.00

图 F.1 | AccountTest 类创建并操作 Account 对象。

在以下步骤中，您将使用断点和各种调试器命令检查 AccountTest（图 F.1）中声明的变量 depositAmount 的值。

1. 打开命令提示符窗口并更改目录。选择 开始 > 程序 > 附件 > 命令提示符 打开命令提示符窗口。通过键入 cd C:\examples\debugger 更改到包含附录 F 示例的目录 [注意：如果您的示例在不同目录中，请在此处使用该目录。]

2. 编译用于调试的应用程序。Java 调试器仅适用于使用 -g 编译器选项编译的 .class 文件，该选项生成调试器用于帮助您调试应用程序的信息。使用 -g 命令行选项编译应用程序，键入 javac -g AccountTest.java Account.java。请记住从第 3 章中，该命令同时编译 AccountTest.java 和 Account.java。命令 java -g *.java 为调试编译工作目录的所有 .java 文件。

3. 启动调试器。在命令提示符中，键入 jdb（图 F.2）。该命令将启动 Java 调试器并使您能够使用其功能。[注意：我们修改了命令提示符窗口的颜色以提高可读性。]

![](img/009e962758dcc71dbc43a493362e6dc0_1418_0.png)

图 F.2 | 启动 Java 调试器。

4. 在调试器中运行应用程序。通过调试器运行 AccountTest 应用程序，键入 run AccountTest（图 F.3）。如果在调试器中运行应用程序之前未设置任何断点，应用程序将像使用 java 命令一样运行。

![](img/009e962758dcc71dbc43a493362e6dc0_1418_1.png)

图 F.3 | 通过调试器运行 AccountTest 应用程序。

5. 重新启动调试器。为了正确使用调试器，您必须在运行应用程序之前设置至少一个断点。通过键入 jdb 重新启动调试器。

6. 在 Java 中插入断点。您可以在应用程序的特定代码行上设置断点。这些步骤中使用的行号来自图 F.1 中的源代码。通过键入 stop at AccountTest:12（图 F.4）在源代码的第 12 行设置断点。stop 命令在命令后指定的行号处插入断点。您可以设置任意数量的断点。通过键入 stop at AccountTest:19（图 F.4）再设置一个断点在第 19 行。当应用程序运行时，它会在包含断点的任何行处暂停执行。当调试器暂停应用程序的执行时，应用程序被认为处于中断模式。即使调试过程已经开始，也可以设置断点。调试器命令 stop in，后跟类名、句点和方法名（例如，stop in Account.credit）指示调试器在指定方法中的第一个可执行语句处设置断点。当程序控制进入该方法时，调试器会暂停执行。

- F.1 Introduction
- F.2 Breakpoints and the run, stop, cont and print Commands
- F.3 The print and set Commands
- F.4 Controlling Execution Using the step, step up and next Commands
- F.5 The watch Command
- F.6 The clear Command
- F.7 Wrap-Up

Self-Review Exercises | Answers to Self-Review Exercises

