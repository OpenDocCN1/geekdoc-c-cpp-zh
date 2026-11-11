
允许在最后一个值后面加逗号，这对于需要随时间不断添加值的数组来说很方便：

```
    String[] authors = {
       "James Gosling",
       "Bill Joy",
       "Guy Steele",
       // add more names here and put a comma after each name
    };
```

可以声明一个*匿名数组*：

```
    new int[] { 17, 19, 23, 29, 31, 37 }
```

该表达式分配一个新数组，并用花括号内的值填充它。它会计算初始值的数量并相应设置数组大小。你可以使用此语法在不创建新变量的情况下重新初始化数组。例如，

```
    smallPrimes = new int[] { 17, 19, 23, 29, 31, 37 };
```

是以下写法的简写：

```
    int[] anonymous = { 17, 19, 23, 29, 31, 37 };
    smallPrimes = anonymous;
```

> **注意：** 允许使用长度为 0 的数组。如果你编写一个计算数组结果的方法，而结果恰好为空，这样的数组会很有用。可以这样构造一个长度为 0 的数组：
>
> `new elementType[0]`
>
> 或者
>
> `new elementType[] { }`
>
> 注意，长度为 0 的数组与 `null` 不同。

### 3.10.2 访问数组元素

数组元素是*从 0 到 99 编号*的（而不是 1 到 100）。数组创建后，可以填充数组中的元素，例如使用循环：

```
    int[] a = new int[100];
    for (int i = 0; i < 100; i++)
        a[i] = i; // fills the array with numbers 0 to 99
```

当创建数字数组时，所有元素都初始化为零。布尔数组初始化为 `false`。对象数组初始化为特殊值 null，表示它们（尚）不包含任何对象。这对初学者来说可能令人惊讶。例如，

```java
String[] names = new String[10];
```

创建一个包含十个字符串的数组，所有这些字符串都是 null。如果你希望数组包含空字符串，则必须提供它们：

```java
for (int i = 0; i < 10; i++) names[i] = "";
```

> **警告：** 如果构造一个包含 100 个元素的数组，然后尝试访问元素 a[100]（或 0 到 99 范围之外的任何其他索引），将会发生“数组索引越界”异常。

要查找数组的元素个数，请使用 `array.length`。例如：

```java
for (int i = 0; i < a.length; i++)
    System.out.println(a[i]);
```

### 3.10.3 “for each”循环

Java 有一种强大的循环结构，允许你遍历数组（或任何其他元素集合）中的每个元素，而无需费心处理索引值。

*增强的 for 循环*

```java
for (variable : collection) statement
```

将给定变量设置为集合中的每个元素，然后执行语句（当然，该语句可能是一个块）。*集合表达式*必须是数组或实现了 Iterable 接口的类的对象，例如 ArrayList。我们将在第 5 章讨论数组列表，在第 9 章讨论 Iterable 接口。

例如，

```java
for (int element : a)
    System.out.println(element);
```

将数组 a 的每个元素打印在单独的一行上。

你应该将这个循环理解为“对于 a 中的每个元素”。Java 语言的设计者曾考虑使用 foreach 和 in 之类的关键字。但这个循环是后来才添加到 Java 语言中的，最终没有人愿意破坏已经包含这些名称的方法或变量（例如 System.in）的旧代码。

当然，你也可以使用传统的 for 循环达到同样的效果：

```java
for (int i = 0; i < a.length; i++)
    System.out.println(a[i]);
```

然而，“for each”循环更简洁，也更不容易出错，因为你无需担心那些烦人的起始和结束索引值。

> **注意：** “for each”循环的循环变量遍历的是数组的元素，而不是索引值。

如果你需要处理集合中的所有元素，“for each”循环是对传统循环的一个很好的改进。然而，仍然有很多场景需要使用传统的 for 循环。例如，你可能不想遍历整个集合，或者你可能需要在循环内部获取索引值。

> **提示：** 有一种更简单的方法可以打印数组的所有值，即使用 Arrays 类的 toString 方法。调用 Arrays.toString(a) 会返回一个包含数组元素的字符串，用方括号括起来并用逗号分隔，例如 "[2, 3, 5, 7, 11, 13]"。要打印数组，只需调用

```java
System.out.println(Arrays.toString(a));
```

### 3.10.4 数组复制

你可以将一个数组变量复制到另一个数组变量，但这样做之后*两个变量引用同一个数组*：

```java
int[] luckyNumbers = smallPrimes;
luckyNumbers[5] = 12; // now smallPrimes[5] is also 12
```

图 3.14 显示了结果。如果你确实希望将一个数组的所有值复制到一个新数组中，请使用 `Arrays` 类中的 `copyOf` 方法：

```java
int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);
```

第二个参数是新数组的长度。这个方法的一个常见用途是增加数组的大小：

```java
luckyNumbers = Arrays.copyOf(luckyNumbers, 2 * luckyNumbers.length);
```

如果数组包含数字，则额外元素填充 0；如果数组包含布尔值，则填充 false。相反，如果长度小于原始数组的长度，则只复制初始值。

```java
    else if (args[0].equals("-g"))
        System.out.println("Goodbye,");
    // print the other command-line arguments
    for (int i = 1; i < args.length; i++)
        System.out.println(" " + args[i]);
    System.out.println("!");
}
```

如果程序是这样调用的：

```
java Message -g cruel world
```

那么 args 数组将包含以下内容：

```
args[0]: "-g"
args[1]: "cruel"
args[2]: "world"
```

程序会打印出消息：

```
Goodbye, cruel world!
```

> **C++ 注意：** 在 Java 程序的 main 方法中，程序名称不会存储在 args 数组中。例如，当你从命令行启动程序时：
>
>     java Message -h world
>
> 那么 args[0] 将是 "-h"，而不是 "Message" 或 "java"。

### 3.10.6 数组排序

要对数字数组进行排序，可以使用 Arrays 类中的 sort 方法之一：

```java
int[] a = new int[10000];
. . .
Arrays.sort(a)
```

该方法使用了经过调优的 QuickSort 算法版本，据称在大多数数据集上都非常高效。Arrays 类还提供了其他几个方便的数组方法，这些方法包含在本节末尾的 API 注释中。

清单 3.7 中的程序展示了数组的实际应用。该程序为彩票游戏生成一组随机数字组合。例如，如果你玩“从 49 个数字中选择 6 个”的彩票，程序可能会打印如下内容：

下注以下组合，它会让你变得富有！

+   4
+   7
+   8
+   19
+   30
+   44

为了选择这样一组随机数字，我们首先用一个数组 numbers 填充值 1, 2, ..., n：

```
int[] numbers = new int[n];
for (int i = 0; i < numbers.length; i++)
    numbers[i] = i + 1;
```

第二个数组保存要抽取的数字：

```
int[] result = new int[k];
```

现在我们抽取 k 个数字。Math.random 方法返回一个介于 0（包含）和 1（不包含）之间的随机浮点数。将结果乘以 n，我们得到一个介于 0 和 n − 1 之间的随机数。

```
int r = (int) (Math.random() * n);
```

我们将结果设置为该索引处的数字。最初，这只是 r + 1，但稍后你会看到，numbers 数组的内容在每次抽取后都会改变。

```
result[i] = numbers[r];
```

现在我们必须确保不再抽取该数字——所有彩票数字必须互不相同。因此，我们用数组中的最后一个数字覆盖 numbers[r]，并将 n 减 1。

```
numbers[r] = numbers[n - 1];
n--;
```

关键在于，每次抽取时我们选择的是一个索引，而不是实际值。该索引指向一个包含尚未抽取的值的数组。

抽取 k 个彩票数字后，我们对 result 数组进行排序，以获得更令人满意的输出：

```
Arrays.sort(result);
for (int r : result)
    System.out.println(r);
```

