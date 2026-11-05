
⑤ 此调用中方法参数 `a` 被称为“非尾随命名参数”，因为它位于位置参数 `'d'` 之前（例如）。

⑥ 此调用中的 `a` 和 `b` 必须使用命名参数语法。

## 9.3. `params` 参数

在 C# 中，形式参数列表中的最后一个参数可以是 `params` 数组参数，它由以下部分组成

- 可选
- `params` 关键字
- 一维数组类型，以及
- 参数名。

`params` 参数是值参数。（但请注意，数组是引用类型。）在方法调用中，`params` 参数的参数可以指定为数组值，也可以指定为零个、一个或多个数组元素类型的参数。例如，给定以下函数，

```csharp
static int AddAll(params int[] operands) => operands.Sum();
```

可以将其与 int 数组参数一起调用，

```csharp
var ints = new int[] { 1, 2, 3 };
var sum1 = AddAll(ints);
Console.WriteLine($"sum = {sum1}");
```

## 9.4. 值参数

未使用任何参数修饰符声明的形式参数默认为值参数。值参数对应于一个局部变量，其初始值来自函数中提供的相应参数。因此，参数应为可隐式转换为参数类型的表达式。

## 9.5. `in` 参数

使用 `in` 或 `ref` 修饰符的参数按引用传递。`in` 关键字指定被调用的方法不修改值。`in` 参数对应于局部 `ref readonly`。`in` 参数使用参数规范中的 `in` 修饰符声明，并且可以包含默认值。例如，

```csharp
static void PrintCoord(in Coord cord) =>
    Console.WriteLine($"Lat = {cord.Lat}; Lon = {cord.Lon}");
record struct Coord(float Lat, float Lon);
```

① `in` 参数 `cord` 使用按引用调用语义。`PrintCoord` 函数无法修改其值。

此函数可以带或不带 `in` 关键字调用。

```csharp
var coord = new Coord(40.0f, -100.0f);
PrintCoord(coord);
PrintCoord(in coord);
```

尽管它使用引用语义，但它不能更改 `in` 参数的值。因此，可以在不必担心数据可变性的情况下预期一定的性能提升。

## 9.6. `out` 参数

使用 `out` 修饰符声明的参数是输出参数。相应的参数按引用传递。例如，

```csharp
static void SetCoord(out Coord c) =>
    c = new(0.0f, 0.0f);
```

① `out` 参数在被赋值之前不能被引用，并且必须在函数返回之前被赋一个值。

要使用 `out` 参数，方法定义和调用方法都必须显式使用 `out` 关键字。您可以在方法调用的参数列表中声明一个新的 `out` 变量。例如，

```csharp
SetCoord(out var c);
Console.WriteLine($"Lat = {c.Lat}; Lon = {c.Lon}");
```

① 我们也可以使用显式类型，例如 `SetCoord(out Coord c)`。这或多或少等同于 `Coord c; SetCoord(out c);`。

## 9.8. 通过引用返回

### 9.8.1. Ref 返回

C# 方法默认按与参数按值传递类似的方式返回值。相比之下，`ref` 返回是方法通过引用返回给调用者的值。也就是说，而不是复制方法返回的值，而是返回其引用。（或者，更准确地说，复制其引用。）`ref` 返回正常工作有三个方面。

方法签名中的返回类型需要以 `ref` 为前缀。例如，`public ref MyStruct`。

方法体中 `return` 语句的表达式需要标记为 `ref`。例如，`return ref`。

为了使调用者能够修改对象的状态，`ref` 返回值需要被赋给一个 `ref` 局部变量。

### 9.8.2. Ref 只读返回

被调用的方法也可以将返回值声明为 `ref readonly` 以通过引用返回该值，同时强制调用代码不能修改返回值。调用方法可以通过将值存储在局部 `ref readonly` 中来避免复制返回值。例如，

```csharp
static class RefReturnDemo {
    static ref readonly Coord Move(ref Coord moving) =>
        ref moving; // return ref
    public static void PrintAfterMove(Coord here) {
        ref readonly var t = ref Move(ref here);
        Console.WriteLine($"Lat = {t.Lat}; Lon = {t.Lon}");
    }
}
```

## 10. 内置值类型

本章将介绍几种简单类型。内置的 `string` 类型将在下一章讨论。

## 10.1. `bool` 类型

C# `bool` 类型是 .NET `System.Boolean` 结构类型的别名，其值可以是 `true` 或 `false`。`bool` 类型的默认值是 `false`。也就是说，`default(bool)` 返回 `false`。

### 10.1.1. 可空的 `bool?` 类型

可空的 `bool?` 类型可用于三值逻辑，例如在处理支持三值布尔类型的数据库时。预定义的 `&` 和 `|` 运算符支持 `bool?` 操作数的三值逻辑。

## 10.2. `char` 类型

C# `char` 类型是 .NET `System.Char` 结构类型的别名，表示 UTF-16 编码中的 Unicode 字符。`char` 类型的默认值是 `'\0'`；也就是说，`default(char)` 返回 `'\0'`。

### 10.2.1. 字符字面量

您可以使用以下方式指定 `char` 值：

- 一个字符字面量。
- Unicode 转义序列；或
- 十六进制转义序列，例如 `\x` 后跟字符代码的十六进制表示。

## 10.3. 整数类型

C# 支持 11 种整数类型：四种无符号整数类型和四种有符号整数类型，均使用二进制补码格式表示。`char` 类型也是整数类型。此外，C# 还包括两种本机整数类型，`nint` 和 `nuint`。

| 类型 | 描述 |
| --- | --- |
| `byte` | 值范围为 0 到 255 的无符号 8 位整数 |
| `sbyte` | 值范围为 -128 到 127 的有符号 8 位整数 |
| `ushort` | 值范围为 0 到 65535 的无符号 16 位整数。 |
| `short` | 值范围为 -32768 到 32767 的有符号 16 位整数。 |
| `uint` | 值范围为 0 到 4294967295 的无符号 32 位整数。 |
| `int` | 值范围为 -2147483648 到 2147483647 的有符号 32 位整数。 |
| `ulong` | 值范围为 0 到 18446744073709551615 的无符号 64 位整数。 |
| `long` | 值范围为 -9223372036854775808 到 9223372036854775807 的有符号 64 位整数。 |

`checked` 和 `unchecked` 运算符和语句用于控制整数类型算术运算和转换的溢出检查。

## 10.4. 本机整数类型

C# 现在包含两个新的上下文关键字，`nint` 和 `nuint`，它们分别表示本机有符号和本机无符号整数类型，旨在用于低级库。这些上下文关键字仅在名称查找在该程序位置找不到可行结果时才被视为关键字。

C# 类型 `nint` 和 `nuint` 分别对应于底层的 .NET 类型 `System.IntPtr` 和 `System.UIntPtr`，编译器支持在特定平台或操作系统上将这些类型作为本机整数类型的额外转换和操作。

## 10.5. 浮点类型

C# 支持两种浮点类型，`float` 和 `double`，它们分别使用 32 位单精度和 64 位双精度 IEC 60559 格式表示。浮点数字面量在词法分析章节中描述。

## 10.6. `decimal` 类型

`decimal` 类型是 128 位实数类型，适用于高精度计算。内部 `decimal` 表示为按十的幂缩放的整数。十进制数保证至少有 28 位精度。`decimal` 类型的精度更高，但范围可能小于浮点类型。

如果 `decimal` 算术运算产生的结果的绝对值对于 `decimal` 来说太大，则会抛出 `System.OverflowException`。
