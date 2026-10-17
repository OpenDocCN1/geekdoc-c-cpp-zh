
在列表 2.10 中，我们声明了两个可空变量 `i` 和 `j`。这意味着 `i` 和 `j` 变量包含整数值或空值。我们已将空值赋给 `i` 变量，并将 30 的值赋给 `j` 变量。使用 `??` 运算符在 `k = i ?? 25` 语句中，编译器会检查 `i` 的值是否为空。由于 `i` 的值为空，因此返回右操作数的值。同样在 `k = j ?? 25` 语句中，`j` 的值为 30，不是空。因此，`j` 的值被赋给 `k` 变量。列表 2.10 的输出如图所示 2.7：

![](img/e073a4882197be4ab61103cbe0bcb394_136_0.png)

图 2.7：显示 NullCoalescing 应用的输出

让我们在下一节学习变量的作用域。

## 指定变量的作用域

C# 有多个变量级别，包括不同种类变量的不同作用域。如讨论所述，您可以在局部或类级别声明变量。让我们通过执行“声明变量”标题下给出的步骤，创建一个名为 `ScopingVariable` 的新 C# 2010 控制台应用程序（也可在 CD-ROM 上获得），以学习如何指定变量的作用域。创建应用程序后，将列表 2.11 中给出的代码添加到 `ScopingVariable` 应用程序的 `Program.cs` 文件中：

### Listing 2.11: 显示 ScopingVariable 应用程序的 Program.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ScopingVariable
{
    class Program
    {
        static int x = 10;
        static void Main(string[] args)
        {
            // Locally defined copy of x
            int x = 5;
            int y = x;
            double z = y + 10.25;
            int a = (int)z;
            // Output x, which one gets written?
            Console.WriteLine("X = {0} Y = {1} Z = {2}", x, y, z);
            Console.WriteLine("A = {0}", a);
            // Force the output of the class level x variable
            Console.WriteLine("Class Level X = {0}", Program.x);
            Console.ReadLine();
        }
    }
}
```

在列表 2.11 中，`x` 变量被声明了两次。在第一次声明时，`x` 持有值 10 并被声明为整个程序中的静态变量。由于 `x` 在 `Main` 函数之外声明，因此它充当全局变量。然而，当您用相同名称 `x` 声明变量时，它充当局部变量，并且在任何上下文中都与全局 `x` 无关。`x` 变量（`int x = 5`）的范围仅限于 `Main()` 方法。列表 2.11 的输出如图所示 2.8：

![](img/e073a4882197be4ab61103cbe0bcb394_136_1.png)

图 2.8：显示 ScopingVariable 应用程序的输出

现在，让我们学习如何使用作用域解析运算符。

## 使用作用域解析运算符 (::)

`::`（作用域解析）运算符被添加到两个标识符之间以定义它们的作用域。现在，让我们通过执行本章前面“声明变量”标题下给出的步骤，创建一个名为 `AliasClass` 的新 C# 2010 控制台应用程序（也可在 CD-ROM 上获得）。`AliasClass` 应用程序展示了 `::` 运算符与全局标识符一起使用。列表 2.12 显示了 `AliasClass` 应用程序的代码：

### Listing 2.12: 显示 AliasClass 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace AliasClass
{
    class Program
    {
        public class System
        {
            public void Print()
            {
                global::System.Console.WriteLine("This is an example of :: operator");
            }
        }
        // Define a constant 'Console'
        const string Console = "Hello";
        const string str1 = "World";
        static void Main(string[] args)
        {
            // Error Accesses TestApp.Console
            System sys = new System();
            sys.Print();
            global::System.Console.WriteLine(Console);
            global::System.Console.WriteLine(str1);
            global::System.Console.ReadLine();
        }
    }
}
```

在列表 2.12 中，我们使用 `::` 运算符与 `global` 标识符一起使用，以在应用程序中全局访问标识符。列表 2.12 的输出如图所示 2.9：

![](img/e073a4882197be4ab61103cbe0bcb394_137_0.png)

图 2.9：显示 AliasClass 应用程序的输出

现在，让我们学习如何声明和初始化字符串。

## 声明和初始化字符串

除了将字符串仅用作字符数组外，您还可以使用字符串表示 Unicode 字符的字符串。您可以使用 `string` 关键字声明字符串变量。`string` 关键字是 `System.String` 类的别名。现在，让我们通过执行本章前面“声明变量”标题下给出的步骤，创建一个名为 `Strings` 的 C# 2010 控制台应用程序（也可在 CD-ROM 上获得）。`Strings` 应用程序展示了如何声明和初始化字符串变量。将列表 2.13 中显示的代码添加到 `Strings` 应用程序的 `Program.cs` 文件中以声明和初始化字符串：

### Listing 2.13: 显示声明和初始化字符串的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Strings
{
    class Program
    {
        static void Main(string[] args)
        {
            string str;                 //Declaring a string variable
            str = "Kogent Learning Solutions";  //Initializing the string
            Console.WriteLine("The value of the string variable is " + str);
            Console.ReadLine();
        }
    }
}
```

在列表 2.13 中，我们声明并初始化了一个名为 `str` 的字符串变量。列表 2.13 的输出如图所示 2.10：

![](img/e073a4882197be4ab61103cbe0bcb394_138_0.png)

图 2.10：显示输出 Strings 应用程序

需要注意的是，在初始化字符串变量时，值用双引号括起来。如果您用单引号括住值，编译器会将值视为 `char` 并抛出错误。

## 操作字符串

`System.String` 类提供了一组不同的方法来操作字符串，例如更改字符串的大小写和添加两个或多个字符串。假设您有两个或多个字符串，您想将它们相加，或者您想要某个字符串文字的反转，或者您想要查找字符串的长度。您可以通过简单地创建字符串数据类型并使用点运算符（`.`）来获取字符串功能，对字符串执行所有这些操作。为了使字符串的概念更清晰，让我们通过执行本章前面“声明变量”标题下给出的步骤，创建一个名为 `StringManipulating` 的新 C# 2010 控制台应用程序（也可在 CD-ROM 上获得）。`StringManipulating` 应用程序使用不同的方法操作字符串文字。列表 2.14 显示了 `StringManipulating` 应用程序的完整代码：

### Listing 2.14: 显示 StringManipulating 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace StringManipulating
{
    class Program
    {
        static void Main(string[] args)
        {
            string fname;  //Declaring a string variable
            string mname;  //Declaring a string variable
            string lname;  //Declaring a string variable
            Console.WriteLine("Enter your first name");
            fname = Console.ReadLine();
            Console.WriteLine("Enter your middle name");
            mname = Console.ReadLine();
            Console.WriteLine("Enter your last name");
            lname = Console.ReadLine();
            string completename = fname + "\t" + mname + "\t" + lname; //Concatenating the string values
            Console.WriteLine("Your complete name is " + completename);
            Console.WriteLine("");
            Console.WriteLine("Your name in UPPERCASE is " +
            completename.ToUpper();//Converting to UPPERCASE
            Console.WriteLine("");
            Console.WriteLine("Enter the new first name with which you want to replace your previous first name");
            string newname = Console.ReadLine();
            Console.WriteLine("The new name is " + completename.Replace(fname, newname));//Replacing string
            Console.ReadLine();
        }
    }
}
```

在列表 2.14 中，我们声明了五个字符串变量，名为 `fname`、`mname`、`lname`、`completename` 和 `newname`。`fname`、`mname` 和 `lname` 的值是从用户输入中获取的。`completename` 变量存储 `fname`、`mname` 和 `lname` 变量的连接值。`completename.ToUpper()` 方法将 `completename` 中的值大小写转换为大写。同样，`completename.Replace(fname,newname)` 方法用存储在 `newname` 中的新输入名称替换 `completename` 中的 `fname` 值。

列表 2.14 的输出如图所示 2.11：

![](img/e073a4882197be4ab61103cbe0bcb394_139_0.png)

现在，让我们学习如何将一种数字类型转换为另一种数字类型。

## 将一种数字类型转换为另一种数字类型

将数字从一种类型转换为另一种类型的任务是一个复杂任务。有时，您只想转换给定类型以获取其整数部分。其他时候，您可能想将字符串转换为数字，或者您可能想以类型安全的方式直接将一种类型转换为另一种类型。C# 已考虑到所有这些因素，并提供了处理数字的方法。之前，您已使用 C 转换方法，即简单地将一种类型强制转换为另一种类型。

如果您以非类型安全的方式转换一种类型，例如直接强制转换，编译器无法验证您正在转换的类型是否彼此合法。

现在，让我们通过执行本章前面“声明变量”标题下给出的步骤，创建一个名为 `Conversion` 的新 C# 2010 控制台应用程序（也可在 CD-ROM 上获得）。在此应用程序中，您将看到如何将一种数字类型转换为另一种数字类型。创建应用程序后，将列表 2.15 中显示的代码添加到 `Conversion` 应用程序的 `Program.cs` 文件中：

### Listing 2.15: 显示将一种数字类型转换为另一种数字类型的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Conversion
{
    class Program
    {
        static void Main(string[] args)
        {
            string str1 = "123.45";
            // Converting str1 to a real floating point
            Single sngl1 = Convert.ToSingle(str1);
            // Converting str1 to an integer
            int x = Convert.ToInt16(sngl1);
            Console.WriteLine("Single 1 = {0}", sngl1);
            Console.WriteLine("Integer 1 = {0}", x);
            // Converting str1 to double
            double y = Convert.ToDouble(str1);
            Console.WriteLine("double = {0}", y);
            Int16 z = Convert.ToInt16(y);
            Console.WriteLine("Int16 = {0}", z);
            Console.ReadLine();
        }
    }
}
```

在清单 2.15 中，`Convert.ToSingle(str1)` 方法将字符串类型转换为 `Single` 类型。使用 `Convert.ToInt(sngl1)` 方法，将 `Single` 类型转换为整数类型。`Convert.ToDouble(str1)` 方法将字符串类型转换为 `double` 类型，而 `Convert.ToInt16(y)` 将 `double` 类型转换为 `Int16` 类型。由于整数类型不包含小数部分；因此，`Integer` 和 `Int16` 变量都省略了小数部分，仅存储 123。清单 2.15 的输出如图所示 2.12：

![](img/e073a4882197be4ab61103cbe0bcb394_140_0.png)

图 2.12：显示转换应用程序的输出

现在，让我们学习如何将字符串类型转换为数字类型。

## 将字符串类型转换为数字类型

在创建 C# 应用程序时，有时需要将以文本数据形式输入的输入转换为数字格式，以便对其进行计算。这样的情况的一些示例包括从文本文件读取行并将其转换为数字，以及使用表单从用户读取输入，然后将这些输入文本字符串转换为数字，以便进行比较和计算。

在 C# 中，要将字符串转换为其他数据类型，可以使用字符串类内置的转换函数。现在，让我们通过执行本章前面“声明变量”标题中给出的步骤，创建一个名为 `StringToNumber` 的新 C# 2010 控制台应用程序（也可在 CD-ROM 上获得）。

### 清单 2.16：显示 StringToNumber 应用程序的代码
