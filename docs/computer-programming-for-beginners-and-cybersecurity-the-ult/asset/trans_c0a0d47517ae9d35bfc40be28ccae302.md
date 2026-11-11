

```java
for(int i=0; i<5; i++) {
    System.out.print(numberArray[i]);
    System.out.print(", ");
}
System.out.print("\n");
}
}
```

### While 循环实现

```java
public class whileDemo {
    public static void main(String args[]) {
        int [] numberArray = {100, 300, 500, 700, 900};
        int i = 0;
        while(i<5) {
            System.out.print(numberArray[i]);
            System.out.print(", ");
            i++;
        }
        System.out.print("\n");
    }
}
```

### Do While 循环实现

```java
public class doWhileDemo {
    public static void main(String args[]) {
        int [] numberArray = {100, 300, 500, 700, 900};
        int i = 0;
        do {
            System.out.print(numberArray[i]);
            System.out.print(",");
            i++;
        } while (i<5);
        System.out.print("\n");
    }
}
```

### 增强型 For 循环

Java 还支持一种增强型循环结构，可用于数组元素。此循环结构的语法如下——

```java
for(declaration : expression) {
/*Body*/
}
```

增强型 for 循环的声明部分用于声明一个变量。该变量应当是“for 循环”的局部变量，并且其类型必须与数组元素的类型相同。该变量的当前值始终等于循环中正在遍历的数组元素。表达式是一个数组或返回数组的方法调用。

增强型 for 循环的示例实现如下 -

```java
public class forArrayDemo {
    public static void main(String args[]) {
        int [] numberArray = {100, 300, 500, 700, 900};
        for(int i : numberArray ) {
            System.out.print( i );
            System.out.print(",");
        }
        System.out.print("\n");
    }
}
```

### 异常层次结构

Java 有一个名为 java.lang.Exception 的内置类，所有异常都属于这个类。所有异常类都是此类的子类。此外，Throwable 类是异常类的超类。Throwable 类的另一个子类是 Error 类。上述的栈溢出等所有错误都属于这个 Error 类。

Exception 类有两个子类，即 RuntimeException 类和 IOException 类。下面列出了作为 Throwable 类的一部分、在 Java 中提供定义的方法。

```java
public String getMessage()
```

调用时，此方法返回已遇到异常的详细描述。

```java
public Throwable getCause()
```

调用此方法时，它返回一条包含异常原因的消息。

```java
public String toString()
```

此方法返回异常的详细描述，并与类名拼接在一起。

```java
public void printStackTrace()
```

调用此方法可以将 toString() 的结果连同堆栈跟踪打印到标准错误流 System.err。

```java
public StackTraceElement [] getStackTrace()
```

在某些场景下，你可能需要访问堆栈跟踪的不同元素。此方法返回一个数组，堆栈跟踪的每个元素分别保存到数组的不同元素中。数组的第一个元素包含堆栈跟踪的顶部元素，而堆栈跟踪的底部保存在数组的最后一个元素中。

```java
public Throwable fillInStackTrace()
```

将堆栈跟踪中的先前信息与堆栈跟踪的当前内容追加在一起，并以数组形式返回。

### 捕获异常

捕获异常的标准方法是使用“try 和 catch”关键字及其代码实现。try 和 catch 块应当以包含预期会引发异常的代码的方式实现。这里还需要说明的是，预期会引发异常的代码被称为受保护代码。try 和 catch 块实现的语法如下——

```java
try {
    /*Protected code*/
} catch(ExceptionName exc1) {
    /*Catch code*/
}
```

预期会引发异常的代码放在 try 块内。如果引发异常，则在 catch 块中实现为处理异常而执行的相应操作。每个 try 块都必须有 catch 块或 finally 块。

作为 catch 语句的一部分，需要声明预期会引发的异常。如果发生异常，执行将转移到 catch 块。如果引发的异常与 catch 块中定义的异常匹配，则执行该 catch 块。

try 和 catch 块的示例实现如下。该代码实现了一个包含 2 个元素的数组。但是，代码试图访问不存在的第三个元素。结果引发异常。

```java
import java.io.*;

public class demoException {
    public static void main(String args[]) {
        try {
            int arr[] = new int[2];
            System.out.println("Accessing the 3rd element of the array:" + arr[3]);
        } catch(ArrayIndexOutOfBoundsException exp) {
            System.out.println("Catching Exception:" + exp);
        }
        System.out.println("Reached outside catch block");
    }
}
```

### 实现多个 Catch 块

一个代码块可能导致多个异常。为了满足此需求，也允许实现多个 catch 块。此类实现的语法如下。

```java
try {
    /*Protected Code*/
} catch(ExpType1 exp1) {
    /*Catch block 1*/
} catch(ExpType2 exp2) {
    /*Catch block 2*/
} catch(ExpType3 exp3) {
    /*Catch block 3*/
}
```

上述语法展示了三个 catch 块的实现。但是，你可以实现任意数量的 catch 块。当执行此代码时，会执行受保护代码。如果发生异常，则将异常类型与第一个 catch 块的异常进行匹配。但是，如果异常类型不匹配，则忽略 catch 块 1，并尝试匹配第二个 catch 块的异常类型。哪个 catch 块与所引发异常的类型相同，就执行相应的 catch 块。

## 第 9 章：ADT、数据结构和 Java 集合

### 抽象数据类型（ADT）

抽象数据类型（ADT）是对数据以及允许对其执行的操作的逻辑描述。ADT 被定义为从用户视角对数据的描述。ADT 关注数据的可能取值及其对外暴露的接口。ADT 不关注数据结构的实际实现。

例如，用户想要存储一些整数并求其平均值。此数据结构的 ADT 将支持两个函数：一个用于添加整数，另一个用于获取平均值。此数据结构的 ADT 不讨论它究竟将如何实现。

![](img/ecb1bfa35f80f656f92811abb43b3df7_171_0.png)

### 数据结构

数据结构是数据的具体表示，并被定义为从程序员视角对数据的描述。数据结构表示数据将如何存储在内存中。所有数据结构都有各自的优缺点。根据问题的类型，我们选择最适合该问题的数据结构。例如，我们可以将数据存储在数组、链表、栈、队列、树等中。

注意：在本章中，我们将学习各种数据结构及其 API。以便用户无需了解其内部实现即可使用它们。

### Java 集合框架

Java 编程语言提供了 Java 集合框架，它是一组高质量、高性能且可复用的数据结构和算法。

![](img/ecb1bfa35f80f656f92811abb43b3df7_172_0.png)

使用 Java 集合框架具有以下优点：

- 1. 程序员不必重复实现基本数据结构和算法。从而避免重复造轮子。因此，程序员可以将更多精力投入到业务逻辑中。
- 2. Java 集合框架代码是经过充分测试的高质量、高性能代码。使用它们可以提高程序质量。
- 3. 由于集合框架中实现的基本数据结构和算法可被复用，因此降低了开发成本。
- 4. 由于大多数 Java 开发者使用集合框架，因此易于审查和理解其他开发者编写的程序。此外，集合框架文档完善。

