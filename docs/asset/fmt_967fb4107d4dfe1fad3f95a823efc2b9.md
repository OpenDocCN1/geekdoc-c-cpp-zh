
| 大写字母 | 大写字母计数 | 小写字母 | 小写字母计数 |
|------------------|-----------------|------------------|-----------------|
| A | 0 | a | 10 |
| B | 1 | b | 1 |
| C | 1 | c | 1 |
| D | 0 | d | 0 |
| E | 0 | e | 3 |
| F | 0 | f | 0 |
| G | 0 | g | 2 |
| H | 1 | h | 1 |
| I | 1 | i | 2 |
| J | 0 | j | 0 |
| K | 0 | k | 0 |
| L | 0 | l | 2 |
| M | 0 | m | 2 |
| N | 0 | n | 4 |
| O | 0 | o | 1 |
| P | 1 | p | 1 |
| Q | 0 | q | 0 |
| R | 0 | r | 3 |
| S | 1 | s | 3 |
| T | 0 | t | 2 |
| U | 0 | u | 1 |
| V | 0 | v | 1 |
| W | 0 | w | 0 |
| X | 0 | x | 0 |
| Y | 0 | y | 3 |
| Z | 0 | z | 0 |

非字母字符：14

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_415_0.png)

视频注释  
关于`LetterCount`示例的讨论。

两个计数器数组的索引范围都是0到25。我们必须将每个字符映射到一个计数器。一种合乎逻辑的做法是使用`upper[0]`统计找到的`'A'`字符数，使用`upper[1]`统计找到的`'B'`字符数，依此类推。同样，`lower[0]`用于计数字符`'a'`，`lower[1]`用于计数字符`'b'`，依此类推。另一个名为`other`的变量用于统计遇到的所有非字母字符。

注意，为了判断一个字符是否为大写字母，我们使用了布尔表达式`current >= 'A' && current <= 'Z'`。判断小写字母时也使用了类似的表达式。我们本可以使用`Character`类中的静态方法`isUpperCase`和`isLowerCase`来进行这些判断，但在这个示例中我们没有使用，以便强调这样一个要点：由于字符基于Unicode字符集，它们具有特定的数值和顺序，我们可以在编程中使用这些数值和顺序。

我们使用当前字符来计算要引用的数组索引。在计算索引时，我们必须小心，确保它保持在数组边界内并与正确的元素匹配。请记住，在Unicode字符集中，大写和小写字母都是连续的，并按顺序排列（参见附录C）。因此，取一个大写字母（如`'E'`，其数值为69）的数值，然后减去字符`'A'`的数值（65），得到4，这正是字符`'E'`的计数器所对应的正确索引。注意，在程序中我们实际上不需要知道每个字母的具体数值。

## 另一种数组语法

从语法上讲，在Java中声明数组引用有两种方式。第一种方式（在前面的示例和本书中一直使用）是将方括号与数组中存储的值的类型关联起来。第二种方式是将方括号与数组名关联起来。因此，下面两种声明是等价的：

```java
int[] grades;
int grades[];
```

尽管就编译器而言，这两种声明方式没有区别，但第一种方式与其他类型的声明保持一致。如果将数组方括号与元素类型关联，则声明的类型是明确的，尤其是在同一行声明多个变量时。因此，在本书中我们始终将方括号与元素类型关联。

## 初始化列表

**关键概念：** 可以使用初始化列表来实例化数组对象，而不必使用`new`运算符。

可以使用*初始化列表*来实例化数组，并为数组元素提供初始值。本质上，这与在声明中初始化基本数据类型的变量是相同的思路，只是数组需要多个值。

初始化列表中的各项用逗号分隔，并用花括号`{}`括起来。使用初始化列表时，不使用`new`运算符。数组的大小由初始化列表中的项数决定。例如，下面的声明将数组`scores`实例化为一个包含八个整数的数组，索引从0到7，并具有指定的初始值：

```java
int[] scores = {87, 98, 69, 87, 65, 76, 99, 83};
```

初始化列表只能在数组首次声明时使用。

初始化列表中每个值的类型必须与数组元素的类型匹配。让我们看另一个例子：

```java
char[] vowels = {'A', 'E', 'I', 'O', 'U'};
```

在这种情况下，变量`vowels`被声明为包含五个字符的数组，初始化列表包含字符字面量。

清单8.4中显示的程序演示了如何使用初始化列表来实例化数组。

## 数组作为参数

**关键概念：** 整个数组可以作为参数传递，使形式参数成为原始数组的别名。

整个数组可以作为参数传递给方法。因为数组是对象，所以当整个数组作为参数传递时，传递的是原始数组引用的副本。我们在第7章讨论过这个问题，它适用于所有对象。

接收数组作为参数的方法可以永久性地更改数组中的某个元素，因为它引用的是原始元素值。但该方法不能永久性地更改对数组本身的引用，因为发送给方法的是原始引用的副本。这些规则与适用于任何对象类型的规则一致。

数组元素也可以传递给方法。如果元素类型是基本类型，则传递的是值的副本。如果元素是对对象的引用，则传递的是对象引用的副本。与往常一样，方法内部对参数所做的更改产生的影响取决于参数的类型。我们将在下一节进一步讨论对象数组。

### 列表 8.4

```java
//******************************
// Primes.java Author: Lewis/Loftus
// Demonstrates the use of an initializer list for an array.
//******************************
public class Primes
{
// Stores some prime numbers in an array and prints them.
//
public static void main (String[] args)
{
int[] primeNums = { 2, 3, 5, 7, 11, 13, 17, 19};
System.out.println ("Array length: " + primeNums.length);
System.out.println("The first few prime numbers are:");
for (int prime : primeNums)
System.out.print(prime + " ");
}
}
```

### 输出

Array length: 8
The first few prime numbers are:
2 3 5 7 11 13 17 19

### 自测题（答案见附录 N）

- SR 8.4 数组的元素类型是什么？
- SR 8.5 创建数组的过程是什么？何时为数组分配内存？
- SR 8.6 写一个数组声明来表示参加夏令营的全部 100 名儿童的年龄。
- SR 8.7 写一个数组声明来表示掷标准六面骰子时每个面出现的次数。
- SR 8.8 解释数组边界检查的概念。当 Java 数组使用无效值进行索引时会发生什么？
- SR 8.9 什么是差一错误？它与数组有何关系？
- SR 8.10 编写代码，将名为 `values` 的整数数组的每个元素递增（加一）。
- SR 8.11 编写代码，计算并打印名为 `values` 的整数数组元素的总和。
- SR 8.12 数组初始化列表实现了什么？
- SR 8.13 能否将整个数组作为参数传递？如何实现？

### 8.3 对象数组

本章前面示例中，我们使用数组存储整数和字符等基本类型。数组也可以将对象引用作为元素存储。仅使用数组和其他对象就可以创建相当复杂的信息管理结构。例如，一个数组可以包含对象，而每个对象又可以由多个变量和使用这些变量的方法组成。这些变量本身也可以是数组，等等。程序的设计应利用组合这些构造的能力，为信息创建最合适的表示。

请记住，数组本身就是一个对象。因此，将名为 `weight` 的 `int` 值数组形象化如下是合适的：

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_419_0.png)

> 实例化对象数组只会为存储引用预留空间。存储在每个元素中的元素必须分别实例化。

当我们将对象存储在数组中时，每个元素都是一个单独的对象。也就是说，对象数组实际上是对象引用的数组。考虑以下声明：

```
String[] words = new String[5];
```

变量 `words` 是对 `String` 对象的引用数组。声明中的 `new` 运算符实例化数组并为五个 `String` 引用预留空间。此声明不会创建任何 `String` 对象；它仅创建了一个保存对 `String` 对象引用的数组。最初，数组看起来如下：

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_420_0.png)

在创建几个 `String` 对象并放入数组后，它可能看起来如下：

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_420_1.png)

`words` 数组是一个对象，它所包含的每个字符字符串都是其自己的对象。数组中包含的每个对象都必须分别实例化。

请记住，`String` 对象可以用字符串字面量表示。因此，以下声明创建了一个名为 `verbs` 的数组，并使用初始化列表用多个 `String` 对象填充它，每个对象都使用字符串字面量实例化：

```
String[] verbs = {"play", "work", "eat", "sleep"};
```

列表 8.5 中所示的程序 `GradeRange` 创建一个 `Grade` 对象数组，然后打印它们。`Grade` 对象是使用数组初始化列表中的几个 `new` 运算符创建的。

`Grade` 类如列表 8.6 所示。每个 `Grade` 对象代表学校课程的字母等级，并包含一个数值下限。等级名称和下限的值可以使用 `Grade` 构造函数设置，也可以使用适当的修改器方法设置。还定义了访问器方法，以及 `toString` 方法以返回等级的字符串表示形式。`toString` 方法在 `main` 方法中打印等级时会自动调用。

让我们再看一个例子。列表 8.7 显示了 `Movies` 类，其中包含一个 `main` 方法，该方法创建、修改和检查 DVD 收藏。

### 列表 8.5

```java
//*******************************************************************
//  GradeRange.java      Author: Lewis/Loftus
//
// Demonstrates the use of an array of objects.
//*******************************************************************
public class GradeRange
{
    //-------------------------------------------------------------
    //  Creates an array of Grade objects and prints them.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        Grade[] grades =
        {
            new Grade("A", 95), new Grade("A-", 90),
            new Grade("B+", 87), new Grade("B", 85), new Grade("B-", 80),
            new Grade("C+", 77), new Grade("C", 75), new Grade("C-", 70),
            new Grade("D+", 67), new Grade("D", 65), new Grade("D-", 60),
            new Grade("F", 0)
        };
        for (Grade letterGrade : grades)
            System.out.println (letterGrade);
    }
}
```

### 输出

|  |  |
|---|---|
| A | 95 |
| A- | 90 |
| B+ | 87 |
| B | 85 |
| B- | 80 |
| C+ | 77 |
| C | 75 |
| C- | 70 |
| D+ | 67 |
| D | 65 |
| D- | 60 |
| F | 0 |

### 列表 8.6

```java
//***************************************************************************
// Grade.java      Author: Lewis/Loftus
//
// Represents a school grade.
//***************************************************************************
public class Grade
{
    private String name;
    private int lowerBound;
    //---------------------------------------------------------------
    // Constructor: Sets up this Grade object with the specified
    // grade name and numeric lower bound.
    //---------------------------------------------------------------
    public Grade (String grade, int cutoff)
    {
        name = grade;
        lowerBound = cutoff;
    }
    //---------------------------------------------------------------
    // Returns a string representation of this grade.
    //---------------------------------------------------------------
    public String toString()
    {
        return name + "\t" + lowerBound;
    }
    //---------------------------------------------------------------
    // Name mutator.
    //---------------------------------------------------------------
    public void setName (String grade)
    {
        name = grade;
    }
    //---------------------------------------------------------------
    // Lower bound mutator.
    //---------------------------------------------------------------
    public void setLowerBound (int cutoff)
    {
        lowerBound = cutoff;
    }
```

### 列表 8.7 继续

```java
System.out.println (movies);
movies.addDVD ("Iron Man 2", "Jon Favreau", 2010, 22.99, false);
movies.addDVD ("Casablanca", "Michael Curtiz", 1942, 19.95, false);
System.out.println (movies);
}
```

### 输出

```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
My DVD Collection
Number of DVDs: 5
Total cost: $98.30
Average cost: $19.66
DVD List:
$24.95 1972 The Godfather Francis Ford Coppola Blu-ray
$19.95 2009 District 9 Neill Blomkamp
$15.95 2008 Iron Man Jon Favreau
$17.50 1950 All About Eve Joseph Mankiewicz
$19.95 1999 The Matrix Andy & Lana Wachowski Blu-ray
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

My DVD Collection
Number of DVDs: 7
Total cost: $141.24
Average cost: $20.18
DVD List:
```
