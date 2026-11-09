
- 11. *Press* the F5 key to run the application. The output of the application appears, displaying a list of names in the first list box present on the form (Fig.VB-7.48).
- 12. *Click* the **Create New List** button (Fig.VB-7.48). The names starting with letter ‘S’, from the list of names in the first list box, are displayed in the second list box, as shown in Fig.VB-7.49.

![](img/9862a98a1a2d3bb14334137965a1ec60_276_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_276_1.png)

*Fig.VB-7.48*    *Fig.VB-7.49*

You have learned how to use a lambda expression in a LINQ query. In the next section, you learn about Parallel LINQ, a new feature added to LINQ in .NET Framework 4.0.

## Exploring Parallel LINQ

PLINQ is a parallel implementation of the LINQ pattern and aims to use all the processors present in a system. LINQ queries are syntactically very similar to the LINQ to Objects queries. For instance, consider the following simple LINQ to Objects query:

```text
var output = from x in source
             where (some condition)
             select (something)
```

Now, consider the following PLINQ query:

```text
var output = from x in source.AsParallel()
             where (some condition)
             select (something)
```

Note that the preceding PLINQ query is the same as the LINQ to Objects query, except the use of the AsParallel method. This method is specific to PLINQ and is available in the ParallelEnumerable class. This class exposes most of the PLINQ functionalities and is available in the System.Linq namespace.

> **LINQ to Objects indicates the use of LINQ queries on any in-memory IEnumerable or IEnumerable(Of T) interface. In LINQ to Objects queries, the queries are executed without using technologies, such as LINQ to SQL.**

Similar to the non-parallel sequential PLINQ query, PLINQ queries perform operations on any in-memory IEnumerable or IEnumerable(Of T) interface. PLINQ divides a data source into different segments and then executes each of the segments on separate worker threads across multiple processors. In many cases, queries run much faster because of parallel execution. However, parallelization does not imply that all the queries will run fast as there may be various complexities involved with parallelization. Moreover, note that the PLINQ concept applies only to the LINQ to Objects queries.

Perform the following steps to use a simple PLINQ query in a Console application:

- 1. *Start* Visual Studio 2010.
- 2. *Select* File→New→Project from the menu bar. The **New Project** dialog box opens.
- 3. *Select* Visual Basic→Windows from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Console Application** in the middle pane to create a Console application.
- 5. Enter the name of the application as **PLINQExample** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
- 6. *Click* the **OK** button to close the **New Project** dialog box. The **PLINQExample** application is created.
- 7. Double-click the **Module1.vb** file in **Solution Explorer** to open this file in Code Editor and add the highlighted code snippet shown in Listing 7.24 to Code Editor:

**Listing 7.24: Showing the Use of a PLINQ Query**

```vb
Module Module1
    Sub Main()
        Dim dataSource = Enumerable.Range(2, 20)
        Dim output = From x In dataSource.AsParallel() Where x Mod 2 = 0
        For Each x In output
            Console.WriteLine(x)
        Next
        Console.ReadLine()
    End Sub
End Module
```

The highlighted code snippet in Listing 7.24 shows the code of the Sub procedure, Main, of the Module1 Module. In the highlighted code snippet, we first generate a sequence of integral numbers in the range from 2 to 20 by calling the **Range** method of the **Enumerable** class. Then, we create a PLINQ query in which we retrieve the numbers that are divisible by 2 from the range of numbers that is 2 to 20, which range we defined by Range function of the **Enumerable** class. Note that we have used the **AsParallel** method in the PLINQ query to specify that the query will be executed using parallel execution.

- 8. Press the F5 key to run the application. The output of the application appears, as shown in Fig.VB-7.50:

![](img/9862a98a1a2d3bb14334137965a1ec60_277_0.png)

Fig.VB-7.50

The output screen displays only those numbers that are divided by 2 from 2 to 20 numbers series.

## Summary

In this chapter, you first learned how to create a simple LINQ query. Then, standard query operators were discussed that are used to create LINQ queries. Next, you learned to implement LINQ to ADO.NET. You also learned to use anonymous types and lambda expressions in LINQ queries. Finally, parallel LINQ was discussed.

## 床架中心支撑方案

![](img/9862a98a1a2d3bb14334137965a1ec60_278_0.png)

该床架在墨西哥组装，配有金属框架和中心支撑横档。用户询问是否需要额外的中心支撑。

### 是否需要中心支撑？

是否需要在床架下方增加支撑取决于床垫类型和床架本身的横档设计。如果您的床架已有中心横档且使用弹簧床垫底座（box spring），则通常不需要额外支撑。

- 如果使用泡沫床垫，建议增加中心支撑
- 如果使用弹簧床垫底座，现有支撑通常已足够
- 纸板可以作为临时支撑方案，但长期使用不推荐

C# pronounced as *sharp*, is a modern, high-level, robust, powerful, and object-oriented programming language that is based on the traditional C++ language. However, C# is relatively easier to learn and work with than C++ because it has a simple syntax and is a .NET-compatible language. Being a .NET-compatible language, C# can use the services that Common Language Runtime (CLR) offers, such as type-safety, garbage collection, and integrated security. Microsoft introduced C# along with the beta version of .NET Framework in 2000. Since then, C# has been an important part of the .NET Framework. The latest version of C# is a part of .NET Framework 4.0 and Visual Studio 2010; therefore, this new version is also known as C# 2010.

C# 2010 enables you to develop secure, reliable, and robust applications on the Microsoft .NET platform. You can use C# 2010 to create traditional Windows client applications, distributed components, client-server Web applications, and database applications. In addition, C# 2010 provides an advanced code editor, user interface designers, integrated debugger, and many other tools to make it easier to develop applications based on latest versions of the .NET Framework.

This chapter begins by discussing the new features of C# 2010. Next, C# language fundamentals, including keywords, identifiers, operators, operator precedence, data types, and data type conversion are discussed. Further, you learn to work with variables and constants in C# 2010. You also learn how to work with arrays in C# 2010. Towards the end, you learn to work with control flow statements, including selection statements, iteration statements, and jump statements.

Let’s begin by discussing the new features of C# 2010.

## Exploring New Features of C# 2010

C# 2010 includes a number of new features that enhance the integration of C# .NET applications with Microsoft Office and enables you to develop test-driven applications (applications that have a very short development cycle). The main new features of C# 2010 are as follows:

- Call hierarchy
- Live semantic errors
- Named and optional arguments
- New command-line compiler options
- Enhanced Component Object Model (COM) interoperability

![](img/9862a98a1a2d3bb14334137965a1ec60_279_0.png)

> Some of the new features of C# 2010, such as type equivalence, dynamic support, covariance, and contravariance, work exactly in the same way as in Visual Basic 2010. Therefore, we are not discussing these features again. These features have already been discussed in Chapter 1, *Getting Started with Visual Basic 2010*, of the Visual Basic 2010 section.

Let’s discuss these features, one by one.

### Call Hierarchy

Call hierarchy is a feature of C# 2010 that helps you to work with Visual Studio 2010 Integrated Development Environment (IDE). It provides you the detailed information about all the calls that are made from or to a method, property, and constructor. It allows you to view all implementations of an interface member and all overridden versions of a virtual or abstract member. This feature helps you to understand the flow of control in the program code and enables you to evaluate the effects of changing the program code. The call hierarchy feature is available at design time. Fig. C#-1.1 shows how to use the call hierarchy feature to view all calls to or from a method, that is, all the calls that are made from the method or to the method:
