

## 示例 7 整数变量的三等等声明

```csharp
using System;
...
int i;
Int32 i2;
System.Int32 i3;
```

## 简单类型：常量、默认值和范围

| 类型 | 示例常量 | 默认值 | 范围 (最小值...最大值) |
|---|---|---|---|
| bool | true | false | false, true |
| char | 'A', '\u0041' | '\u0000' | '\u0000''\uFFFF' |
| sbyte | -119 | 0 | -128...127 |
| byte | 219 | 0 | 0...255 |
| short | -30319 | 0 | -32768...32767 |
| ushort | 60519 | 0 | 0...65535 |
| int | -2147483648 | 0 | -2147483648...2147483647 |
| uint | 4294967295 | 0 | 0...4294967295 |
| long | -9223372036854775808 | 0 | -9223372036854775808...9223372036854775807 |
| ulong | 18446744073709551615 | 0 | 0...18446744073709551615 |
| float | -1.99E-3 | 0.0 | ±¹⁰⁷...±¹⁰⁸, 7位有效数字 |
| double | -1.99E-8 | 0.0 | ±¹⁰³...±¹⁰⁸, 15-16位有效数字 |
| decimal | -1.99M | 0.0 | ±¹⁰⁸...±¹⁰⁹, 28-29位有效数字 (*) |

> *) 可能会更改为范围 ±10¹⁴³...±¹⁰¹⁴⁴ 和34位有效数字 (IEEE 754 十进制)。

## 简单类型：种类、大小和结构体名称

| 类型 | 种类 | 大小 | 结构体类型 |
|---|---|---|---|
| bool | 逻辑 | 1 | System.Boolean |
| char | 无符号整数 | 2 | System.Char |
| sbyte | 无符号整数 | 1 | System.SByte |
| byte | 无符号整数 | 1 | System.Byte |
| short | 整数 | 2 | System.Int16 |
| ushort | 无符号整数 | 2 | System.UInt16 |
| int | 整数 | 4 | System.Int32 |
| uint | 无符号整数 | 4 | System.UInt32 |
| long | 整数 | 8 | System.Int64 |
| ulong | 无符号整数 | 8 | System.UInt64 |
| float | 二进制浮点数 | 4 | System.Single |
| double | 二进制浮点数 | 8 | System.Double |
| decimal | 十进制浮点数 | 16 | System.Decimal |

当它是这些类型之一时，`sizeof(t)` 是一个编译时表达式，其值为 `Size`。

## 5.2 引用类型

引用类型可以是类、数组类型或委托类型。类由类声明（第10节）定义，接口由接口声明（第15节）定义，委托类型由委托声明（第17节）定义。数组类型在第9节中讨论过。

引用类型的变量要么包含一个特殊值 `null`，要么包含指向分配在堆上的对象或委托的引用。特殊值 `null` 不引用任何内容。表示空值的常量 `null` 可以是任何引用类型。为变量赋值引用值只赋值引用本身，而不复制所指向的对象或委托。

类型组织在类型层次结构中（如所示），以 `Object` 类作为所有其他类型的基类。这些类型实现的方法由其派生类型继承。

`Object` 类是所有类的基类（超类）。`ol1` 和 `ol2` 是 `Object` 类型的表达式：

- `ol1.Equals(ol2)` 如果 `ol1` 和 `ol2` 相等则返回 `true`；否则取决于默认值。默认情况下，引用类型的值通过相同的 `new` 执行是相等的；但（例如）`String` 重写了 `Equals` 来比较字符串内容（第7节），而 `ValueType` 类 `Equals` 则如果一个类型的两个值的所有字段都相等，则认为它们相等。

- `Object.ReferenceEquals(ol1, ol2)` 如果 `ol1` 和 `ol2` 都为 `null`，或者它们都指向同一个对象或委托，则返回 `true`；否则返回 `false`。

- `Object.Equals(ol1, ol2)` 如果 `ol1` 和 `ol2` 都为 `null`，或者它们引用同一个对象或委托，则返回 `true`；否则返回 `false`。如果 `ol1` 或 `ol2` 是值类型，则取决于具体实现。

- `ol1.GetType()` 返回表示 `ol1` 运行时的唯一类型。

- `ol1.GetHashCode()` 返回 `ol1` 的哈希值，当 `ol1` 用作哈希表的键时（第27节）。子类重写了此方法以确保：1) 如果 `ol1` 和 `ol2` 通过 `Equals` 相等，则具有相同的哈希值；(2) 对 `ol1` 的修改不改变其哈希值；(3) 哈希值分布均匀；(4) 方法必须快速且不抛出异常。所有简单类型和 `String` 都有相应的 `GetHashCode` 方法。

- `ol1.ToString()` 返回对象或引用类型常用的可读表示（第7节）。

`String` 类是 `Object` 的子类，是 `int[]` 的基类。

`ValueType` 类是 `Object` 的子类，是所有值类型的基类，包括简单类型、结构类型和枚举类型。它本身不是值类型。如果 `v1` 和 `v2` 是派自 `ValueType` 的结构类型，则 `v1.Equals(v2)` 使用反射来比较 `v1` 和 `v2` 的字段。这可能很慢，因此结构类型应该重写 `Equals`。派自 `ValueType` 的任何类型都是值类型。

`Enum` 类是 `ValueType` 的子类，是所有枚举类型的基类。它本身不是值类型。

`Delegate` 类是 `Object` 的子类，是所有委托类型的基类。它本身不是值类型。

## 示例 8 Object 类中声明的方法

在 `Object` 类中声明的方法被所有类型继承，并可以使用所有值。

```csharp
Object ol1 = new Object();
Object ol2 = new Object();
Object ol3 = new Object();
ol1.Equals(ol2); // 返回 false
ol1.Equals(ol3); // 返回 false
Object.ReferenceEquals(ol1, ol2); // 返回 false
Object.ReferenceEquals(ol1, null); // 返回 false
Object.ReferenceEquals(null, null); // 返回 true
ol1.GetType(); // 返回 System.Object
ol1.GetHashCode(); // 返回一个哈希值
ol1.ToString(); // 返回 "System.Object"
```

