

# 泛型类和方法

![](img/009e962758dcc71dbc43a493362e6dc0_910_0.png)

> 每个天才都以与同伴不同的角度看待世界。
> —Havelock Ellis

> …我们的特殊个性，与我们的普遍人性相区别。
> —Oliver Wendell Holmes, Sr.

> 生于一法，缚于另一法。
> —Lord Brooke

## Objectives

在本章中你将学习：

- 创建可对不同类型参数执行相同任务的泛型方法。
- 创建一个泛型 Stack 类，可用于存储任何类或接口类型的对象。
- 理解如何用非泛型方法或其它泛型方法重载泛型方法。
- 理解原始类型以及它们如何帮助实现向后兼容。
- 在方法体中不需要参数的精确类型信息时使用通配符。

# 21.1 Introduction

你在第 7 章和第 20 章中使用了现有的泛型方法和类。在本章中，你将学习如何编写自己的泛型方法。你还将学习泛型与其他 Java 特性，如重载和继承之间的关系。

如果我们能编写一个单一的 sort 方法来对 Integer 数组、String 数组或任何支持排序的类型（即其元素可比较）的数组进行排序，那就太好了。如果我们能编写一个单一的 Stack 类，可用作整数栈、浮点数栈、字符串栈或任何其它类型的栈，那就更好了。如果我们能在编译时检测类型不匹配——即编译时类型安全——那就更理想了。例如，如果一个 Stack 只存储整数，尝试将一个 String 压入该 Stack 应该在编译时报错。

本章讨论泛型，它提供了创建上述通用模型的方法。泛型方法使你能够用单一方法声明指定一组相关方法。泛型类（和接口）使你能够用单一类（或接口）声明指定一组相关类型。泛型还提供编译时类型安全，允许你在编译时捕获无效类型。

我们可能会为排序对象数组编写一个泛型方法，然后用 Integer 数组、Double 数组、String 数组等调用该泛型方法来排序数组元素。编译器可以执行类型检查以确保传递给排序方法的数组包含相同类型的元素。我们可能会编写一个单一的泛型 Stack 类来操作对象栈，然后为整数栈、Double 栈、String 栈等实例化 Stack 对象。编译器可以执行类型检查以确保 Stack 存储相同类型的元素。

> 软件工程观察 21.1
> 泛型方法和类是 Java 中实现具有编译时类型安全的软件重用的最强大功能之一。

# 21.2 Motivation for Generic Methods

重载方法常用于对不同类型的数据执行类似操作。为了说明泛型方法的动机，让我们从一个示例（图 21.1）开始，其中包含重载的 printArray 方法（第 21–28 行、第 31–38 行和第 41–48 行），分别打印 Integer 数组、Double 数组和 Character 数组元素的 String 表示。我们本可以使用原始类型 int、double 和 char 的数组。我们使用类型包装器类的数组来为我们的泛型方法示例做准备，因为只有引用类型才能与泛型方法和类一起使用。

- 21.1 Introduction
- 21.2 Motivation for Generic Methods
- 21.3 Generic Methods: Implementation and Compile-Time Translation
- 21.4 Additional Compile-Time Translation Issues: Methods That Use a Type Parameter as the Return Type
- 21.5 Overloading Generic Methods
- 21.6 Generic Classes
- 21.7 Raw Types
- 21.8 Wildcards in Methods That Accept Type Parameters
- 21.9 Generics and Inheritance: Notes
- 21.10 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

```
// Fig. 21.1: OverloadedMethods.java
// Printing array elements using overloaded methods.
public class OverloadedMethods
{
    public static void main( String[] args )
    {
        // create arrays of Integer, Double and Character
        Integer[] integerArray = { 1, 2, 3, 4, 5, 6 };
        Double[] doubleArray = { 1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7 };
        Character[] characterArray = { 'H', 'E', 'L', 'L', 'O' };

        System.out.println( "Array integerArray contains:" );
        printArray( integerArray ); // pass an Integer array
        System.out.println( "\nArray doubleArray contains:" );
        printArray( doubleArray ); // pass a Double array
        System.out.println( "\nArray characterArray contains:" );
        printArray( characterArray ); // pass a Character array
    } // end main

    // method printArray to print Integer array
    public static void printArray( Integer[] inputArray )
    {
        // display array elements
        for ( Integer element : inputArray )
            System.out.printf( "%s ", element );

        System.out.println();
    } // end method printArray

    // method printArray to print Double array
    public static void printArray( Double[] inputArray )
    {
        // display array elements
        for ( Double element : inputArray )
            System.out.printf( "%s ", element );

        System.out.println();
    } // end method printArray

    // method printArray to print Character array
    public static void printArray( Character[] inputArray )
    {
        // display array elements
        for ( Character element : inputArray )
            System.out.printf( "%s ", element );

        System.out.println();
    } // end method printArray
} // end class OverloadedMethods
```

![](img/009e962758dcc71dbc43a493362e6dc0_913_0.png)

程序首先声明并初始化三个数组——六元素 Integer 数组 integerArray（第 8 行）、七元素 Double 数组 doubleArray（第 9 行）和五元素 Character 数组 characterArray（第 10 行）。然后第 12–17 行显示每个数组的内容。

当编译器遇到方法调用时，它会尝试查找具有相同名称且参数与调用中的参数类型匹配的方法声明。在本例中，每个 printArray 调用都匹配其中一个 printArray 方法声明。例如，第 13 行用 integerArray 作为参数调用 printArray。编译器确定参数的类型（即 Integer[]）并尝试查找指定 Integer[] 参数的 printArray 方法（第 21–28 行），然后设置对该方法的调用。类似地，当编译器遇到第 15 行的调用时，它确定参数的类型（即 Double[]），然后尝试查找指定 Double[] 参数的 printArray 方法（第 31–38 行），然后设置对该方法的调用。最后，当编译器遇到第 17 行的调用时，它确定参数的类型（即 Character[]），然后尝试查找指定 Character[] 参数的 printArray 方法（第 41–48 行），然后设置对该方法的调用。

研究每个 printArray 方法。数组元素类型出现在每个方法的头（第 21、31 和 41 行）和 for 语句头（第 24、34 和 44 行）中。如果我们将每个方法中的元素类型替换为泛型名称——按惯例为 T——那么这三个方法看起来都像图 21.2 中的方法。看起来如果我们能用单一泛型类型替换这三个方法中的数组元素类型，那么我们应该能够声明一个 printArray 方法来显示包含对象的任何数组元素的 String 表示。图 21.2 中的方法与我们在第 21.3 节中讨论的泛型 printArray 方法声明类似。

```java
public static void printArray( T[] inputArray )
{
    // display array elements
    for ( T element : inputArray )
        System.out.printf( "%s", element );

    System.out.println();
} // end method printArray
```

