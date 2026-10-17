
| 运算符 | 符号 | 描述 |
|---|---|---|
| 逻辑 OR | <code>&#124;</code> | 计算其布尔操作数的逻辑 OR。对于整数操作数，<code>&#124;</code> 比较两个整数的对应位并计算操作数的逻辑按位 OR。只有当任一操作数为 `true` 时才返回 `true`。 |
| 条件 AND | `&&` | 计算其布尔操作数的逻辑 AND。它在必要时求值第二个操作数，并且仅当两个操作数都为 `true` 时才返回 `true`。 |
| 条件 OR | <code>&#124;&#124;</code> | 计算其布尔操作数的逻辑 OR。它在必要时求值第二个操作数，并且仅当任一操作数为 `true` 时才返回 `true`。 |
| 条件 | `?:` | 根据布尔表达式产生的结果返回两个值之一。 |
| 赋值 | `=` | 将值赋给变量、属性或索引器。 |
| 赋值 | `+=` | 将第一个操作数和第二个操作数的和的结果赋给第一个操作数。 |
| 赋值 | `-=` | 将第一个操作数和第二个操作数的差的结果赋给第一个操作数。 |
| 赋值 | `*=` | 将第一个操作数和第二个操作数的乘积的结果赋给第一个操作数。 |
| 赋值 | `/=` | 将第一个操作数除以第二个操作数的除法结果赋给第一个操作数。 |
| 赋值 | `%=` | 将第一个操作数除以第二个操作数的余数赋给第一个操作数。 |
| 赋值 | `&=` | 将第一个操作数和第二个操作数的逻辑 AND 赋给第一个操作数。 |
| 赋值 | <code>&#124;=</code> | 将第一个操作数和第二个操作数的逻辑 OR 赋给第一个操作数。 |
| 赋值 | `^=` | 将第一个操作数和第二个操作数的逻辑 XOR 赋给第一个操作数。 |
| 赋值 | `<<=` | 将第一个操作数和第二个操作数的左移结果赋给第一个操作数。 |
| 赋值 | `>>=` | 将第一个操作数和第二个操作数的右移结果赋给第一个操作数。 |
| 空合并 | `??` | 根据空值返回两个值之一。如果其值不为空则返回左操作数；否则返回右操作数。 |
| Lambda | `=>` | 将其左侧的输入变量与其右侧的语句或表达式分隔开。 |
| 作用域解析 | `::` | 定义指定标识符的访问范围 |

由于 C# 中的每个运算符在表达式中都有其自身的值；因此，C# 为它们提供了一个优先级级别，允许 C# 编译器以特定顺序执行表达式。凭借 C# 中大量的运算符，您可以在一个表达式中同时使用其中许多运算符来执行所需的计算。然而，使用两个或多个运算符可能会导致运算符优先级的冲突，即哪个操作先执行。为此，C# 将优先级与每个运算符关联起来，以定义具有这些运算符的表达式的求值顺序。运算符优先级是一组规则，指定编译器求值表达式的顺序。运算符与表达式的左侧或右侧相关联，这称为运算符的结合性。表 2.7 列出了 C# 中不同运算符的优先级：

#### 表 2.7：显示运算符优先级

| 运算符 | 结合性 |
|---|---|
| `(x), (x,y), f(x), a[x], x++, x--, new, typeof, sizeof, checked, unchecked` | 左 |
| `+（一元）, -（一元）, ~, ++x, --x, (T)x` | 左 |
| `*, /, %` | 左 |
| `+（算术）, -（算术）` | 左 |
| `<<, >>` | 左 |
| `<, >, <=, >=, is, as` | 左 |
| `==, !=` | 左 |
| `&` | 左 |
| `^` | 左 |
| <code>&#124;</code> | 左 |
| `&&` | 左 |
| <code>&#124;&#124;</code> | 左 |
| `?:` | 右 |
| `=`, `*=`, `/=`, `%=`, `+=`, `-=`, `<<=`, `>>=`, `&=`, `^=`, <code>&#124;=</code> | 右 |

在表 2.7 中，同一级别的运算符具有相同的优先级，并在表达式中按给定顺序求值，直到且除非由括号分隔。

现在，让我们继续进入即时解决方案部分，以了解在深入部分讨论的概念的实际实现。

## 即时解决方案

### 声明变量

如前所述，变量用于存储值。变量有两种类型，输入和输出。输入变量用于从用户获取输入；而输出变量用于存储输出结果并向用户显示数据。现在，为了了解变量的声明，让我们创建一个名为 `DeclaringVariable` 的新 C# 2010 控制台应用程序（也可在 CD-ROM 上获得）。执行以下步骤创建 `DeclaringVariable` 应用程序并在其中声明变量：

1. 通过单击 开始 → 所有程序 → Microsoft Visual Studio 2010 → Microsoft Visual Studio 2010 打开 Visual Studio 2010 IDE。

2. 在菜单栏上选择 文件 → 新建 → 项目。会出现新建项目对话框，如图 2.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_131_0.png)

#### 图 2.1：从新建项目对话框中选择项目类型

3. 从已安装模板窗格中选择 Visual C# → Windows（图 2.1）。

4. 从模板列表中选择控制台应用程序模板（图 2.1）。

5. 在名称文本框中为您的应用程序输入名称（图 2.1）。在本例中，我们输入了 `DeclaringVariable`。

6. 在位置组合框中输入要保存应用程序的文件夹的完整路径（图 2.1）。在本例中，我们输入了 `D:\CSharp 2010 Black book Platinum Edition\Chapter 02\Code\`。

7. 单击确定按钮（图 2.1）。这将创建一个新的控制台应用程序，如图 2.2 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_132_0.png)

#### 图 2.2：显示新的控制台应用程序

8. 将清单 2.6 中给出的代码添加到应用程序的 `Program.cs` 文件中：

#### 清单 2.6：显示 `Program.cs` 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace DeclaringVariable
{
    class Program
    {
        static void Main(string[] args)
        {
            short x;    //Declaring short type variable
            int y;      //Declaring integer type variable
            double z;   //Declaring double type variable
            x = 6;
            y = 10;
            z = x + y;
            Console.WriteLine("x = {0}, Y = {1}, Z = {2}", x, y, z);
            Console.ReadLine();
        }
    }
}
```

在清单 2.6 中，我们声明了一些变量，为它们赋值，然后打印结果。我们调用了 `System.Console` 对象的 `WriteLine()` 方法来显示变量的值。清单 2.6 的输出如图 2.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_132_1.png)

#### 图 2.3：显示 `DeclaringVariable` 应用程序的输出

### 初始化变量

创建变量后，必须用某个值对其进行初始化。变量可以通过多种方式初始化——在声明时，在应用程序中使用固定值，或者将另一个变量的值复制到其中。现在，让我们按照本章前面“声明变量”标题下给出的步骤，创建一个新的 C# 2010 控制台应用程序，名为 `InitializingVariable`（也随附于 CD-ROM）。创建 `InitializingVariable` 应用程序后，在其 `Program.cs` 文件中添加清单 2.7 中所示的代码以初始化变量：

#### 清单 2.7：显示 `Program.cs` 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace InitializingVariable
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a variable at declaration
            short x = 5;
            // Initialize a variable as a copy of another
            int y = x;
            double z = y + 10.25; //assigning an integer value with a floating-point value
            int a = (int)z; // converting the floating-point number to integer
            Console.WriteLine("X = {0} Y = {1} Z = {2}", x, y, z);
            Console.WriteLine("A = {0}", a);
            Console.ReadLine();
        }
    }
}
```

在清单 2.7 中，我们将一个整数值与一个浮点值的和赋给了一个浮点变量。接下来，我们将浮点数转换成了整数。此转换需要显式强制转换，因为它在执行期间可能会丢失精度。

假设你将清单 2.7 中的语句 `int a = (int)z;` 写成如下代码片段所示：

```
int a = z;
```

当你使用上述代码片段运行应用程序时，编译器会生成错误消息“无法将类型 'double' 隐式转换为 'int'”。通过强制你显式地将浮点数转换为整数，编译器确保你了解自己操作的后果。在应用程序中，无效转换引入了错误，这些错误造成了严重损害且难以追踪，这样的情形数不胜数。

清单 2.7 的输出如图 2.4 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_133_0.png)

#### 图 2.4：显示 `InitializingVariable` 应用程序的输出

现在，让我们学习如何声明常量。

### 声明常量

在创建 C# 应用程序时，有时需要为变量设置固定值。该值在应用程序的整个执行过程中不能更改。常量主要用于执行数学计算，其中 e、pi、√2、√3 等值已预先计算。现在，让我们按照本章前面“声明变量”标题下给出的步骤，创建一个新的 C# 2010 控制台应用程序，名为 `Constants`（也随附于 CD）。`Constants` 应用程序演示了如何在应用程序中声明和初始化常量值。在 `Program.cs` 文件中添加清单 2.8 中所示的代码：

#### 清单 2.8：显示 `Program.cs` 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Constants
{
    class Program
    {
        static void Main(string[] args)
        {
            const double pi = 3.1472; //Declaring constant variable
            int r;
            Console.WriteLine("Enter the value of r");
            r = int.Parse(Console.ReadLine());
            double circleArea = pi * r * r;
            Console.WriteLine("The area of circle is " + circleArea);
            Console.ReadLine();
        }
    }
}
```

在清单 2.8 中，我们使用 `const` 关键字声明了一个 `double` 数据类型的常量变量 `pi`。`const` 关键字的使用表明 `pi` 变量的值是常量，即 3.1472。

清单 2.8 的输出如图 2.5 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_134_0.png)

#### 图 2.5：显示 `Constants` 应用程序的输出

现在，让我们学习如何声明可空类型变量。

### 声明可空类型变量

你可以将正常范围的值以及 `null` 值赋给可空类型。这些值是为可空类型的底层值类型指定的。例如，你可以将 -2147483648 到 2147483647 范围内的值或 `null` 值赋给 `Nullable<Int32>`（读作 nullable of Int32）。你可以将值 `true`、`false` 或 `null` 赋给 `Nullable<bool>`。为了更好地理解这个概念，让我们按照本章前面“声明变量”标题下给出的步骤，创建一个新的 C# 2010 控制台应用程序，名为 `NullableTypes`（也随附于 CD-ROM）。创建 `NullableTypes` 应用程序后，在其 `Program.cs` 文件中添加清单 2.9 中所示的代码：

#### 清单 2.9：显示 `NullableTypes` 应用程序的 `Program.cs` 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace NullableTypes
{
    class Program
    {
        static void Main(string[] args)
        {
            int? var1 = null; //Declaring nullable type variable
            int var2 = 5;
            var1 = var2;  //valid
            // int? is Nullable where underlying type is int
            if (var1.HasValue == true)
            {
                Console.WriteLine("var1 = " + var1.Value);
            }
            else
            {
                Console.WriteLine("var1 = Null");
            }
            Console.ReadLine();
        }
    }
}
```

在清单 2.9 中，`var1` 的值在控制台上打印为 5。这是因为 `var2` 的值被赋给了 `var1`。如果没有为 `var1` 赋值，则输出将显示为 `var1=null`。可空类型提供的 `HasValue` 属性检查 `null` 变量的值。清单 2.9 的输出如图 2.6 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_135_0.png)

#### 图 2.6：显示 `NullableTypes` 应用程序的输出

现在，让我们学习如何使用 `??`（空合并）运算符。

### 使用 `??`（空合并）运算符

空合并运算符（`??`）主要用于可空值类型和引用类型。`??` 运算符用在两个操作数之间，其中第一个操作数必须是可空类型。第二个操作数必须与第一个操作数类型相同，或者是可以隐式转换为第一个类型的类型。它检查第一个操作数的值是否为 `null`。如果第一个操作数的值为 `null`，则返回第二个操作数的值，否则返回第一个操作数的值。如果你将第二个操作数声明为无法隐式转换为第一个操作数类型的类型，则会生成编译时错误。现在，让我们创建一个新的 C# 2010 控制台应用程序，名为 `NullCoalescing`（也随附于 CD-ROM），以使 `??` 运算符的概念更加清晰。请按照本章前面“声明变量”标题下给出的步骤创建应用程序，并在应用程序的 `Program.cs` 文件中添加清单 2.10 中所示的代码，以使用空合并运算符：

#### 清单 2.10：显示使用空合并运算符的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace NullCoalescing
{
    class Program
    {
        static void Main(string[] args)
        {
            int? i = null; //Nullable variable
            int? j = 30;   //Nullable variable
            int k;
            k = i ?? 25; //Using ?? operator to check for null values
            Console.WriteLine("The value of k is " + k);
            k = j ?? 25; //Using ?? operator to check for null values
            Console.WriteLine("Now the value of k is " + k);
            Console.ReadLine();
        }
    }
}
```
