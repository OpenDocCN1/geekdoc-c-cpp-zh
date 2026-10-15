

添加到收藏中的每张 DVD 都通过其标题、导演、发行年份、购买价格以及是否为蓝光格式来指定。

清单 8.8 展示了 DVDCollection 类。它包含一个 DVD 对象数组，用于表示该收藏。它维护着收藏中 DVD 的数量及其总价值。它还会跟踪收藏数组的当前大小，以便在向收藏中添加过多 DVD 时可以创建更大的数组。

## 清单 8.8

```
//****************************************************************
//  DVDCollection.java      Author: Lewis/Loftus
//
//  Represents a collection of DVD movies.
//****************************************************************

import java.text.NumberFormat;

public class DVDCollection
{
    private DVD[] collection;
    private int count;
    private double totalCost;

    //---------------------------------------------------------------
    // Constructor: Creates an initially empty collection.
    //---------------------------------------------------------------
    public DVDCollection ()
    {
        collection = new DVD[100];
        count = 0;
        totalCost = 0.0;
    }

    //---------------------------------------------------------------
    // Adds a DVD to the collection, increasing the size of the
    // collection array if necessary.
    //---------------------------------------------------------------
    public void addDVD (String title, String director, int year,
                        double cost, boolean bluray)
    {
        if (count == collection.length)
            increaseSize();

        collection[count] = new DVD (title, director, year, cost, bluray);
        totalCost += cost;
        count++;
    }

    //-------------------------------------------------------------------------
    // Returns a report describing the DVD collection.
    //-------------------------------------------------------------------------
    public String toString()
    {
        NumberFormat fmt = NumberFormat.getCurrencyInstance();

        String report = "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~\n";
        report += "My DVD Collection\n\n";

        report += "Number of DVDs: " + count + "\n";
        report += "Total cost: " + fmt.format(totalCost) + "\n";
        report += "Average cost: " + fmt.format(totalCost/count);

        report += "\n\nDVD List:\n\n";

        for (int dvd = 0; dvd < count; dvd++)
            report += collection[dvd].toString() + "\n";

        return report;
    }

    //-------------------------------------------------------------------------
    // Increases the capacity of the collection by creating a
    // larger array and copying the existing collection into it.
    //-------------------------------------------------------------------------
    private void increaseSize ()
    {
        DVD[] temp = new DVD[collection.length * 2];

        for (int dvd = 0; dvd < collection.length; dvd++)
            temp[dvd] = collection[dvd];

        collection = temp;
    }
}
```

collection 数组在 DVDCollection 构造函数中被实例化。每次向收藏中添加一张 DVD（使用 addDVD 方法）时，都会创建一个新的 DVD 对象，并将其引用存储在 collection 数组中。

每次向收藏中添加 DVD 时，我们都会检查是否已达到 collection 数组的当前容量。如果不进行此检查，当我们尝试在无效索引处存储新的 DVD 对象时，最终会抛出异常。如果已达到当前容量，则会调用私有的 increaseSize 方法，该方法首先创建一个大小为当前 collection 数组两倍的数组。然后，将现有收藏中的每张 DVD 复制到新数组中。最后，将 collection 引用设置为更大的数组。利用这种技术，理论上我们的 DVD 收藏永远不会空间不足。DVDCollection 对象的用户（此处是 main 方法）永远不必担心空间不足的问题，因为这一切都在内部处理。

图 8.3 展示了 Movies 程序的 UML 类图。回想一下，空心菱形表示聚合关系。关系中的基数也已注明：一个 DVDCollection 对象包含零个或多个 DVD 对象。

DVDCollection 类的 toString 方法返回一份完整报告，汇总该收藏。该报告部分是借助对收藏中存储的每个 DVD 对象的 toString 方法的调用来创建的。清单 8.9 展示了 DVD 类。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_427_0.png)

图 8.3 Movies 程序的 UML 类图

## 清单 8.9

```
//***************************************************************************
// DVD.java      Author: Lewis/Loftus
//
// Represents a DVD video disc.
//***************************************************************************

import java.text.NumberFormat;

public class DVD
{
    private String title, director;
    private int year;
    private double cost;
    private boolean bluray;

    //--------------------------------------------------------------------------------
    // Creates a new DVD with the specified information.
    //--------------------------------------------------------------------------------
    public DVD (String title, String director, int year, double cost,
                boolean bluray)
    {
        this.title = title;
        this.director = director;
        this.year = year;
        this.cost = cost;
        this.bluray = bluray;
    }

    //--------------------------------------------------------------------------------
    // Returns a string description of this DVD.
    //--------------------------------------------------------------------------------
    public String toString()
    {
        NumberFormat fmt = NumberFormat.getCurrencyInstance();

        String description;

        description = fmt.format(cost) + "\t" + year + "\t";
        description += title + "\t" + director;
        if (bluray)
            description += "\t" + "Blu-ray";

        return description;
    }
}
```

## 自测题（见附录 N 中的答案）

SR 8.14 如何创建对象数组？

SR 8.15 假设 team 是一个字符串数组，用于存放排球队六名队员的名字：Amanda、Clare、Emily、Julie、Katie 和 Maria。

- a. 为 team 编写数组声明。
- b. 展示如何使用初始化列表同时声明和填充 team。

SR 8.16 假设 Book 是一个类，其对象表示书籍。假设 Book 类的构造函数接受两个参数——书名和页数。

- a. 为名为 library 的变量编写声明，它是一个包含十本书的数组。
- b. 编写一条 new 语句，将 library 数组中的第一本书设置为《星船伞兵》，该书有 208 页。

## 8.4 命令行参数

Java 应用程序 main 方法的形参始终是一个 String 对象数组。在之前的示例中我们忽略了该参数，但现在我们可以讨论它如何偶尔发挥作用。

> 关键概念
> 命令行参数存储在一个 String 对象数组中，并传递给 main 方法。

当应用程序提交给解释器时，Java 运行时环境会调用 main 方法。String[] 参数（我们通常称为 args）表示在调用解释器时提供的命令行参数。调用解释器时命令行上的任何额外信息都会存储在 args 数组中，供程序使用。这种技术是向程序提供输入的另一种方式。

清单 8.10 中显示的程序使用命令行参数来打印一个姓名标签。它假定第一个参数代表某种问候语，第二个参数代表一个人的姓名。

如果在命令行中没有为 NameTag 程序提供两个字符串，args 数组将没有足够（如果有的话）的元素，程序中的引用将导致抛出 ArrayIndexOutOfBoundsException 异常。如果命令行中包含额外信息，它们会存储在 args 数组中，但程序会忽略它们。

