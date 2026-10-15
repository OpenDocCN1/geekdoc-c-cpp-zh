

表达式 height[8] 指的是存储在特定内存位置的一个整数。它可以在任何可以使用整数变量的地方使用。因此你可以为其赋值、在计算中使用它、打印其值等等。此外，由于数组索引是整数，因此你可以使用整数表达式来指定用于访问数组的索引。这些概念在以下代码行中得以演示：

```
height[2] = 72;
height[count] = feet * 12;
average = (height[0] + height[1] + height[2]) / 3;
System.out.println ("The middle value is " + height[MAX/2]);
pick = height[rand.nextInt(11)];
```

数组在内存中是连续存储的，这意味着元素在内存中一个接一个地存储，就像我们在概念上想象的那样。这使得通过索引访问数组中的任何特定元素变得极其高效。内部确定任何特定元素的地址时，索引会乘以每个元素的大小，然后加上数组起始点的内存地址。这就是为什么数组索引从零开始而不是从一开始——为了使该计算尽可能简单。因此从效率角度来看，访问数组中第 500 个元素与访问第一个元素一样容易。

## 自我复习问题（答案见附录 N）

+ SR 8.1 什么是数组？
+ SR 8.2 如何引用数组的每个元素？
+ SR 8.3 基于图 8.1 所示的数组，以下各值是什么？
+ a. height[1]
+ b. height[2] + height[5]
+ c. height[2 + 5]
+ d. 索引 8 处存储的值
+ e. 第四个值
+ f. height.length

## 8.2 声明和使用数组

在 Java 中，数组是对象。要创建数组，必须声明对数组的引用。然后可以使用 new 操作符实例化数组，该操作符分配内存空间来存储值。以下代码表示图 8.1 所示数组的声明：

```
int[] height = new int[11];
```

变量 `height` 被声明为整数数组，其类型写为 `int[]`。存储在数组中的所有值具有相同的类型（或至少兼容）。例如，我们可以创建一个可以容纳整数的数组，也可以创建一个可以容纳字符串的数组，但不能创建一个可以同时容纳整数和字符串的数组。数组可以设置为保存任何原始类型或任何对象（类）类型。存储在数组中的值有时称为 *数组元素*，而数组保存的值的类型称为数组的 *元素类型*。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_409_0.png)

### LISTING 8.1

```java
//***********************************************
//  BasicArray.java          Author: Lewis/Loftus
//
//  Demonstrates basic array declaration and use.
//***********************************************

public class BasicArray
{
   //---------------------------------------------
   //  Creates an array, fills it with various integer values,
   //  modifies one value, then prints them out.
   //---------------------------------------------
   public static void main (String[] args)
   {
      final int LIMIT = 15, MULTIPLE = 10;

      int[] list = new int[LIMIT];

      // Initialize the array values
      for (int index = 0; index < LIMIT; index++)
         list[index] = index * MULTIPLE;

      list[5] = 999;  // change one array value

      // Print the array values
      for (int value : list)
         System.out.print (value + " ");
   }
}
```

### OUTPUT

0  10  20  30  40  999  60  70  80  90  100  110  120  130  140

请注意，数组变量的类型（int[]）不包括数组的大小。使用 new 操作符实例化 height 会保留存储 11 个整数的内存空间，索引从 0 到 10。一旦数组被声明为特定大小，它所能容纳的值的数量就不能更改。

清单 8.1 中显示的示例创建了一个名为 list 的数组，可以容纳 15 个整数，并用 10 的递增序列填充它。然后它更改数组中第六个元素（索引为 5）的值。最后，它打印数组中存储的所有值。

图 8.2 显示了在 BasicArray 程序执行期间数组的变化。使用 for 循环处理数组时通常很方便，因为数组中的位置数量是恒定的。请注意，BasicArray 程序中在多个地方使用了名为 LIMIT 的常量。此常量用于声明数组的大小并控制初始化数组值的 for 循环。

迭代器版本的 for 循环用于打印数组中的值。回想一下第 5 章中，这个版本的 for 循环提取迭代器中的每个值。

VideoNote
数组概述。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_410_0.png)

### FIGURE 8.2 The array list as it changes in the BasicArray program

指定的迭代器。每个 Java 数组都是一个迭代器，因此这种类型的循环可以在我们想要处理数组中存储的每个元素时使用。

用于指示数组索引的方括号在 Java 中被视为运算符。因此，就像 + 运算符或 <= 运算符一样，索引运算符（[]）相对于其他 Java 运算符具有优先级，决定了它的执行时间。它是所有 Java 运算符中优先级最高的。

## 边界检查

索引运算符执行自动边界检查，确保索引在被引用的数组范围内。每当对数组元素进行引用时，索引必须大于或等于零且小于数组的大小。例如，假设创建了一个名为 prices 的数组，包含 25 个元素。该数组的有效索引从 0 到 24。每当对数组中的特定元素进行引用时（如 prices[count]），索引的值就会被检查。如果它在数组的有效索引范围内（0 到 24），则会执行引用。如果索引无效，则会抛出名为 ArrayIndexOutOfBoundsException 的异常。

KEY CONCEPT
边界检查确保用于引用数组元素的索引在范围内。

当然，在我们的程序中，我们希望执行自己的边界检查。也就是说，我们希望小心地保持在数组的边界内并处理我们打算处理的每个元素。由于数组索引从零开始到小于数组大小，因此很容易在程序中创建差一错误，即处理除一个元素之外的所有元素或尝试索引多一个元素的问题。

检查数组边界的一种方法是使用 length 常量，该常量存储在数组对象中并存储数组的大小。它是公共常量，因此可以直接引用。例如，在创建包含 25 个元素的数组 prices 之后，常量 prices.length 包含值 25。它的值在数组首次创建时设置一次且不能更改。length 常量是每个数组不可分割的一部分，可以在需要数组大小时使用，而无需创建单独的常量。请记住，数组的长度是它可以容纳的元素数量，因此数组的最大索引是 length-1。

让我们再看一个例子。清单 8.2 中显示的程序读取 10 个整数到名为 numbers 的数组中，然后以相反的顺序打印它们。

请注意，在 ReverseOrder 程序中，数组 numbers 被声明为有 10 个元素，因此索引从 0 到 9。通过使用数组对象的 length 字段来控制 for 循环中的索引范围。你应该仔细设置循环控制变量的初始值和终止循环的条件，以保证处理所有预期元素并且仅使用有效索引来引用数组元素。

```java
//**********************************************************************
// ReverseOrder.java     Author: Lewis/Loftus
// Demonstrates array index processing.
//**********************************************************************
import java.util.Scanner;

public class ReverseOrder
{
    //-----------------------------------------------------------
    // Reads a list of numbers from the user, storing them in an
    // array, then prints them in the opposite order.
    //-----------------------------------------------------------
    public static void main (String[] args)
    {
        Scanner scan = new Scanner (System.in);
        double[] numbers = new double[10];
        System.out.println ("The size of the array: " + numbers.length);
        for (int index = 0; index < numbers.length; index++)
        {
            System.out.print ("Enter number " + (index+1) + ": ");
            numbers[index] = scan.nextDouble();
        }
        System.out.println ("The numbers in reverse order:");
        for (int index = numbers.length-1; index >= 0; index--)
            System.out.print (numbers[index] + " ");
    }
}
```

The size of the array: 10
Enter number 1: 18.36
Enter number 2: 48.9
Enter number 3: 53.5
Enter number 4: 29.06

