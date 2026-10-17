
关键字是保留字，其含义由 C# 编译器预先定义。换句话说，关键字是 C# 编译器保留用于特定任务的词语。你不能将关键字用作变量、方法和属性，因为它们已经被定义给编译器以执行特定的功能。如果你想将关键字用作标识符，请在关键字前面加上 `@` 字符。C# 提供了一些在代码上下文中具有特殊含义的标识符，例如 `get` 和 `set`，但它们不是保留关键字。这些标识符被称为上下文关键字。表 2.1 列出了 C# 中可用的不同保留关键字和上下文关键字：

表 2.1：显示 C# 中的保留关键字和上下文关键字

| 保留关键字 | | | | | | |
|---|---|---|---|---|---|---|
| abstract | as | base | bool | break | byte | case |
| catch | char | checked | class | const | continue | decimal |
| default | delegate | do | double | else | enum | event |
| explicit | extern | false | finally | fixed | float | for |
| foreach | goto | if | implicit | in | in（泛型修饰符） | int |
| interface | internal | is | lock | long | namespace | new |
| null | object | operator | out | out（泛型修饰符） | override | params |
| private | protected | public | readonly | ref | return | sbyte |
| sealed | short | sizeof | stackalloc | static | string | struct |
| switch | this | throw | true | try | typeof | uint |
| ulong | unchecked | unsafe | ushort | using | virtual | void |
| volatile | while |  |  |  |  |  |

| 上下文关键字 | | | | | | |
|---|---|---|---|---|---|---|
| add | alias | ascending | descending | dynamic | from | get |
| global | group | into | join | let | orderby | partial（类型） |
| partial（方法） | remove | select | set |  |  |  |

现在，让我们来了解变量和常量。

## 变量和常量

变量是表示内存中存储位置的标识符。它存储在程序执行期间可能更改的数字或字符串值。在程序执行期间，变量在不同时间可能取不同的值，但变量的名称始终保持不变。每个变量都有一种数据类型，该类型决定了你可以存储在变量中的值的类型。以下代码片段演示了如何声明变量并为其赋值：

```
int i;
i=15;
```

在上述代码片段的第一行中，我们通过指定数据类型 `int` 来声明一个名为 `i` 的整数类型变量。在第二行中，我们使用 `=` 运算符将值 15 赋给整数变量 `i`。

变量可以声明为局部变量或类变量。局部变量存在于类中给定方法的作用域内；而类变量存在于类的对象实例的整个生命周期内。类变量可以在类的任何方法中使用，并且可以是 `public`、`private` 或 `protected`。局部变量不能定义为 `public` 或 `private`，因为在定义它们的方法之外无法访问它们。

C# 还提供了静态类变量，可用于静态类方法。对于给定类的所有实例，只存在一个静态类变量实例。

变量可以是数组类型。以下代码片段演示了如何声明整数类型的数组：

```
int[] arr = new int[10];
```

与变量类似，常量也用于存储值。但是，与变量不同的是，常量的值在程序执行期间不会更改。使用 `const` 关键字可以将变量声明为常量。以下代码片段演示了如何在应用程序中使用常量：

```
const double e= 2.718281828459045235360287;
const int x=100;
```

在上述代码片段的第一行中，我们声明了一个 `double` 数据类型的常量 `e`，并将值 2.718281828459045235360287 赋给它。在第二行中，我们声明了一个常量 `x`，其数据类型为 `int` 数据类型并将其值赋值为 100。这些常量所赋的值在整个程序执行过程中不会改变。如果你尝试给常量赋另一个值并编译程序，将会显示一个错误，指出赋值的左侧必须是变量、属性或索引器。

常量和变量只能在特定的作用域内访问。变量的作用域决定了在程序中可以访问和引用该变量的区域。作用域有两种类型，块作用域和类作用域。当你在代码块内声明一个变量时，该变量获得局部作用域或块作用域，因此它被称为局部变量。具有局部作用域的变量不能在声明它的代码块之外使用。如果你将变量声明在代码块之外（或在定义 `Main()` 方法之前），则该变量被认为具有类作用域并被称为全局变量。这样的变量可以在整个程序中使用。清单 2.1 显示了一个示例来说明变量的作用域：

### Listing 2.1: Showing an Example for the Scope of Variables

```
class Scope
{
public void Scope1()
{
    int i = 0;
    i = i + 1;
}
public void Scope2()
{
    Console.WriteLine(i);
}
}
```

在清单 2.1 中，变量 `i` 在 `Scope1()` 方法内声明并初始化。现在当你尝试在 `Scope1()` 方法之外访问变量 `i` 时，会发生编译时错误，指出名称 `i` 在当前上下文中不存在。这是因为 `i` 变量是 `Scope1()` 方法的局部变量，只能在此方法内访问。

类作用域使用访问修饰符，例如 `private` 和 `public`，来指定变量的作用域。`private` 关键字使变量对类是局部的，并指定该变量不能在声明它的类之外使用和访问。你可以通过将其声明为 `public` 使变量在类中变为全局。这使得变量可以在整个程序中的任何类中使用。清单 2.2 显示了一个示例来理解类的作用域：

### Listing 2.2: Showing an Example for the Scope of a Class

```
public class LocalScope1
{
    int i = 0;
}
public class LocalScope2
{
    void Scope()
    {
        Console.WriteLine(i);
    }
}
```

在清单 2.2 中，你可以看到变量 `i` 在类 `LocalScope1` 中声明。如果你尝试在 `LocalScope1` 类之外访问 `i`，相同的编译时错误会发生，指出名称 `i` 在当前上下文中不存在。错误发生是因为 `i` 变量在 `LocalScope1` 类中声明，并且默认是 `private`。因此该变量不能在 `LocalScope2` 类中访问。

C# 支持丰富多样的各种数据类型，从内置类型，如整数或字符串，到用户定义类型，如枚举、结构和类。C# 语言提供了丰富的内置数据类型。在处理这些数据类型时，你必须记住以下几点：

- 所有变量，无论是用户定义的还是固有的（内置的），都可以在程序中的任何地方用作对象

- 程序中的所有变量在声明时都会由系统自动初始化为默认值

在 C# 中，变量分为以下三类：

- 值类型

- 引用类型

- 指针类型

让我们详细讨论这些。

## Value Types

值类型是可以直接赋值的变量。它们派生自 `System.ValueType`，并在通用语言运行时（CLR）中具有特殊行为。值类型及其内容存储在内存的同一位置。值类型的默认值存储在栈上。表 2.2 列出了 C# 2010 中可用的值类型：

Table 2.2: Showing the Value Types In C# 2010

| Value Type | What it represents | Ranges | Default Value |
|---|---|---|---|
| bool | Represents a Boolean value | True or False | false |
| byte | Represents 8-bit unsigned integer type | 0 to 255 | 0 |
| char | Represents single 16-bit Character type, a char value is a Unicode character | U+0000 to U+ffff | '\0' |
| decimal | Represents 128-bit Precise decimal type with 28-29 significant digits | (-7.9 x 10^28 to 7.9 x 10^28) / (10^0 to 28) | 0.0M |
| double | Represents 64-bit Double-precision floating-point type | ±5.0 x 10^-324 to ±1.7 x 10^308 | 0.0D |
| float | Represents 32-bit Single-precision floating-point type | -3.4 x 10^38 to +3.4 x 10^38 | 0.0F |
| int | Represents 32-bit signed integer type | -2,147,483,648 to 2,147,483,647 | 0 |
| long | Represents 64-bit signed integer type | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | 0L |
| sbyte | Represents 8-bit signed integer type | -128 to 127 | 0 |
| short | Represents 16-bit signed integer type | -32,768 to 32,767 | 0 |
| uint | Represents 32-bit unsigned integer type | 0 to 4,294,967,295 | 0 |
| ulong | Represents 64-bit unsigned integer type | 0 to 18,446,744,073,709,551,615 | 0 |
| ushort | Represents 16-bit unsigned integer type | 0 to 65,535 | 0 |

值类型分为以下几类：

- Struct type

- Enum type

让我们详细讨论这些。

### Struct Type

结构类型是一种具有值类型属性的特殊形式类。正如你所知，值类型存储在栈上；本质上结构类型也存储在栈上。结构类型可以高效地复制和创建，因为栈是存储和访问类型的高效便捷手段。结构类型封装一组相关的变量，例如学生的姓名、学号、年龄、班级和班级编号。它们可以包含构造函数、方法、属性、运算符、事件、嵌套类型、索引器、常量和字段。在创建结构类型时，你应该记住结构成员不能声明为 `protected`，因为它们不支持继承。在结构声明下，字段只能在声明为 `const` 或 `static` 时初始化。

你可以使用 `struct` 关键字创建结构类型。当你创建结构对象并将其赋给变量时，变量保存结构对象的值。你也可以将结构类型用作可空类型，通过为其赋 `null` 值。清单 2.3 显示了如何创建结构类型：

### Listing 2.3: Showing an Example of the Struct Type

```
public struct student
{
    string name;
    int rollno;            //fields
    int classname;
    int section;
    ...                    //methods
    ...                    //properties
}
```

在清单 2.3 中，我们创建了一个名为 `student` 的结构类型并将其声明为 `public`。在结构体内部，我们声明了成员，如 `name`、`rollno`、`classname` 和 `section`。

结构类型分为以下五类：

- Integral type

- Floating-Point type

- Decimal type

- Boolean type

- Nullable type

让我们在后续章节中简要讨论所有这些数据类型。

### Integral Type

C# 提供了一组基本数据类型，被称为整型。此集合包括 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong` 和 `char` 等类型。要了解这些数据类型的大小、范围和默认值，请参阅表 2.2。

整型可以分为两种值类型：有符号和无符号。有符号值类型可能包含负值或正值，而无符号值类型仅包含正值。与 C++ 不同，两种类型之间的转换通常需要显式强制转换。

### Floating-Point Type

浮点类型分为两种——单精度和双精度。单精度浮点数类似于 C++ 的 `float` 数据类型，可保存高达 10^38 的值。双精度数据类型也类似于 C++ 的 `double` 类型，可保存高达 10^308 的值。浮点类型以分数形式取值。例如，如果你声明一个变量为 `float` 并赋值为 2，则该变量将存储值 2.0。

### Decimal Type

另一种数据类型 `Decimal` 等同于一个表现得像浮点数的长整数。`Decimal` 值旨在用于计算货币值或其他不需要四舍五入的计算。与浮点类型相比，`decimal` 类型具有更高的精度和更小的范围。

### Boolean Type

布尔值是简单的真或假值。与 C++ 不同，它们不能赋给其他类型，也不能用于任何计算。C# 中表达式的结果不是布尔表达式，除非你明确将其指定为 `true` 或 `false`。

### Nullable Type

当处理数据库或用户不希望为任何数据类型的变量赋值时，编程语言支持可空数据类型。如果你使用的编程语言不支持可空数据类型，你可以使用不同的策略来处理空值。例如，你可以使用 -1 来指定整数变量的空值。你也可以使用布尔空指示符来指定变量的空值。

例如，你可以将 `true`、`false` 或 `null` 值赋给布尔变量。此外，你还可以使用 .NET Framework 支持的由用户定义的可空类型集合。

## 枚举类型

枚举是使用 `enum` 关键字声明的用户定义整数数据类型。使用枚举，你可以定义一组命名的整型常量并将其赋给变量。例如，你可能有一个模拟交通灯的程序。交通灯有三种可能的状态——绿灯表示通行，黄灯表示准备停车，红灯表示停车。交通灯一次只能处于其中一种状态，这意味着交通灯一次只能是红、黄或绿。在这种情况下，你可以定义枚举类型变量并为其赋 3 个值。以下代码片段展示了如何创建枚举类型：

```
enum TrafficLight
{Red, Green, Yellow}
```

要使用枚举类型，你需要声明一个新枚举类型变量，如以下代码片段所示：

```
TrafficLight t1;
```

`TrafficLight` 枚举可以取三种值中的任意一个，`Red`、`Green` 和 `Yellow`；即枚举只能取在创建枚举类型时定义的值，如以下代码片段所示：

```
t1 = TrafficLight.Red;
t1 = TrafficLight.Green;
t1 = TrafficLight.Yellow;
```

枚举默认从第一个条目的 0 值开始。然而，你可以通过为第一个条目输入不同的值来修改此值，如以下代码片段所示：

```
enum TrafficLight
{
Red=1, Green, Yellow
}
```

让我们来看看 C# 中的引用类型。

## 引用类型

C# 还提供了作为引用传递给调用函数的类型，称为引用类型。引用对象的变量存储实际数据的引用。在引用类型中，对新副本所做的任何更改都会修改对象所引用的旧副本。引用类型使用堆来存储引用而不是实际数据。在 C# 中，堆称为托管堆，因为它管理和维护指向要分配下一个对象的地址的指针。最初，指针指向堆的基地址，当创建第一个引用时，内存会在基地址分配。当在应用程序中创建下一个对象时，垃圾收集器会在紧邻第一个对象之后的地址空间为其分配内存，并继续为所有新创建的对象分配内存。C# 提供了一些内置引用类型，如下所示：

- `dynamic` 类型 — 在运行时而不是编译时对 `dynamic` 类型变量进行类型检查。你可以在 `dynamic` 类型变量中添加任何类型的值。此类型类似于 `object` 类型；区别在于 `object` 类型变量的类型检查是在编译时执行的。以下代码片段展示了如何声明 `dynamic` 类型变量：

  ```
  dynamic dyn = 10;
  ```

- `object` 类型 — 使你能够将任何类型的值赋给 `object` 类型的变量。`Object` 是预定义 `System.Object` 类的别名。`Object` 类型是通用类型系统 CTS 中其他类型的终极基类，例如值类型、引用类型、预定义类型和用户定义类型。所有这些类型都是直接或间接从 `object` 类型派生的。`Object` 类型可以赋予任何其他类型的值，但在赋值前需要进行类型转换。当值类型转换为 `object` 类型时，该过程称为装箱，而相反地，当 `object` 类型转换为值类型时，该过程称为拆箱。以下代码片段展示了 `object` 类型的使用：

  ```
  object x;
  x=15; //boxing
  ```
