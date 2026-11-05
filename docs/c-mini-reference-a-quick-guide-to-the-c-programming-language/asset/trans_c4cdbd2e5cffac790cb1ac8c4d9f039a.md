
### 4.3.2. using static 指令

using static 指令导入某个类型的嵌套类型和静态成员，以便无需限定即可使用这些成员和类型的名称。

```csharp
using static TYPE_NAME;
```

例如，

```csharp
namespace Arithmetic {
    public class Adder {
        public static void Add(int a, int b) => a + b;
    }
}
namespace App {
    using static Arithmetic.Adder;
    class Calculator {
        public int Sum(int a, int b) => Add(a, b);
    }
}
```

### 4.3.3. using alias 指令

using alias 指令为最内层包含命名空间（或编译单元）内的某个命名空间或类型引入一个标识符（即别名）。由 using alias 指令引入的标识符可用于引用给定的命名空间或类型。

```csharp
using IDENTIFIER = NAMESPACE_OR_TYPE_NAME ;
```

例如，

```csharp
namespace Europe.Ukraine {
    public class Citizen ()
}
namespace World {
    using Person = Europe.Ukraine.Citizen;
    class Farmer: Person ()
}
```

## 4.4. 全局 using

通过关键字 global，可以使 using 声明在整个程序中生效。全局 using 声明可用于三种 using 声明类型中的任意一种：using namespace、using static 和 using alias。但是，全局 using 只能用于编译单元中，而不能用于显式声明的命名空间内，并且其作用域覆盖整个程序。例如，

```csharp
global using Machine;
global using static Robot.Arm;
global using Orange = Modern.Black;
```

## 4.5. 隐式 using

从 C# 10 开始，可以使用隐式 usings 功能，为正在构建的 C# 项目自动添加常用的全局 using 指令。“隐式”这一方面指的是，全局 using 指令会被添加到项目 obj 目录下的生成文件中。

例如，以下命名空间会通过 global 隐式声明

- System
- System.Collections.Generic
- System.IO
- System.Linq
- System.Net.Http
- System.Threading
- System.Threading.Tasks

## 4.6. 成员声明

如前所述，从 C# 9 及更高版本开始，可以在程序的某个源代码文件中使用顶级语句，以替代包含 Main 方法的类型，例如作为程序的入口点。除了这一例外（它仅仅是语法糖），命名空间（无论是显式声明还是其他方式）中的所有语句都必须是其他（嵌套）命名空间声明或类型声明。

类型声明是

- 类声明，
- 结构体声明，
- 记录声明，
- 枚举声明，
- 接口声明，或
- 委托声明。

可以使用访问修饰符显式控制对这些命名空间顶级类型声明的访问。否则，它们的默认访问级别是

## 5. C# 类型系统

C# 和 .NET 具有统一的类型系统。C# 语言中的每个类型都直接或间接继承自 .NET 上的 object 基类型。

C# 中的类型分为两大类：引用类型和值类型。值类型的变量可以直接包含其数据，而引用类型的变量存储对其数据的引用。只需将引用类型的值视为 object 类型，这些值就会被当作对象处理。另一方面，值类型的值通过执行装箱和拆箱操作而被当作对象处理。

泛型类型将在后面讨论。泛型类型参数可以指定值类型或引用类型。

### 5.1. 值类型

C# 的值类型可以分为简单类型、枚举类型、结构体类型（包括 record struct）和可空类型。简单类型包括内置的 bool 类型和其他数值类型。可空值类型可以包含 null 值。

默认情况下，在赋值、将参数传递给方法或返回方法结果时，值会被复制。但请注意，如果值类型包含引用类型的数据成员，则复制的是对该引用类型实例的引用。

### 5.1.1. System.ValueType 类型

值类型不能显式派生自其他类型。所有值类型都隐式继承自一个类，而该类本身不是值类型。它又继承自最终基类，

### 5.1.2. 默认构造函数

所有值类型都隐式声明一个称为默认构造函数的公共无参数实例构造函数。默认构造函数返回一个零初始化的实例，称为该类型的默认值

### 5.1.3. 装箱和拆箱

通过装箱和拆箱，任何类型的值（值类型或引用类型）都可以被当作对象处理。这提供了 C# 类型系统的统一视图。对值类型的值进行装箱会在堆上创建一个对象，可以通过引用变量引用该对象。拆箱执行相反的操作。也就是说，它返回给定变量所引用对象中包含的值。

### 5.1.4. 可空值类型

可空值类型 T? 除了可以表示其基础（不可空）值类型的所有值之外，还可以表示 null 值。此语法 T? 是泛型 System.Nullable 结构的简写形式。例如，可以将以下三个值中的任意一个赋给 bool? 变量：或 可空值类型 T? 的实例有两个公共只读属性：

```csharp
public bool HasValue { get; }
public T Value { get; }
```

### 5.2. 引用类型

C# 中的所有类型（包括引用类型）都派生自 .NET 基类。对于值类型，每个变量都有自己的数据副本。另一方面，对于引用类型，两个变量可以引用同一个对象。因此，对一个变量的操作可能会影响其他变量所引用的对象。

C# 提供了三种内置引用类型，此外，可以使用以下关键字声明自定义引用类型：

record（或 record

和

数组类型有些特殊，因为它们不必在使用前声明。数组类型是通过在类型名称后追加方括号构造的。例如，int[] 是 int 的（一维）数组，int[,] 是 int 的二维数组，int[][] 是 int 的数组的数组。

### 5.2.1. 可空引用类型

在可空引用类型上下文中，引用类型的所有变量都是不可空的。可以通过在类型名称后追加 ? 符号来显式声明可空变量，该符号表示可空引用类型。例如，

```csharp
string firstName = "Pele";
string? middleName = null;
```

①

变量 firstName 是不可空的。

②

string? 是引用类型 string 的可空对应形式。变量 middleName 是可空的。

对于可空引用类型，编译器使用流分析来确保在访问任何可空引用类型的变量之前，或在将其赋值给不可空引用类型之前，检查该变量是否为 null。

### 5.3. 动态类型

所有 C# 类型（内置或用户定义）都使用静态绑定。也就是说，变量或表达式的类型在编译时确定。dynamic 类型是一个例外。它在运行时使用动态绑定。在大多数情况下，dynamic 可以被视为与 object 相同（因为所有类型最终都继承自 object）。

例如，

```csharp
dynamic theSecret = 42;
dynamic theGreatestUnknown = "meh";
```

从语法上讲，dynamic 类型的表达式在运行时可以隐式转换为任何类型。但是，如果转换失败，则会引发运行时异常。如果不希望使用动态绑定，可以先将表达式转换为 object，然后再转换为所需类型。例如，

```csharp
dynamic realSecret = 42 * 42 * 42;
int huh = realSecret;
string cops = realSecret;
```

①

此隐式转换将在运行时成功。

## 6. 常量

常量是表示常量值的变量，即可以在编译时计算的值。常量成员将在后面讨论，例如在类常量成员一节中。

可以使用局部常量声明语句声明局部常量。

```csharp
const TYPE NAME = EXPR ;
```

①

常量使用关键字 const 声明。在此类记法中，全部大写的单词是占位符。也就是说，在实际语句中，TYPE、NAME 和 EXPR 需要分别替换为类型、名称（或标识符）和表达式。在局部常量声明中，右侧的 EXPR 必须是常量表达式。

可以在单条语句中声明多个常量。例如，

```csharp
const TYPE NAME1 = EXPR1 , NAME2 = EXPR2 ;
```
