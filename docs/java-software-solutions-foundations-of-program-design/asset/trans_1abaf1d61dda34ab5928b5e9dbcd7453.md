

# 列表 8.4

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

# 输出

Array length: 8
The first few prime numbers are:
2 3 5 7 11 13 17 19

# 自测题（答案见附录 N）

- SR 8.4 数组的元素类型是什么？
- SR 8.5 创建数组的过程是什么？何时为数组分配内存？
- SR 8.6 写一个数组声明来表示参加夏令营的全部 100 名儿童的年龄。
- SR 8.7 写一个数组声明来表示掷标准六面骰子时每个面出现的次数。

- SR 8.8 解释数组边界检查的概念。当 Java 数组使用无效值进行索引时会发生什么？
- SR 8.9 什么是差一错误？它与数组有何关系？
- SR 8.10 编写代码，将名为 values 的整数数组的每个元素递增（加一）。
- SR 8.11 编写代码，计算并打印名为 values 的整数数组元素的总和。
- SR 8.12 数组初始化列表实现了什么？
- SR 8.13 能否将整个数组作为参数传递？如何实现？

# 8.3 对象数组

本章前面示例中，我们使用数组存储整数和字符等基本类型。数组也可以将对象引用作为元素存储。仅使用数组和其他对象就可以创建相当复杂的信息管理结构。例如，一个数组可以包含对象，而每个对象又可以由多个变量和使用这些变量的方法组成。这些变量本身也可以是数组，等等。程序的设计应利用组合这些构造的能力，为信息创建最合适的表示。

请记住，数组本身就是一个对象。因此，将名为 weight 的 int 值数组形象化如下是合适的：

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_419_0.png)

> 实例化对象数组只会为存储引用预留空间。存储在每个元素中的元素必须分别实例化。

当我们将对象存储在数组中时，每个元素都是一个单独的对象。也就是说，对象数组实际上是对象引用的数组。考虑以下声明：

```
String[] words = new String[5];
```

变量 words 是对 String 对象的引用数组。声明中的 new 运算符实例化数组并为五个 String 引用预留空间。此声明不会创建任何 String 对象；它仅创建了一个保存对 String 对象引用的数组。最初，数组看起来如下：

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_420_0.png)

在创建几个 String 对象并放入数组后，它可能看起来如下：

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_420_1.png)

words 数组是一个对象，它所包含的每个字符字符串都是其自己的对象。数组中包含的每个对象都必须分别实例化。

请记住，String 对象可以用字符串字面量表示。因此，以下声明创建了一个名为 verbs 的数组，并使用初始化列表用多个 String 对象填充它，每个对象都使用字符串字面量实例化：

```
String[] verbs = {"play", "work", "eat", "sleep"};
```

列表 8.5 中所示的程序 GradeRange 创建一个 Grade 对象数组，然后打印它们。Grade 对象是使用数组初始化列表中的几个 new 运算符创建的。

Grade 类如列表 8.6 所示。每个 Grade 对象代表学校课程的字母等级，并包含一个数值下限。等级名称和下限的值可以使用 Grade 构造函数设置，也可以使用适当的修改器方法设置。还定义了访问器方法，以及 toString 方法以返回等级的字符串表示形式。toString 方法在 main 方法中打印等级时会自动调用。

让我们再看一个例子。列表 8.7 显示了 Movies 类，其中包含一个 main 方法，该方法创建、修改和检查 DVD 收藏。

# 列表 8.5

```
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

# 输出

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

# 列表 8.6

```
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

# 列表 8.7 继续

```
System.out.println (movies);

movies.addDVD ("Iron Man 2", "Jon Favreau", 2010, 22.99, false);
movies.addDVD ("Casablanca", "Michael Curtiz", 1942, 19.95, false);

System.out.println (movies);
}
```

# 输出

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

$24.95 1972 The Godfather Francis Ford Coppola Blu-ray
$19.95 2009 District 9 Neill Blomkamp
$15.95 2008 Iron Man Jon Favreau
$17.50 1950 All About Eve Joseph Mankiewicz
$19.95 1999 The Matrix Andy & Lana Wachowski Blu-ray
$22.99 2010 Iron Man 2 Jon Favreau
$19.95 1942 Casablanca Michael Curtiz
```

