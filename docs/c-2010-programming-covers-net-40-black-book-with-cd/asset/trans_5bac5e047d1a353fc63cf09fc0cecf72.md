

# 即时解决方案

## 创建指向 int 数据类型的指针

指针是保存其他值类型变量地址的变量，例如 int 和 char。让我们创建一个名为 MyPointer 的控制台应用程序（也在 CD 上提供），它展示了如何创建指向 int 数据类型的指针。图 6.1 显示了 MyPointer 应用程序的 Program.cs 文件的代码：

### 列表 6.1：创建指向 int 数据类型的指针

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyPointer {
class Program {
    unsafe static void Main(string[] args) {
        int Number = 100;
        int* MyPointer;
        MyPointer = &Number;
        {
        Console.WriteLine("The value of 'Number' is: "+Number);
        Console.WriteLine("The value of 'MyPointer' is: "+(int)MyPointer);
        Console.WriteLine("\n");
        Console.WriteLine("Press ENTER to quit.....");
        Console.Read();
        }
    }
}
```

在列表 6.1 中，我们创建了一个整数指针 MyPointer，它保存了一个名为 Number 的整数变量的内存地址。

要执行包含指针的任何应用程序，首先需要在 Visual Studio 2010 中更改设置。为此，请执行以下步骤：

- 1. 在解决方案资源管理器中选择并右键单击项目名称，在本例中为 MyPointer，然后从上下文菜单中选择属性选项。

MyPointer 属性窗口出现，如图 6.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_261_0.png)

图 6.1：显示 MyPointer 属性窗口

- 2. 在 MyPointer 属性窗口中选择生成选项卡。
- 3. 选择允许不安全代码复选框，如图 6.2 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_262_0.png)

图 6.2：选择允许不安全代码复选框

- 4. 关闭 MyPointer 属性窗口。
- 5. 按键盘上的 F5 键运行 MyPointer 应用程序。
- MyPointer 应用程序的输出出现，如图 6.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_262_1.png)

图 6.3：显示 MyPointer 应用程序的输出

> 注意
> 您也可以使用 C# 编译器执行包含指针的应用程序。为此，首先需要使用 /unsafe 关键字编译程序（csc），然后在命令提示符下运行应用程序。

让我们现在学习如何取消引用指针。

## 取消引用指针

取消引用指针意味着访问指针变量所保存的值。指针的取消引用是通过取消引用运算符（*）完成的。正如地址运算符（&）返回变量的地址一样，取消引用运算符（*）返回由（&）运算符保存的内存地址上的值。让我们创建一个名为 Dereference 的控制台应用程序（也在 CD 上提供），它展示了如何取消引用指针。列表 6.2 显示了 Dereference 应用程序的 Program.cs 文件的代码：

### 列表 6.2：显示 Program.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Dereference
{
    class Program
    {
```

```
unsafe static void Main(string[] args)
{
    int Number = 100;
    int* MyPointer;
    MyPointer = &Number;
    Console.WriteLine("Old values:");
    Console.WriteLine("Number: " + Number);
    Console.WriteLine("MyPointer: " + (int)MyPointer);
    Console.WriteLine("*MyPointer: " + *MyPointer);
    *MyPointer = 50;
    Console.WriteLine("--------------------------");
    Console.WriteLine("New values:");
    Console.WriteLine("Number: " + Number);
    Console.WriteLine("MyPointer: " + (int)MyPointer);
    Console.WriteLine("*MyPointer: " + *MyPointer);
    Console.Read();
}
```

在列表 6.2 中，您可以看到指针变量 *MyPointer 保存了由 &MyPointer 保存的内存地址上的值。

图 6.4 显示了前述代码的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_263_0.png)

图 6.4：取消引用指针

注意
每次执行应用程序时，指针的值在系统上都会发生变化。

让我们现在学习如何使用指针指向数组。

## 使用指针指向数组

在 C# 中，您可以使用指针访问数组元素。让我们创建一个名为 PointersToArray 的控制台应用程序（也在 CD 上提供），它展示了如何使用指针访问数组的元素。列表 6.3 显示了 PointersToArray 应用程序的 Program.cs 文件的代码：

### 列表 6.3：显示 Program.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace PointerToArray
{
    class MyClass
    {
        public unsafe void MyMethod()
        {
            int[] MyArray = new int[10];
            for (int Counter = 0; Counter < 10; Counter++)
            {
                MyArray[Counter] = Counter * Counter;
            }
            fixed (int* MyPointer = MyArray)
            ShowData(MyPointer);
        }
        public unsafe void ShowData(int* ptr)
        {
            for (int i = 0; i < 10; i++)
```

```
{
    Console.WriteLine(*(ptr + i));
}
}
class MainClass
{
    public static void Main()
    {
        MyClass myclass = new MyClass();
        myclass.MyMethod();
        Console.WriteLine("\n");
        Console.WriteLine("Press ENTER to quit...");
        Console.Read();
    }
}
```

在列表 6.3 中，我们创建了一个名为 MyArray[] 的整数数组和一个名为 MyPointer 的指针变量，通过它我们可以访问 MyArray[] 数组的元素。

图 6.5 显示了前述代码的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_264_0.png)

图 6.5：显示 PointertoArray 应用程序的输出

让我们现在学习如何使用指针指向结构。

## 使用指针指向结构

如果结构仅包含值类型作为其成员，则指针可与结构一起使用。指针可以使用指针运算符（->）访问结构的成员。让我们创建一个名为 PointersToStruct 的控制台应用程序（也在 CD 上提供），它展示了如何使用指针访问结构。列表 6.4 显示了 PointersToStruct 应用程序的 Program.cs 文件的代码：

### 列表 6.4：显示 Program.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace PointersToStruct
{
struct MyStruct {
    public double Length;
    public double Breadth;
    public double Height;
    public void SetDimensions()
    {
        Console.Write("Enter Length of Room (in meter):");
        Length = Convert.ToDouble(Console.ReadLine());
        Console.Write("Enter Breadth of Room (in meter):");
        Breadth = Convert.ToDouble(Console.ReadLine());
        Console.Write("Enter Height of Room (in meter):");
        Height = Convert.ToDouble(Console.ReadLine());
    }
    public void ShowVolume()
```

```
{
    double volume = (Length * Breadth * Height);
    Console.WriteLine("The Volume of Room is: " + volume + " cubic meter");
}
}
class MainClass
{
    public unsafe static void Main()
    {
        MyStruct mystruct = new MyStruct();
        MyStruct* mystruct1 = &mystruct;
        mystruct1->SetDimensions();
        mystruct1->ShowVolume();
        Console.WriteLine("\n");
        Console.WriteLine("Press ENTER to quit....");
        Console.Read();
    }
}
```

在列表 6.4 中，我们声明了一个名为 MyStruct 的结构，并使用 (->) 运算符访问其成员。图 6.6 显示了前述代码的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_265_0.png)

让我们现在学习如何使用指向指针的指针。

## 使用指向指针的指针

指向指针的指针变量保存另一个指针变量的地址。让我们创建一个名为 PointerToPointer 的控制台应用程序（也在 CD 上提供），它展示了如何使用指针指向另一个指针。列表 6.5 显示了 PointerToPointer 应用程序的 Program.cs 文件的代码：

### 列表 6.5：显示 Program.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace PointerToPointer
{
    class Program {
        unsafe static void Main(string[] args)
        {
            char FirstChar;
            char* SecondChar;
            char** ThirdChar;
            FirstChar = 'S';
            SecondChar = &FirstChar;
            ThirdChar = &SecondChar;
            Console.WriteLine("The value of FirstChar is: " + FirstChar);
            Console.WriteLine("The value of SecondChar is: {0}",(int)SecondChar);
            Console.WriteLine("The value of ThirdChar is: {0}",(int)ThirdChar);
            Console.WriteLine("\n");
            Console.WriteLine("Press ENTER to quit....");
            Console.Read();
        }
    }
}
```

在列表 6.5 中，我们声明了一个变量 FirstChar、一个指针变量 SecondChar 和一个指向指针的变量 ThirdChar，类型为 char。SecondChar 变量保存 FirstChar 变量的内存地址，而 ThirdChar 变量保存指针变量 SecondChar 的内存地址。图 6.7 显示了前述代码的输出：

