
在列表 1 中，变量 `x` 的值除以变量 `y` 的值（0），这是不允许的并会导致程序中断。即使在程序语法上不正确的情况下，这种情况也会发生。图 1 显示了执行 `DemoException` 类时生成的异常：

![](img/d3faa73f55d3d314bb5bfb277886900d_223_0.png)

图 1：显示由 DemoException 类抛出的异常

图 1 显示了程序中断的原因，以便对其进行修复。在这里，你可以看到 `ArithmeticException`，它是当程序逻辑中出现数学计算相关问题时生成的。尽管显示了某些关于问题的信息，但你应该对异常、其类型以及抛出它们的原因有详细的了解。

Java 中有两种类型的错误：编译时错误和运行时错误。由于程序中的语法问题，在某些条件下（如内存故障）或内部错误，会发生运行时错误。

当异常发生时，会创建一个 `Exception` 类的实例对象，该对象包含有关异常的信息，例如异常的类型和异常发生时的程序状态。在创建对象后，它会在导致异常的方法中被抛出。Java 运行时系统会寻找异常处理技术来处理导致异常的异常。如果没有找到相应的异常处理技术，Java 运行时系统将在定义抛出异常方法的 Java 类中寻找异常处理技术。在任何情况下，如果没有处理异常的技术，Java 运行时系统将终止且程序中断。所有类型的异常都属于 `Exception` 类。图 2 了异常的层次结构，这将有助于你识别异常和错误：

![](img/d3faa73f55d3d314bb5bfb277886900d_224_0.png)

▲ 图 2：显示异常层次结构

图 2 显示 `Exception` 类是所有异常类的父类，而 `Error` 类是所有运行时错误类的子类。此外，`Exception` 和 `Error` 类都是 `Throwable` 类的子类。`Throwable` 类本身是所有 Java 类的父类 `Object` 类的子类。`Object` 类属于默认的 Java 包 `java.lang`，但这并不意味着所有异常都属于同一个包。例如，I/O 异常（如 `FileNotFoundException` 和 `EOFException`）属于 `java.io` 包中的 `Exception` 类。图 3 显示了 `Exception` 类的层次结构。

![](img/d3faa73f55d3d314bb5bfb277886900d_224_1.png)

▲ 图 3：显示 Exception 类的层次结构

图 3 显示了 `Exception` 类的两个子类，即 `RuntimeException` 类和 `ClassNotFoundException` 类。除了这些类，还有其他 `Exception` 类的子类，但为了简单起见，图 3 显示了 `Exception` 类的子类，即 `RuntimeException` 类和 `ClassNotFoundException` 类。除了这些类，还有 `Exception` 类的其他子类，但为了简单起见，图 3 显示了 `Exception` 类的子类。以下是 `Exception` 类的子类：

- `RuntimeException`：当发生运行时错误时抛出。
- `ClassNotFoundException`：当找不到类时抛出。
- `CloneNotSupportedException`：当未实现克隆时抛出。
- `IllegalAccessException`：当没有访问权限时抛出。
- `InstantiationException`：当尝试实例化抽象的类时抛出。
- `InterruptedException`：当线程处于睡眠或等待状态时抛出。
- `NullPointerException`：当类未定义时抛出。
- `NoSuchMethodException`：当方法未定义时抛出。

如所述，`RuntimeException` 类包含了其他子类，用于处理特定类型的异常。我们讨论这些子类。`RuntimeException` 的子类：

- `ArithmeticException`：当发生算术问题（如除以 0）时抛出。
- `IndexOutOfBoundsException`：当索引超出范围时抛出。
- `ArrayOutOfBoundsException`：当数组索引超出范围时抛出。
- `StringOutOfBoundsException`：当字符串超出范围时抛出。
- `ArrayStoreException`：当尝试向数组存储类型类型的值时抛出。
- `ClassCastException`：当类型转换不时不抛出。
- `IllegalArgumentException`：当向方法传递非法参数时抛出。
- `ThreadStateException`：当线程状态不时不抛出。
- `NumberFormatException`：当数值转换为字符串失败时。
- `IllegalStateException`：当运行时环境处于非法状态时抛出。
- `NegativeArraySizeException`：当尝试创建负数大小的数组时抛出。
- `NullPointerException`：当通过空引用访问对象时抛出。
- `SecurityException`：当方法违反 Java 定义的安全策略时抛出。

# 异常处理与 I/O 操作 213

你必须记住这些异常类及其子类，以及抛出特定异常的原因。这些信息有助于你处理异常。图 4 展示了 `Error` 类的层次结构：

![](img/d3faa73f55d3d314bb5bfb277886900d_226_0.png)

▲ 图 4：显示 Error 的层次结构

图 4 显示了 `Error` 类的两个子类 `LinkageError` 和 `VirtualMachineError`，这些子类进一步划分为它们的子类。除了 `LinkageError` 和 `VirtualMachineError` 子类，以下是 `Error` 类的子类列表：

- `LinkageError`：当链接类引用到另一个类时发生错误。该子类包含各种其他子类，如 `ClassFormatError`、`NoClassFoundError` 等。
- `VirtualMachineError`：当 Java 虚拟机 `JVM` 遇到错误时抛出。该子类包含各种其他子类，如 `InternalMemoryError` 等。
- `ThreadDeath`：当调用线程对象的 `stop()` 方法以杀死线程时抛出错误。
- `AssertionError`：当断言结果为假时抛出错误。

所有异常大致分为两类：受检查异常和未检查异常。在编译时检查的异常称为受检查异常，而未检查异常在编译时不进行检查。受检查异常是良好的程序可以捕获并通过提供异常发生的原因来通知异常。例如，`ArithmeticException` 通知用户

# 第 7 章

该异常由于算术计算错误。`Throwable` 类中的所有异常，属于 `Error` 和 `RuntimeException` 类及其子类的异常外，都是受检异常（checked exceptions）。
让我们在下一节讨论异常的类型。

## 探索异常类型

Java 用户可以处理其支持的异常。这些异常被称为内置异常（built-in exceptions）。除了这些内置异常，Java 还允许用户创建自己的异常并在 Java 程序中抛出，这些异常被称为自定义异常（user-defined exceptions）。在本节中，我们将通过以下子标题探索异常的类型：

- 内置异常
- 自定义异常
让我们逐一进行详细讨论。

## 内置异常

内置异常是 Java 中已经提供的异常。这些异常由 Java 运行时系统抛出以解释某种状态。内置异常进一步分为以下类型：

- 受检异常（Checked Exceptions）：受检异常是从 `Exception` 类继承的类，`RuntimeException` 类除外。受检异常必须使用隐式或显式的异常处理技术进行捕获。编译器能够在编译时检测受检异常。受检异常的一些示例包括 `ClassNotFoundException`、`CloneNotSupportedException` 和 `IllegalAccessException`。
- 未受检异常（Unchecked Exceptions）：未受检异常是从 `RuntimeException` 类继承的类。编译器在编译时无法检测未受检异常。这些异常不需要使用隐式或显式的异常处理技术进行捕获。未受检异常的一些示例包括 `ArrayIndexOutOfBoundsException`、`ArithmeticException` 和 `NullPointerException`。

表 1 解释了最常用的内置异常：

| 异常 | 描述 |
| --- | --- |
| ArithmeticException | 当 Java 运行时系统检测到算术运算时抛出。例如，当一个数除以 0 时会抛出此异常。 |
| ArrayIndexOutOfBoundsException | 当你尝试用非法索引访问数组时抛出。假设你声明了一个用于存储最多 5 个元素的数组，但在循环遍历时，你 own尝试访问第 6 个元素。在这种情况下，将抛出此异常。 |
| ClassNotFoundException | 当你尝试访问在 Java 程序中未定义的类时抛出。 |

| 表 1：Java 内置异常说明 |
| 异常 | 描述 |
| --- | --- |
| FileNotFoundException | 当你尝试访问不存在的文件或无法打开的文件时抛出。 |
| IOException | 当输入输出操作失败或中断时抛出。 |
| InterruptedException | 当线程在处理、等待或睡眠期间被中断时抛出。 |
| IllegalAccessException | 当对类的访问被拒绝时抛出。 |
| NoSuchFieldException | 当你尝试使用类中不可用的字段或变量时抛出。 |
| NoSuchMethodException | 当你尝试访问不存在的方法时抛出。 |
| NullPointerException | 当你引用空空对象的成员时抛出。 |
| NumberFormatException | 当你尝试将字符串转换为数字时抛出。 |
| StringIndexOutOfBoundsException | 当你尝试用非法索引访问字符串数组时抛出。 |

这些是最常见的内置异常。你可以使用这些异常处理来使你的程序更健壮。现在我们来讨论自定义异常。

- 自定义异常
我们知道 Java 提供了内置异常。然而，你也可以创建自己的异常类型，以你自己的方式描述应用程序中的异常。要创建自己的异常类型，你必须创建一个作为 `Exception` 类子类的异常类。要创建 `Exception` 类的子类，你必须继承 `Exception` 类。列表 2 显示了如何创建自己的异常类型（你可以在 CD|Code(Chapter2)文件夹中找到 `EnumNumException.java` 文件）：

- 列表 2：显示 `EnumNumException.java` 文件

```
package com.kogent;

class EnumNumException extends Exception {

    EnumNumException(String str) // 类的构造函数

{

        super(str); // 用于引用父类构造函数

    }

    public static void main(String[] args) {

        try {

            int arr[]={2,4,6,9};

            int var;

            int i;

            for(i=0;i<arr.length; i++) {

                var = arr[i]%2;

                if(var==0) {

                    System.out.println(arr[i]+"" is an even number");

                }

            }

        }
```

```
else {

    EvenNumException exp= new EvenNumException(arr[i]+
    "+"is not an even number");

    throw exp;

}

} catch(EvenNumException exp) {

    System.out.println("Exception is " + exp);

}
```

在列表 2 中，我们创建了 `EvenNumException` 类，它继承了 `Exception` 父类。然后我们为 `EvenNumException` 类创建一个构造函数，并在其中使用 `super` 关键字。在列表 2 中，我们首先在 `main` 方法中声明并初始化了一个数组。接下来，我们检查数组元素是否为偶数。然后，使用 `if` 语句，当数组除以 2 的值为 0 时。我们创建一个 `EvenNumException` 对象。接下来，我们使用 `throw` 子句，该子句用于数组除以 2 返回非 0 值的情况。在 `catch` 块中，我们处理了偶数异常。图 5 显示了 `EvenNumException` 的输出：

![](img/d3faa7f55d3d314bb5bf2778690d_229_0.png)

▲ 图 5：EvenNumException 的输出

图 5 显示了偶数。列表 2 中定义的异常在数组元素被除以 2 时抛出。让我们讨论 Java 中如何处理异常。

## 7.3 处理异常

在 Java 中，我们有诸如 `try` 和 `catch` 等各种处理技术。这些技术使用了 `try-catch` 块、`finally` 子句、`throws` 子句和 `throw` 子句。你可以使用这些技术创建设计良好的应用程序。异常处理在以下子标题下讨论：

- 使用 try 和 catch 块
- 使用嵌套的 try 和 catch 块
- 使用 finally 子句
- 使用 throws 子句
- 使用 throw 子句

让我们逐一进行详细讨论。

## 使用 try 和 catch 块

Java 程序中的 `try` 块用于封装可能导致异常的语句。`try` 块必须后跟一个 `catch` 块。`catch` 块充当异常处理器，包含指定异常类的对象，用于处理抛出的异常。当 Java 运行时系统调用异常处理器时，会执行 `catch` 块中的代码。图 6 显示了使用 `try-catch` 结构处理异常的流程结构。

![](img/d3faa7f55d3d314bb5bf2778690d_230_0.png)

▲ 图 6：显示 try-catch 结构的流程图

图 6 显示了在异常处理中使用 `try-catch` 结构的过程。当程序执行时，会检查其方法是否有错误，如果遇到任何错误，将搜索相应的异常处理技术。如果没有找到异常处理技术，程序将终止。然而，如果找到了异常处理技术，则执行编写在 `catch` 块中的代码。以下代码片段表示了 `try-catch` 结构的基本工作结构：

# 218 ► 第 7 章

```java
try {
    // 代码
} catch (exception_class var) {
    // 抛出异常时执行的代码
}
```

在前面的代码段中，`exception_class` 可以是任何异常相关的类或其子类，而 `var` 可以是任何引用存储异常详情的异常栈的变量名。使用 `try-catch` 结构的某些规则：

- `try` 块不能在没有 `catch` 块的情况下使用。
- `catch` 块后面必须跟 `try` 块，也就是说在 `try` 块结束处和 `catch` 块开始处没有语句。
- `finally` 块不能放在 `catch` 块之前。

列表 3 定义了 `DemoException_tc` 类，该类使用 `Exception` 类来处理抛出的异常（您可以在 CD 的 Code\Chapter7 文件夹下找到 `DemoException_tc.java` 文件）：

```java
package com.kogent;

public class DemoException_tc {
    public static void main(String args[]) {
        try {
            int x=5;
            int y=0;
            int z=x/y;
            System.out.println("Result of the program is " + z);
        } catch (Exception e) {
            e.printStackTrace();
            System.out.println("a number cannot be divided by zero ");
        }
    }
}
```
