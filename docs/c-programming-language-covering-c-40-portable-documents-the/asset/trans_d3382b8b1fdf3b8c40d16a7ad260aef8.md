

“仅求值一次”是指，在对 `x op= y` 求值时，`x` 的任何组成表达式的结果都会被暂时保存，并在对 `x` 执行赋值时重新使用。例如，在赋值 `A()[B()] += C()` 中，假设 `A` 是一个返回 `int[]` 的方法，而 `B` 和 `C` 是返回 `int` 的方法，则这些方法只调用一次，调用顺序为 A、B、C。

当复合赋值左操作数是属性访问或索引器访问时，该属性或索引器必须同时具有 get 访问器和 set 访问器。如果不满足此条件，则会发生绑定时错误。

上述第二条规则允许在某些上下文中将 `x op= y` 求值为 `x = (T)(x op y)`。该规则的存在使预定义运算符能够作为复合运算符使用，即使左操作数的类型是 `sbyte`、`byte`、`short`、`ushort` 或 `char`。即使两个参数都是这些类型之一，预定义运算符产生的结果类型仍为 `int`，如 §7.3.6.2 所述。因此，如果不进行强制转换，就无法将结果赋值给左操作数。

对于预定义运算符而言，该规则的直观效果是：只要 `x op y` 和 `x = y` 都是有效的，就允许使用 `x op= y`。例如：

```
byte b = 0;
char ch = '\0';
int i = 8;

b += 1;            // Okay
b += 1000;         // Error: b = 1000 not permitted
b += i;            // Error: b = i not permitted
b += (byte)i;      // Okay
ch += 1;           // Error: ch = 1 not permitted
ch += (char)1;     // Okay
```

每个错误的直观原因是：相应的简单赋值同样会产生错误。

这也意味着复合赋值运算支持提升运算。在下面的示例中：

```
int? i = 0;
i += 1;            // Ok
```

使用的是提升运算符 `+(int?,int?)`。

### 7.17.3 事件赋值

如果 `+=` 或 `-=` 运算符的左操作数被归类为事件访问，则表达式按以下方式求值：

- 对事件访问中的实例表达式（如果有）求值。
- 对 `+=` 或 `-=` 运算符的右操作数求值，并在需要时通过隐式转换（§6.1）将其转换为左操作数的类型。
- 调用该事件的事件访问器，参数列表由求值并在必要时完成转换后的右操作数组成。如果运算符是 `+=`，则调用 add 访问器；如果运算符是 `-=`，则调用 remove 访问器。

事件赋值表达式不产生值。因此，事件赋值表达式仅在语句表达式（§8.6）的上下文中有效。

## 7.18 表达式

表达式可以是非赋值表达式，也可以是赋值。

```
expression:
    non-assignment-expression
    assignment
```

```
non-assignment-expression:
    conditional-expression
    lambda-expression
    query-expression
```

## 7.19 常量表达式

常量表达式是指可以在编译时完全求值的表达式。

```
constant-expression:
    expression
```

常量表达式必须是 null 字面量，或具有以下类型之一的值：`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double`、`decimal`、`bool`、`string`，或任意枚举类型。常量表达式中只允许使用以下构造：

- 字面量（包括 null 字面量）。
- 对类类型和结构类型的 const 成员的引用。
- 对枚举类型成员的引用。
- 对 const 参数或局部变量的引用。
- 括号括起来的子表达式，且这些子表达式本身也是常量表达式。
- 强制转换表达式，前提是目标类型是上述类型之一。
- `checked` 和 `unchecked` 表达式。
- 默认值表达式。
- 预定义的一元 `+`、`-`、`!` 和 `~` 运算符。
- 预定义的二元 `+`、`-`、`*`、`/`、`%`、`<<`、`>>`、`&`、`|`、`^`、`&&`、`||`、`==`、`!=`、`<`、`>`、`<=` 和 `>=` 运算符，前提是每个操作数的类型都属于上述类型。
- `?:` 条件运算符。

常量表达式中允许使用以下转换：

- 标识转换。
- 数值转换。
- 枚举转换。
- 常量表达式转换。
- 隐式引用转换和显式引用转换，前提是转换的源是一个求值结果为 null 值的常量表达式。

其他转换（包括装箱、拆箱，以及对非 null 值执行的隐式引用转换）不允许出现在常量表达式中。例如：

```
class C {
    const object i = 5;       // Error: boxing conversion not permitted
    const object str = "hello"; // Error: implicit reference conversion
}
```

在此示例中，`i` 的初始化会产生错误，因为需要进行装箱转换。`str` 的初始化也会产生错误，因为需要对非 null 值执行隐式引用转换。

只要表达式满足上述要求，就会在编译时对其求值。即使该表达式是包含非常量构造的更大表达式的子表达式，这一规则仍然适用。

常量表达式的编译时求值使用与非常量表达式运行时求值相同的规则，唯一的区别是：在运行时求值会引发异常的情况下，编译时求值会导致编译时错误。

除非常量表达式被显式置于 `unchecked` 上下文中，否则在表达式的编译时求值期间，整型算术运算和转换中发生的溢出始终会导致编译时错误（§7.19）。

常量表达式出现在以下上下文中。在这些上下文中，如果表达式无法在编译时完全求值，则会发生编译时错误。

- 常量声明（§10.4）。
- 枚举成员声明（§14.3）。
- `switch` 语句的 `case` 标签（§8.7.2）。
- `goto case` 语句（§8.9.3）。
- 包含初始化表达式的数组创建表达式中的维度长度（§7.6.10.4）。
- 特性（§17）。

隐式常量表达式转换（§6.1.8）允许将 `int` 类型的常量表达式转换为 `sbyte`、`byte`、`short`、`ushort`、`uint` 或 `ulong`，前提是常量表达式的值处于目标类型的取值范围内。

## 7.20 布尔表达式

布尔表达式是直接产生 `bool` 类型结果，或在下述特定上下文中通过应用 `true` 运算符产生该结果的表达式。

```
boolean-expression:
    expression
```

`if` 语句（§8.7.1）、`while` 语句（§8.8.1）、`do` 语句（§8.8.2）或 `for` 语句（§8.8.3）的控制条件表达式必须是布尔表达式。`?:` 运算符（§7.14）的控制条件表达式遵循与布尔表达式相同的规则，但出于运算符优先级的原因，它被归类为条件或表达式。

布尔表达式必须能够隐式转换为 `bool`，或者其类型必须实现 `true` 运算符。如果两个条件都不满足，则会发生绑定时错误。

当布尔表达式无法隐式转换为 `bool`，但其类型实现了 `true` 运算符时，在对表达式求值后，会调用该类型提供的 `true` 运算符实现，以产生一个 `bool` 值。

## 8. 语句

C# 提供了多种语句。其中大多数语句对于使用 C 和 C++ 编程的开发人员来说都很熟悉。

+   statement:
+     - labeled-statement
+     - declaration-statement
+     - embedded-statement

+   embedded-statement:
+     - block
+     - empty-statement
+     - expression-statement
+     - selection-statement
+     - iteration-statement
+     - jump-statement
+     - try-statement
+     - checked-statement
+     - unchecked-statement
+     - lock-statement
+     - using-statement
+     - yield-statement

`embedded-statement` 非终结符用于表示出现在其他语句中的语句。在这些上下文中使用 `embedded-statement` 而不是 `statement`，排除了使用声明语句和带标签语句的可能性。示例：

```
void F(bool b) {
    if (b)
        int i = 44;
}
```

会导致编译时错误，因为 `if` 语句要求其 `if` 分支使用 `embedded-statement`，而不是 `statement`。如果允许这段代码，那么变量 `i`

