
- 参数的数据类型
- 参数传递的顺序

以下代码片段展示了方法 Display() 的两个重载版本：

```
void Display(string name)
{
    Console.WriteLine("Name: " + name);
}
void Display(string name, int marks)
{
    Console.WriteLine("Name: " + name);
    Console.WriteLine("Marks: " + marks);
}
```

在上述代码片段中，Display() 方法的第一个重载版本只接受一个 string 类型的参数。Display() 方法的第二个重载版本接受两个参数，一个是 string 类型，另一个是 int 类型。

执行以下步骤来实现方法重载：

- 1. *启动* Visual Studio 2010。
- 2. 在菜单栏中*选择* **文件→新建→项目**。此时将打开“新建项目”对话框。
- 3. 在 **新建项目** 对话框左侧窗格的 **已安装模板** 部分中，*选择* **Visual C#→Windows**。可用于在 Visual C# 中开发 Windows 应用程序的项目模板将显示在 **新建项目** 对话框的右侧窗格中。
- 4. 从右侧窗格中*选择* **控制台应用程序**，以创建控制台应用程序。
- 5. 在 **名称** 文本框中输入应用程序名称 **MethodOverloading**（也可在随附 CD 上获得），并在 **位置** 文本框中为应用程序选择适当的位置。
- 6. 单击 **确定** 按钮，关闭 **新建项目** 对话框并创建 **MethodOverloading** 应用程序。
- 7. 将清单 2.10 中显示的突出显示的代码片段*添加*到 **Program.cs** 文件中：

### 清单 2.10：实现方法重载

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MethodOverloading
{
    public class Shape
    {
        public void Area(int side)
        {
            Console.WriteLine("The area of the square is: " + (side * side));
        }
        public void Area(int length, int breadth)
        {
            Console.WriteLine("The area of the rectangle is: " + (length * breadth));
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Shape obj = new Shape();
            obj.Area(15);
            obj.Area(10, 20);
            Console.ReadLine();
        }
    }
}
```

清单 2.10 中的第一段突出显示的代码片段展示了 Shape 类的定义。Shape 类定义了名称同为 Area 的两个不同的方法。第一个 Area() 方法接受一个 int 类型参数，计算并显示正方形的面积。第二个 Area() 方法接受两个 int 类型参数，计算并显示长方形的面积。在第二段突出显示的代码片段中，我们创建了 Shape 类的一个对象 obj。之后，我们借助 obj 对象调用了 Area() 方法：先传入一个整数参数，再传入两个整数参数。第一次调用 Area() 方法显示正方形的面积，第二次调用 Area() 方法显示长方形的面积。

- 8. 按键盘上的 F5 键运行应用程序。应用程序的输出如图 C#-2.11 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_342_0.png)

图 C#-2.11

## 运算符重载

C# 中的所有运算符都有其特定的含义和功能；例如，+ 运算符将两个数值相加，- 运算符将两个数值相减。然而，有时您可能需要更改运算符的默认功能。例如，您可能希望使用 + 运算符将两个复数相加。如您所知，复数由实数和虚数组成；因此，不能直接使用 + 运算符将两个复数相加。在这种情况下，可以使用运算符重载为现有运算符赋予新的含义和功能。运算符重载是一种在运算符已有功能之外再为其赋予新功能的机制。

在 C# 2010 中，并非所有运算符都可以重载。表 2.2 显示了不同运算符的重载行为：

| 运算符 | 类型 | 重载行为 |
|---|---|---|
| `+`, `-`, `~`, `!`, `++`, `--`, `true`, `false` | 一元 | 可以重载 |
| `+`, `-`, `*`, `/`, `%`, `&`, `\|`, `^`, `<<`, `>>` | 二元 | 可以重载 |
| `==`, `!=`, `<`, `>`, `<=`, `>=` | 比较 | 可以重载，但只能成对重载，如 `==` 和 `!=`，`<` 和 `>` |
| `&&`, `\|\|` | 条件逻辑 | 不能重载，但可以使用 `&` 和 `\|` 运算符进行计算 |
| `[]` | 数组索引 | 不能重载，但可用于定义索引器 |
| `()` | 强制转换 | 不能重载 |
| `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `\|=`, `^=`, `<<=`, `>>=` | 赋值 | 不能重载 |
| `??`, `?:`, `->`, `new`, `is`, `sizeof`, `typeof` | 其他 | 不能重载 |

执行以下步骤实现运算符重载：

- 1. 启动 Visual Studio 2010。
- 2. **选择** 菜单栏中的 文件→新建→项目。此时将打开“新建项目”对话框。
- 3. 在“新建项目”对话框左侧窗格的 **已安装模板** 部分中，**选择** Visual C#→Windows。可在 Visual C# 中用于开发 Windows 应用程序的项目模板显示在“新建项目”对话框的右侧窗格中。
- 4. 从右侧窗格中**选择** 控制台应用程序，以创建控制台应用程序。
- 5. 在 **名称** 文本框中**输入**应用程序名称 **OperatorOverloading**（也可在随附 CD 上获得），并在 **位置** 文本框中为应用程序选择适当的位置。
- 6. **单击** **确定** 按钮，关闭“新建项目”对话框并创建 **OperatorOverloading** 应用程序。
- 7. 将清单 2.11 中显示的突出显示的代码片段**添加**到 **Program.cs** 文件中：

### 清单 2.11：实现运算符重载

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace OperatorOverloading
{
    class Complex
    {
        int x, y;
        public Complex(int real, int imag)
        {
            x = real;
            y = imag;
        }
        public static Complex operator +(Complex c1, Complex c2)
        {
            Complex c3 = new Complex(c1.x + c2.x, c1.y + c2.y);
            return c3;
        }
        public override string ToString()
        {
            return x + "+i" + y;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Complex a = new Complex(5, 4);
            Complex b = new Complex(3, 2);
            Complex c = a + b;
            Console.WriteLine("a = " + a.ToString());
            Console.WriteLine("b = " + b.ToString());
            Console.WriteLine("Sum of a and b = " + c.ToString());
            Console.ReadLine();
        }
    }
}
```

清单 2.11 中的第一段突出显示的代码片段展示了 Complex 类的定义。在 Complex 类中，我们首先定义了两个 int 类型变量和一个用于初始化这些变量的构造函数。之后，我们定义了一个运算符方法来重载 + 运算符。该运算符方法将两个 Complex 类型对象作为参数，通过分别将两个对象的实部和虚部相加，返回一个新的 Complex 类型对象。接下来，我们重载了 ToString() 方法，以便在屏幕上显示 Complex 类型对象。在第二段突出显示的代码片段中，我们创建了两个 Complex 类型对象 a 和 b。之后，我们使用 + 运算符的重载版本将 a 和 b 对象相加，并将结果赋给另一个 Complex 类型对象 c。最后，我们在屏幕上显示 a、b 对象以及它们的和。

- 8. *按下*键盘上的 F5 键运行应用程序。应用程序的输出如图 C#-2.12 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_344_0.png)

图 C#-2.12

## 运行时多态

运行时多态，也称为方法重写，允许您创建可在派生类中重写的虚方法。在基类中创建虚方法之后，该基类的任何派生类都可以为虚方法提供新的实现。在 C# 中，**virtual** 关键字用于声明虚方法，**override** 关键字用于声明重写虚方法的方法。新方法将替换派生类中虚方法的实现。之所以称为运行时多态，是因为在运行时多态中，编译器在程序执行期间将方法绑定到对象，而不是在程序编译期间。

执行以下步骤实现方法重写：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中*选择* 文件→新建→项目。此时将打开 **新建项目** 对话框。
- 3. 在 **新建项目** 对话框左侧窗格的 **已安装模板** 部分中，*选择* Visual C#→**Windows**。可用于在 Visual C# 中开发 Windows 应用程序的项目模板将显示在 **新建项目** 对话框的右侧窗格中。
- 4. 从右侧窗格中*选择* **控制台应用程序**，以创建控制台应用程序。
- 5. 在 **名称** 文本框中输入应用程序名称 **MethodOverriding**（也可在随附 CD 上获得），并在 **位置** 文本框中为应用程序选择适当的位置。
- 6. *单击* **确定** 按钮，关闭 **新建项目** 对话框并创建 **MethodOverriding** 应用程序。
- 7. 将清单 2.12 中显示的突出显示的代码片段*添加*到 **Program.cs** 文件中：

### 清单 2.12：实现方法重写

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MethodOverriding
{
    public class Animal
    {
        public virtual void Sleep()
        {
            Console.WriteLine("The animal is sleeping...");
        }
    }
    public class Dog : Animal
    {
        public override void Sleep()
        {

```
