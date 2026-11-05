
```csharp
T get_P();
void set_P(T value);
```

即使属性是只读或只写的，这两个签名也都会保留。

*示例：在以下代码中*

```csharp
class A
{
    public int P
    {
        get => 123;
    }
}

class B : A
{
    public new int get_P() => 456;

    public new void set_P(int value)
    {
    }
}

class Test
{
    static void Main()
    {
        B b = new B();
        A a = b;
        Console.WriteLine(a.P);
        Console.WriteLine(b.P);
        Console.WriteLine(b.get_P());
    }
}
```

类 A 定义了一个只读属性 P，因此保留了 get_P 和 set_P 方法的签名。类 B 从 A 派生，并隐藏了这两个保留的签名。该示例产生以下输出：

```
123
123
456
```

*示例结束*

### 15.3.10.3 为事件保留的成员名称

对于委托类型 T 的事件 E（§15.8），保留以下签名：

```csharp
void add_E(T handler);
void remove_E(T handler);
```

### 15.3.10.4 为索引器保留的成员名称

对于类型为 T、参数列表为 L 的索引器（§15.9），保留以下签名：

```csharp
T get_Item(L);
void set_Item(L, T value);
```

即使索引器是只读或只写的，这两个签名也都会保留。

此外，成员名称 Item 是保留的。

## 15.3.10.5 为终结器保留的成员名称

对于包含终结器（§15.13）的类，保留以下签名：

```csharp
void Finalize();
```

## 15.4 常量

常量是一种类成员，它表示一个常量值：即可以在编译时计算的值。constant_declaration 引入一个或多个给定类型的常量。

```
constant_declaration
: attributes? constant_modifier* 'const' type constant_declarators ';'
;
```

```
constant_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
;
```

constant_declaration 可以包含一组特性（§22）、一个 new 修饰符（§15.3.5），以及允许的已声明可访问性中的任意一种（§15.3.6）。特性和修饰符适用于该 constant_declaration 声明的所有成员。尽管常量被视为静态成员，但 constant_declaration 既不要求也不允许使用 static 修饰符。同一个修饰符在常量声明中出现多次是错误的。

constant_declaration 的类型指定该声明引入的成员的类型。类型之后是 constant_declarators 列表（§13.6.3），其中每个声明符引入一个新成员。constant_declarator 由命名该成员的标识符、后跟一个“=”标记、再后跟一个给出该成员值的 constant_expression（§12.23）组成。

常量声明中指定的类型应为 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool、string、enum_type 或 reference_type。每个 constant_expression 应产生目标类型的值，或产生可通过隐式转换（§10.2）转换为目标类型的类型的值。

> 注意：此类构造的示例包括 case 标签、goto case 语句、枚举成员声明、特性以及其他常量声明。注结束

> 注意：如 §12.23 所述，constant_expression 是可在编译时完全求值的表达式。由于创建 string 以外的 reference_type 的非 null 值的唯一方式是应用 new 运算符，并且 constant_expression 中不允许使用 new 运算符，因此 string 以外的 reference_type 常量唯一可能的值是 null。注结束

当需要为常量值使用符号名称，但该值的类型不允许出现在常量声明中，或者该值无法由 constant_expression 在编译时计算时，可以改用只读字段（§15.5.3）。

> 注意：const 和 readonly 的版本控制语义不同（§15.5.3.3）。注结束

声明多个常量的一个常量声明等价于多个具有相同特性、修饰符和类型的单个常量声明。

示例：

```
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```

等价于

```
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

示例结束

只要依赖关系不是循环的，就允许常量依赖于同一程序中的其他常量。编译器会自动按适当的顺序安排常量声明的求值。

示例：在以下代码中

```
class A
{
    public const int X = B.Z + 1;
    public const int Y = 10;
}

class B
{
    public const int Z = A.Y + 1;
}
```

编译器先对 A.Y 求值，然后对 B.Z 求值，最后对 A.X 求值，得到的值分别为 10、11 和 12。

示例结束

常量声明可以依赖其他程序中的常量，但这种依赖只能是一个方向上的。

示例：参照上面的示例，如果 A 和 B 声明在不同的程序中，则 A.X 可以依赖 B.Z，但此时 B.Z 不能同时依赖 A.Y。示例结束

## 15.5 字段

### 15.5.1 概述

字段是一种成员，它表示与对象或类关联的变量。field_declaration 引入一个或多个给定类型的字段。

```
field_declaration
  : attributes? field_modifier* type variable_declarators ';'
  ;
```

```
field_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'static'
  | 'readonly'
  | 'volatile'
  | unsafe_modifier  // unsafe code support
  ;
```

```
variable_declarators
  : variable_declarator (',' variable_declarator)*
  ;
```

```
variable_declarator
  : identifier ('=' variable_initializer)?
  ;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

field_declaration 可以包含一组特性（§22）、一个 new 修饰符（§15.3.5）、四个访问修饰符的有效组合（§15.3.6）以及一个 static 修饰符（§15.5.2）。此外，field_declaration 可以包含 readonly 修饰符（§15.5.3）或 volatile 修饰符（§15.5.4），但不能同时包含两者。特性和修饰符适用于该 field_declaration 声明的所有成员。同一个修饰符在 field_declaration 中出现多次是错误的。

field_declaration 的类型指定该声明引入的成员的类型。类型之后是 variable_declarators 列表，其中每个声明符引入一个新成员。variable_declarator 由命名该成员的标识符组成，后面可选地跟一个“=”标记和一个给出该成员初始值的 variable_initializer（§15.5.6）。

字段的类型应至少与字段本身一样可访问（§7.5.5）。

在表达式中，可以使用 simple_name（§12.8.4）、member_access（§12.8.7）或 base_access（§12.8.14）获取字段的值。非只读字段的值使用赋值（§12.21）进行修改。

非只读字段的值既可以使用后缀递增和递减运算符（§12.8.15）获取和修改，也可以使用前缀递增和递减运算符（§12.9.6）获取和修改。

声明多个字段的一个字段声明等价于多个具有相同特性、修饰符和类型的单个字段声明。

示例：

```
class A
{
    public static int X = 1, Y, Z = 100;
}
```

等价于

```
class A
{
    public static int X = 1;
    public static int Y;
    public static int Z = 100;
}
```

示例结束

### 15.5.2 静态字段和实例字段

当字段声明包含 static 修饰符时，该声明引入的字段是静态字段。当不存在 static 修饰符时，该声明引入的字段是实例字段。静态字段和实例字段是 C# 支持的几种变量（§9）中的两种，有时分别称为静态变量和实例变量。

如 §15.3.8 所述，类的每个实例都包含该类的一整套实例字段，而每个非泛型类或封闭构造类型只有一组静态字段，无论该类或封闭构造类型有多少个实例。

### 15.5.3 只读字段

### 15.5.3.1 概述

当 field_declaration 包含 readonly 修饰符时，该声明引入的字段是只读字段。对只读字段的直接赋值只能作为该声明的一部分，或在同一个类中的实例构造函数或静态构造函数中进行。（在这些上下文中，可以对只读字段进行多次赋值。）具体而言，只有在以下上下文中才允许对只读字段进行直接赋值：

- 在引入该字段的 variable_declarator 中（通过在声明中包含 variable_initializer）。
- 对于实例字段，在包含该字段声明的类的实例构造函数中；对于静态字段，在包含该字段声明的类的静态构造函数中。这些也是唯一可以将只读字段作为 out 或 ref 参数传递的有效上下文。

在任何其他上下文中尝试对只读字段赋值或将其作为 out 或 ref 参数传递，都是编译时错误。

### 15.5.3.2 使用静态只读字段表示常量

当需要为常量值使用符号名称，但该值的类型不允许出现在 const 声明中，或者该值无法在编译时计算时，静态只读字段很有用。

示例：在以下代码中

```
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
}
```
