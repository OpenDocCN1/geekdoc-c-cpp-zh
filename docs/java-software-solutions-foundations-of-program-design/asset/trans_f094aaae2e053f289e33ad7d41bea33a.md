

## 11.2 未捕获的异常

如果程序根本不处理异常，它将异常终止并产生一条消息，描述发生了什么异常以及它产生的位置。与异常关联的信息通常有助于追踪问题的原因。

让我们来看一下异常的输出。清单 11.1 中所示的程序在尝试无效的算术运算时会抛出 ArithmeticException。在这种情况下，程序尝试除以零。

由于该程序中没有代码显式处理异常，因此在发生异常时程序会终止，并打印有关异常的特定信息。请注意，程序中最后的 println 语句永远不会执行，因为异常先发生。

### LISTING 11.1

```
//****************************************************************
// Zero.java      Author: Lewis/Loftus
//
// Demonstrates an uncaught exception.
//****************************************************************

public class Zero
{
    //-------------------------------------------------------------
    // Deliberately divides by zero to produce an exception.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        int numerator = 10;
        int denominator = 0;

        System.out.println (numerator / denominator);

        System.out.println ("This text will not be printed.");
    }
}
```

### OUTPUT

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at Zero.main(Zero.java:17)
```

## KEY CONCEPT

抛出异常时打印的消息提供了方法调用栈跟踪。

异常输出的第一行指示抛出了哪个异常，并提供有关其抛出原因的一些信息。剩余的行是调用栈跟踪；它们指示异常发生的位置。在这种情况下，调用栈跟踪中只有一行，但根据异常的来源可能有几行。第一个跟踪行指示异常发生的 方法、文件和行号。如果存在其他跟踪行，则指示导致产生异常的方法所调用的方法。在此程序中，只有一个方法，并且它产生了异常；因此跟踪中只有一行。

调用栈跟踪信息也可以通过调用正在抛出的异常类的 方法来获得。方法 getMessage 返回一个解释异常抛出原因的字符串。方法 printStackTrace 打印调用栈跟踪。

### SELF-REVIEW QUESTION (see answer in Appendix N)

SR 11.3 True or False. Explain.

- a. An exception and an error are the same thing.
- b. An attempt to divide by zero will cause an exception to be thrown.
- c. If a program does not handle a raised exception, the exception is ignored and nothing happens.
- d. If a program does not handle an exception, a message related to the exception will be produced.
- e. A call stack trace shows the sequence of method calls that led to the code where an exception occurred.

## 11.3 The try-catch Statement

现在让我们检查在抛出异常时如何捕获和处理异常。try-catch 语句标识可能抛出异常的语句块。跟随 try 块的 catch 子句定义了如何处理特定类型的异常。一个 try 块可以与其关联多个 catch 子句。每个 catch 子句都是一个异常处理器。

当执行 try 语句时，try 块中的语句会被执行。如果在 try 块执行期间没有抛出异常，则处理将继续执行 try 语句之后 的语句（在所有 catch 子句之后）。这种情况是正常的执行流程，应该大部分时间发生。

如果在 try 块执行期间的任何时刻抛出异常，控制会立即转移到适当的 catch 处理程序（如果存在）。也就是说，控制转移到第一个其异常类与所抛出的异常相对应的 catch 子句。执行 catch 子句中的语句后，控制转移到整个 try-catch 语句之后的语句。

让我们看一个例子。假设一家假想的公司使用代码表示其各种产品。产品代码包括其他信息，其中第十位的一个字符代表该产品生产的区域，4 到 7 位的四位整数代表其将被销售的地区。由于某些重组，来自区域 R 的产品禁止在编号为 2000 或更高的地区销售。清单 11.2 中所示的程序从用户读取产品代码并计算输入的被禁代码的数量。

### KEY CONCEPT
每个 catch 子句处理 try 块中可能抛出的特定类型的异常。

### Try Statement

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_568_0.png)

try 语句包含一段代码，后跟一个或多个 catch 子句。如果在 try 块中发生异常，则执行相应的 catch 子句的代码。finally 子句（如果存在）无论 try 块如何退出都会被执行。

Example:

```
try
{
    System.out.println (Integer.parseInt(numString));
}
catch (NumberFormatException exception)
{
    System.out.println ("Caught an exception.");
}
finally
{
    System.out.println ("Done.");
}
```

```java
/**************************************************************
//  ProductCodes.java        Author: Lewis/Loftus
//
//  Demonstrates the use of a try-catch block.
/**************************************************************

import java.util.Scanner;

public class ProductCodes
{
    //-----------------------------------------------------------
    //  Counts the number of product codes that are entered with a
    //  zone of R and a district greater than 2000.
    //-----------------------------------------------------------
    public static void main (String[] args)
    {
        String code;
        char zone;
        int district, valid = 0, banned = 0;

        Scanner scan = new Scanner (System.in);

        System.out.print ("Enter product code (XXX to quit): ");
        code = scan.nextLine();

        while (!code.equals ("XXX"))
        {
            try
            {
                zone = code.charAt(0);
                district = Integer.parseInt(code.substring(3, 7));
                valid++;
                if (zone == 'R' && district > 2000)
                    banned++;
            }
            catch (StringIndexOutOfBoundsException exception)
            {
                System.out.println ("Improper code length: " + code);
            }
            catch (NumberFormatException exception)
            {
                System.out.println ("District is not numeric: " + code);
            }
        }
    }
}
```

### LISTING 11.2 continued

```
System.out.print ("Enter product code (XXX to quit): ");
code = scan.nextLine();
}

System.out.println ("# of valid codes entered: " + valid);
System.out.println ("# of banned codes entered: " + banned);
}
```

### OUTPUT

```
Enter product code (XXX to quit): TRV2475A5R-14
Enter product code (XXX to quit): TRD1704A7R-12
Enter product code (XXX to quit): TRL2k74A5R-11
District is not numeric: TRL2k74A5R-11
Enter product code (XXX to quit): TRQ2949A6M-04
Enter product code (XXX to quit): TRV2105A2
Improper code length: TRV2105A2
Enter product code (XXX to quit): TRQ2778A7R-19
Enter product code (XXX to quit): XXX
# of valid codes entered: 4
# of banned codes entered: 2
```

try 块中的编程语句尝试提取区域和地区信息，然后确定它是否代表被禁的产品代码。如果在提取区域和地区信息时出现任何问题，则产品代码被视为无效且不再进一步处理。例如，charAt 或 substring 方法可能会抛出 StringIndexOutOfBoundsException。此外，如果子字符串不包含有效整数，parseInt 方法可能会抛出 NumberFormatException。根据抛出的异常打印特定的消息。在任何一种情况下，由于异常被捕获并处理，因此处理会正常继续。

请注意，对于每个检查的代码，只有在没有抛出异常时，整数 valid 才会递增。如果抛出异常，控制会立即转移到适当的 catch 子句。同样，只有在没有抛出异常时，if 语句才会测试区域和地区。

