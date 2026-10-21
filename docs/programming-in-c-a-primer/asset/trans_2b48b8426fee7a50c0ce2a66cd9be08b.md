

## 9.7 ARRAYLIST 类

System.Collections 命名空间定义了一个名为 ArrayList 的类，该类可以存储动态大小的对象数组。ArrayList 类包含许多方法来支持排序、删除和枚举其内容等操作。它还支持一个属性 Count，用于给出数组列表中的对象数量，以及一个属性 Capacity 用于修改或读取容量。

数组列表与数组非常相似，只是它具有动态增长的能力。我们可以通过指定想要的初始容量来创建一个数组列表。示例：

```
ArrayList cities = new ArrayList (30);
```

它创建了一个容量可存储三十个对象的 cities。 如果我们不指定大小，则默认为十六。 即，ArrayList cities = new ArrayList (); 将创建一个容量可存储十六个对象的 cities 列表。我们现在可以使用 Add () 方法向列表中添加元素：

```
cities.Add ("Bombay");
cities.Add ("Anand");
```

我们也可以删除一个元素：

```
cities.RemoveAt (1);
```

这将删除位置 1 处的对象。我们可以使用 Capacity 属性修改列表的容量：

```
cities.Capacity = 20;
```

我们可以使用 Count 属性按如下方式获取列表中实际存在的对象数：

```
int n = cities.Count;
```

如果我们需要创建一个对象数组但事先不知道数组会有多大，则数组列表会非常有用。此外，数组列表可以包含任何对象引用。

表 9.2 列出了 ArrayList 类支持的一些最重要的方法和属性。

### 表 9.2 一些重要的 ArrayList 方法和属性

| METHODS/PROPERTY | PURPOSE |
|---|---|
| Add () | Adds an object to a list |
| Clear () | Removes all the elements from the list |
| Contains () | Determines if an element is in the list |
| CopyTo () | Copies a list to another |
| Insert () | Inserts an element into the list |
| Remove () | Removes the first occurrence of an element |
| RemoveAt () | Removes the element at the specified place |
| RemoveRange () | Removes a range of elements |
| Sort () | Sorts the elements |
| Capacity | Gets or sets the number of elements in the list |
| Count | Gets the number of elements currently in the list |

程序 9.4 演示了如何创建和操作数组列表。

## 程序 9.4 | 使用 ARRAYLIST 类

```
using System;
using System.Collections;
class City
{
    public static void Main( )
    {
        ArrayList n = new ArrayList ();
        n.Add ("Madras");
        n.Add ("Bombay");
        n.Add ("Anand");
        n.Add ("Calcutta");
        n.Add ("Delhi");
        Console.WriteLine("Capacity = " + n.Capacity);
        Console.WriteLine("Elements present = " + n.Count);
        n.Sort();
        for (int i = 0; i < n.Count; i ++)
        {
            Console.WriteLine(n[i]);
        }
        Console.WriteLine();
        n.RemoveAt(4);
        for (int i = 0 ; i < n.Count ; i ++)
        {
            Console.WriteLine(n[i]);
        }
    }
}
```

程序 9.4 产生以下输出：

capacity = 16
Elements present = 5
Anand
Bombay
Calcutta
Delhi
Madras

Anand
Bombay
Calcutta
Delhi

程序 9.5 创建一个包含 10 个质数的数组列表并统计数组列表的元素数和容量。之后，程序从开头删除两个元素，统计元素数，然后再次在数组列表开头替换两个质数。

```
Console.Write(m + "");
Console.WriteLine();
}
}
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_174_0.png)

程序 9.6 在数组中显示数组项，然后反转数组的元素。另一个具有字符串元素的数组用于按字母顺序对数组元素进行排序，然后显示反转后的数据。

## 程序 9.6

### SORT 和 REVERSE 方法的应用

```
using System;
using System.Collections.Generic;
using System.Text;
namespace ArraySort_ReverseExample
{
class Program
{
public static void ArrDisplay(string[] arr1)
{
foreach (string str in arr1)
{
Console.WriteLine("Value: {0}", str);
}
Console.WriteLine("\n");
}
static void Main(string[] args)
{
```

## 程序 9.7 不规则数组的说明

```
using System;
using System.Collections.Generic;
using System.Text;
namespace jaggedArrayExample
{
    class Program
    {
        static void Main(string[] args)
        {
            const int rows = 3;
            // declare the jagged array as 3 rows high
            int[][] jagArr = new int[rows][];
            // a row with 2 elements
            jagArr[0] = new int[2];
            // a row with 3 elements
            jagArr[1] = new int[3];
            // a row with 4 elements
            jagArr[2] = new int[4];
            // Fill some (but not all) elements of the rows
            jagArr[0][1] = 54;
            jagArr[1][0] = 26;
            jagArr[1][1] = 18;
            jagArr[2][0] = 72;
            jagArr[2][3] = 404;
            for (int i = 0; i < 2; i++)
            {
                Console.WriteLine("This is jagged Array 1 having elements : [0][{0}] = {1}", i, jagArr[0][i]);
            }
            for (int i = 0; i < 3; i++)
            {
                Console.WriteLine("This is jagged Array 2 having elements : [1][{0}] = {1}", i, jagArr[1][i]);
            }
            for (int i = 0; i < 4; i++)
            {
                Console.WriteLine("This is jagged Array 3 having elements : [2][{0}] = {1}", i, jagArr[2][i]);
            }
        }
    }
}
```

## 案例研究

### 问题陈述

B.G International School 是一所提供从幼儿园到十年级初等教育给儿童的教育机构。B.G International School 的行政人员必须维护记录，其中包括在不同班级学习的学生姓名、班级和学号。手动维护每个学生的记录对于 B.G International School 的行政人员来说是一个繁琐的过程。当行政人员手动在登记册中输入记录时，会出现大量错误。B.G International School 如何自动化学生记录的输入任务？

### 解决方案

为了使维护学生记录的过程变得简单高效，B.G International School 联系 SoftDev 软件开发组织创建一个应用程序，以帮助输入学生记录的任务。SoftDev 将为 B.G International School 创建应用程序的任务分配给该组织的资深程序员 Siddharth。Siddharth 决定使用 C# 编程语言创建输入学生记录的应用程序。C# 在 System.Collections 命名空间中提供了 ArrayList 类。此 ArrayList 类允许我们创建一个数组列表，可以存储数组对象。数组列表的大小在运行时固定。因此，使用 ArrayList 类创建的数组列表是动态数组列表。由于 B.G International School 需要输入大量数据，使用 ArrayList 对 Siddharth 来说会有所帮助。

在了解了 B.G International School 的需求后，Siddharth 开发了以下 C# 应用程序。

```
using System;
using System.Collections;
using System.Collections.Generic;
using System.Text;
namespace AddStudentDetails
{
    class StudentDetails
    {
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_177_0.png)

```
static void Main(string[] args)
{
    string studname1, studname2, studname3;
    string classname1, classname2, classname3;
    string rollno1, rollno2, rollno3;
    string getresult;
    ArrayList arrlists = new ArrayList();
    Console.WriteLine("The initial capacity of arraylist =" + arrlists.Capacity);
    Console.WriteLine("The initial elements are =" + arrlists.Count);
    Console.WriteLine("Enter Details of Student 1");
    Console.WriteLine("___________________________");
    Console.Write("Enter Name of Student1 : ");
    studname1 = Console.ReadLine();
    Console.Write("Enter Class of Student1 : ");
    classname1 = Console.ReadLine();
    Console.Write("Enter Roll No. of Student1 : ");
    rollno1 = Console.ReadLine();
    Console.WriteLine("___________________________");
    Console.Write("Enter Name of Student2 : ");
    studname2 = Console.ReadLine();
    Console.Write("Enter Class of Student2 : ");
    classname2 = Console.ReadLine();
    Console.Write("Enter Roll No. of Student2 : ");
    rollno2 = Console.ReadLine();
    Console.WriteLine("___________________________");
    Console.Write("Enter Name of Student3 : ");
    studname3 = Console.ReadLine();
    Console.Write("Enter Class of Student3 : ");
    classname3 = Console.ReadLine();
    Console.Write("Enter Roll No. of Student3 : ");
    rollno3 = Console.ReadLine();
    Console.WriteLine("___________________________");
    arrlists.Add(studname1);
    arrlists.Add(classname1);
    arrlists.Add(rollno1);
    arrlists.Add(studname2);
    arrlists.Add(classname2);
    arrlists.Add(rollno2);
    arrlists.Add(studname3);
    arrlists.Add(classname3);
    arrlists.Add(rollno3);
    Console.WriteLine("Current Capacity=" + arrlists.Capacity);
    Console.WriteLine("ArrayList having elements = " + arrlists.Count);
    Console.Write("ArrayList is having content:-");
    for (int i = 0; i < arrlists.Count; i++)
    {
        Console.Write(arrlists[i] + " ");
    }
    Console.WriteLine("\n");
    Console.WriteLine("To remove 2nd student details press y or to interchange student details1 with student details3 press n.");
```

