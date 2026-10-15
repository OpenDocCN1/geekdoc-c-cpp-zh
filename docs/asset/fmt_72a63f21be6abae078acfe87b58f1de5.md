
## 11.5 The Exception Class Hierarchy

The classes that define various exceptions are related by inheritance, creating a class hierarchy that is shown in part in Figure 11.1

The `Throwable` class is the parent of both the `Error` class and the `Exception` class. Many types of exceptions are derived from the `Exception` class, and these classes also have many children. Though these high-level classes are defined in the `java.lang` package, many child classes that define specific exceptions are part of several other packages. Inheritance relationships can span package boundaries.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_576_0.png)

FIGURE 11.1 Part of the Error and Exception class hierarchy

We can define our own exceptions by deriving a new class from `Exception` or one of its descendants. The class we choose as the parent depends on what situation or condition the new exception represents.

The program in Listing 11.5 instantiates an exception object and throws it. The exception is created from the `OutOfRangeException` class, which is shown in Listing 11.6. Note that this exception is not part of the Java standard class library. It was created to represent the situation in which a value is outside a particular valid range.

KEY CONCEPT
A new exception is defined by deriving a new class from the `Exception` class or one of its descendants.

### LISTING 11.5

```
//****************************************************************************
//  CreatingExceptions.java      Author: Lewis/Loftus
//
//  Demonstrates the ability to define an exception via inheritance.
//****************************************************************************

import java.util.Scanner;

public class CreatingExceptions
{
    //------------------------------------------------------------
    // Creates an exception object and possibly throws it.
    //------------------------------------------------------------
    public static void main (String[] args) throws OutOfRangeException
    {
        final int MIN = 25, MAX = 40;
        Scanner scan = new Scanner (System.in);

        OutOfRangeException problem =
            new OutOfRangeException ("Input value is out of range.");

        System.out.print ("Enter an integer value between " + MIN +
                          " and " + MAX + ", inclusive: ");
        int value = scan.nextInt();

        // Determine if the exception should be thrown
        if (value < MIN || value > MAX)
            throw problem;

        System.out.println ("End of main method.");  // may never reach
    }
}
```

### LISTING 11.5 继续

### 输出

```
Enter an integer value between 25 and 40, inclusive: 69

Exception in thread "main" OutOfRangeException:
    Input value is out of range.
    at CreatingExceptions.main(CreatingExceptions.java:20)
```

读取输入值后，`main`方法会对其进行评估，以查看其是否在有效范围内。如果不在，则执行`throw`语句。`throw`语句用于开始异常传播。由于`main`方法未捕获并处理异常，如果抛出异常，程序将终止，并打印与异常关联的消息。

我们通过扩展`Exception`类来创建`OutOfRangeException`类。通常，新的异常与本示例中看到的没有什么不同：

### LISTING 11.6

```
//****************************************************************
// OutOfRangeException.java      Author: Lewis/Loftus
//
// Represents an exceptional condition in which a value is out of
// some particular range.
//****************************************************************

public class OutOfRangeException extends Exception
{
    //-------------------------------------------------------------
    // Sets up the exception object with a particular message.
    //-------------------------------------------------------------
    OutOfRangeException (String message)
    {
        super (message);
    }
}
```

## 11.6 I/O 异常

处理输入和输出是一项经常会产生不可预见情况的任务，从而导致抛出异常。让我们探讨一些 I/O 问题以及可能出现的问题。

流是有序的字节序列。术语“流”源于这样的类比：当我们读写信息时，数据从源流向目的地（或汇），就像水流经溪流一样。信息的来源就像为溪流注水的泉眼，而目的地就像溪流流向的洞穴。

> 关键概念
> 流是字节的顺序序列；它可以用作输入的来源或输出的目的地。

在程序中，我们将流视为输入流，从中读取信息，或视为输出流，向其写入信息。也就是说，程序充当为流注水的泉眼或接收流的洞穴。程序可以同时处理多个输入和输出流。特定的数据存储，例如文件，可以作为程序的输入流或输出流，但通常不能同时兼任两者。

有三个流被称为标准 I/O 流。它们列在图 11.2 中。`System`类包含三个对象引用变量（`in`、`out`和`err`），代表三个标准 I/O 流。这些引用同时声明为 `public` 和 `static`，这使得它们可以通过`System`类直接访问。

> 关键概念
> `System`类中的三个 `public` 引用变量代表标准 I/O 流。

我们在本书的示例中一直在使用标准输出流，例如调用`System.out.println`。我们还使用标准输入流来创建`Scanner`对象，以便处理从用户交互式读取的输入。`Scanner`类以各种方式管理从标准输入流读取的输入，使我们的编程任务更轻松。它还会在内部处理各种 I/O 异常，并在需要时创建`InputMismatchException`。

默认情况下，标准 I/O 流代表特定的 I/O 设备。`System.in`通常代表键盘输入，而`System.out`和`System.err`通常代表显示器屏幕上的特定窗口。默认情况下，`System.out`和`System.err`流将输出写入同一窗口（通常是程序执行的窗口），尽管它们可以设置成写入不同的位置。`System.err`流通常用于发送错误消息。

| 标准 I/O 流 | 描述 |
|---|---|
| `System.in` | 标准输入流。 |
| `System.out` | 标准输出流。 |
| `System.err` | 标准错误流（错误消息的输出） |

图 11.2 标准 I/O 流

除了标准输入流之外，Java 标准类库的`java.io`包提供了许多类，让我们可以定义具有特定特征的流。一些类处理文件，其他类处理内存，还有一些类处理字符串。一些类假定它们处理的数据由字符组成，而另一些类假定数据由原始二进制信息字节组成。一些类提供了以某种方式操作流中数据的方法，例如缓冲信息或对其编号。通过以适当的方式组合类，我们可以创建代表具有我们为特定情况想要的确切特征的信息流的对象。

> 关键概念
> Java 类库包含许多用于定义具有各种特征的 I/O 流的类。

Java I/O 的广泛主题以及`java.io`包中类的 sheer 数量使得我们无法在本書中详细涵盖它。我们目前的重点是 I/O 异常。

I/O 类执行的许多操作都可能抛出`IOException`。`IOException`类是多个表示尝试执行 I/O 时出现问题的异常类的父类。

`IOException`是一个已检查异常。如本章前面所述，这意味着异常必须被捕获，或者所有传播它的方法都必须在其方法头部的`throws`子句中列出它。

由于 I/O 通常处理外部资源，尝试执行 I/O 操作的程序中可能出现许多问题。例如，我们想要读取的文件可能不存在；当我们尝试打开文件时，将抛出异常，因为找不到该文件。一般来说，我们应该尽量设计程序在处理潜在问题时尽可能健壮。

我们在之前的示例中已经看到如何使用`Scanner`类读取和处理从文本文件读取的输入。现在让我们探索一个将数据写入文本输出文件的示例。将输出写入文本文件只需要我们使用适当的类创建输出流，然后调用适当的方法写入数据。

假设我们想测试正在编写的程序，但没有可用的真实数据。我们可以编写一个程序来生成包含随机值的测试数据文件。Listing 11.7 所示的程序生成一个包含特定范围内随机整数值的文件。它还写入一行标准输出，确认数据文件已写入。

### LISTING 11.7

```
//************************************************************************
// TestData.java      Author: Lewis/Loftus
//
// Demonstrates I/O exceptions and the use of a character file
// output stream.
//************************************************************************

import java.util.Random;
import java.io.*;

public class TestData
{
    //-------------------------------------------------------------
    // Creates a file of test data that consists of ten lines each
    // containing ten integer values in the range 10 to 99.
    //-------------------------------------------------------------
    public static void main (String[] args) throws IOException
    {
        final int MAX = 10;
        int value;
        String file = "test.dat";

        Random rand = new Random();
        FileWriter fw = new FileWriter (file);
        BufferedWriter bw = new BufferedWriter (fw);
        PrintWriter outFile = new PrintWriter (bw);

        for (int line=1; line <= MAX; line++)
        {
            for (int num=1; num <= MAX; num++)
            {
                value = rand.nextInt (90) + 10;
                outFile.print (value + " ");
            }
            outFile.println ();
        }
    }
}
```

### LISTING 11.7 continued

```
outFile.close();
    System.out.println ("Output file has been created: " + file);

}
}
```
