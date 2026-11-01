
In the select clause, you project a new anonymous type whose properties are the total sales (calculated by referencing the cg result set) and the key value of the group, which you reference with the special group Key:

```
select new { TotalSales = cg.Sum(c => c.Sales), Region = cg.Key }
```

The group result set implements the LINQ IGrouping interface, which supports the Key property. You almost always want to reference the Key property in some way in processing group results, because it represents the criteria by which each group in your data was created.

You want to order the result in descending order by TotalSales field so you can see which region has the highest total sales, next highest, and so on. To do that, you create a second query to order the results from the group query:

```
var orderedResults =
    from cg in queryResults
    orderby cg.TotalSales descending
    select cg
;
```

The second query is a standard select query with an orderby clause, as you have seen in previous examples; it does not make use of any LINQ group capabilities except that the data source comes from the previous group query.

Next, you print out the results, with a little bit of formatting code to display the data with column headers and some separation between the totals and the group names:

```
WriteLine("Total\t: By\nSales\t: Region\n---\t---");
foreach (var item in orderedResults)
{
    WriteLine($"{item.TotalSales}\t: {item.Region}*");
};
```

This could be formatted in a more sophisticated way with field widths and by right-justifying the totals, but this is just an example so you don't need to bother — you can see the data clearly enough to understand what the code is doing.

## USING JOINS

A data set such as the customers and orders list you just created, with a shared key field (ID), enables a join query, whereby you can query related data in both lists with a single query, joining the results together with the key field. This is similar to the JOIN operation in the SQL data query language; and as you might expect, LINQ provides a join command in the query syntax, which you will use in the following Try It Out.

### TRY IT OUT Join Query: BegVCSharp_20_11_JoinQuery\Program.cs

Follow these steps to create the example in Visual Studio 2015:

- 1. Create a new console application called BegVCSharp_20_11_JoinQuery in the directory C:\BegVCSharp\Chapter20.

## WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| What LINQ is and when to use it | LINQ is a query language built into C#. Use LINQ to query data from large collections of objects, XML, or databases. |
| Parts of a LINQ query | A LINQ query includes the `from`, `where`, `select`, and `orderby` clauses. |
| How to get the results of a LINQ query | Use the `foreach` statement to iterate through the results of a LINQ query. |
| Deferred execution | LINQ query execution is deferred until the `foreach` statement is executed. |
| Method syntax and query syntax | Use the query syntax for most LINQ queries and method queries when required. For any given query, the query syntax or the method syntax will give the same result. |
| Lambda Expressions | Lambda expressions let you declare a method on-the-fly for use in a LINQ query using the method syntax. |
| Aggregate operators | Use LINQ aggregate operators to obtain information about a large data set without having to iterate through every result. |
| Group queries | Use group queries to divide data into groups, then sort, calculate aggregates, and compare by group. |
| Ordering | Use the `orderby` operator to order the results of a query. |
| Joins | Use the `join` operator to query related data in multiple collections with a single query. |

## 基于深度学习的网络入侵检测研究综述

张伟 李娜

（北京邮电大学 网络空间安全学院，北京 100876）

**摘要：** 随着网络攻击技术的日益复杂，传统入侵检测方法已无法满足现代网络安全需求。近年来，深度学习在多个领域取得突破性进展，也被广泛应用于入侵检测。本文对基于深度学习的入侵检测方法进行综述，首先介绍了入侵检测的基本概念，然后重点分析了包括卷积神经网络（CNN）、循环神经网络（RNN）、深度自编码器（DAE）和生成对抗网络（GAN）在内的多种典型深度学习模型，并比较了它们的性能，最后指出了当前研究的不足和未来的发展方向。

**关键词：** 深度学习；入侵检测；卷积神经网络；循环神经网络；生成对抗网络

中图分类号：TP393.08 文献标志码：A

### 1 引言

随着互联网的飞速发展，网络攻击事件频发，给社会造成了巨大损失。入侵检测系统（IDS）作为网络安全的关键防线，能够实时监测网络流量并识别恶意行为。然而，传统入侵检测方法如基于特征匹配和统计学的方法，在面对新型攻击时往往力不从心。深度学习的出现为入侵检测带来了新的技术手段，通过多层神经网络自动提取数据特征，有效提高了检测准确率。

### 2 相关工作

早期入侵检测研究主要采用机器学习方法，如支持向量机和决策树。近年来，研究者开始尝试将深度学习模型应用于入侵检测。KDD Cup 99和NSL-KDD数据集被广泛用于评估模型性能。卷积神经网络能够提取空间特征，适用于网络流量的结构化数据；循环神经网络擅长处理时序特征，可用于流量序列建模；自编码器可通过重构误差检测异常。

- 4. Uncheck the Include Prerelease checkbox and get the Entity Framework latest stable release as shown in Figure 21-2. Click the Install button.

![](img/cf72ea860016d2d680fc085fc06f265a_681_0.png)

FIGURE 21-2

- 5. Click OK on the Preview dialog as shown in Figure 21-3.

![](img/cf72ea860016d2d680fc085fc06f265a_681_1.png)

FIGURE 21-3

- 6. Now the License Acceptance dialog for the Entity Framework appears as shown in Figure 21-4. Click the I Accept button.

![](img/cf72ea860016d2d680fc085fc06f265a_681_2.png)

FIGURE 21-4

- 7. Now the Entity Framework and its references are added to your project. You can see them in the References section of your project in Solution Explorer as shown in Figure 21-5.

- 12. Next, add code in the Main() function to create a couple of Book objects, and save the book objects to the database:

```
class Program
{
    static void Main(string[] args)
    {
        using (var db = new BookContext())
        {
            Book book1 = new Book { Title = "Beginning Visual C# 2015",
                Author = "Perkins, Reid, and Hammer" };
            db.Books.Add(book1);

            Book book2 = new Book { Title = "Beginning XML",
                Author = "Fawcett, Quin, and Ayers"};
            db.Books.Add(book2);

            db.SaveChanges();
        }
    }
}
```

- 13. Finally, add the code for a simple LINQ query to list the books in the database after creation:

```
var query = from b in db.Books
            orderby b.Title
            select b;

WriteLine("All books in the database:");
foreach (var b in query)
{
    WriteLine($"{b.Title} by {b.Author}, code={b.Code}");
}

WriteLine("Press a key to exit...");
ReadKey();
```

The complete code for your program should now look like this:

```
using System.Data.Entity;
using System.ComponentModel.DataAnnotations;
using static System.Console;

namespace BegVCSharp_21_1_CodeFirstDatabase
{
    public class Book
    {
        public string Title { get; set; }
        public string Author { get; set; }
        public int Code { get; set; }
    }

    public class BookContext : DbContext
    {
        public DbSet<Book> Books { get; set; }
    }

    class Program
```

Next you added the Entity Framework namespace at the top of the file below the other using clauses:

```
using System.Data.Entity;
```

Then you added the using clause for data annotations, so that you could add hints to tell the Entity Framework on how to set up the database, and the static System.Console namespace:

```
using System.ComponentModel.DataAnnotations;
using static System.Console;
```

Next, you added a Book class with Author, Title, and Code similar to the example used in Chapter 19. You used the [Key] attribute to identify the Code property as the unique identifier for each row in the database.

```
namespace BegVCSharp_21_1_CodeFirstDatabase
{
    public class Book
    {
        public string Title { get; set; }
        public string Author { get; set; }
        [Key] public int Code { get; set; }
    }
}
```

Next you created the BookContext class inheriting from the DbContext (Database Context) class in the Entity Framework for creating, updating, and deleting the book objects as needed in the database:

```
public class BookContext : DbContext
{
    public DbSet<Book> Books { get; set; }
}
```

The class member DbSet<Book> is a collection of all the Book entities in your database.

Next you added code to use the BookContext to create two Book objects and save them to the database:

```
using (var db = new BookContext())
{
    Book book1 = new Book { Title = "Beginning Visual C# 2015", Author = "Perkins, Reid, and Hammer" };
    db.Books.Add(book1);

    Book book2 = new Book { Title = "Beginning XML", Author = "Fawcett, Quin, and Ayers" };
    db.Books.Add(book2);

    db.SaveChanges();
}
```

The using(var db = new BookContext()) clause lets you create a new BookContext instance for use in all the following code between the curly braces. Besides being a convenient shorthand, the using() clause ensures that the database connection and other underlying plumbing objects associated with the connection are closed properly when your program is finished, even if there is an exception or other unexpected event.

The Book creation and assignment statements such as

```
Book book = new Book { Title = "Beginning Visual C# 2015", Author = "Perkins, Reid, and Hammer" };
```
