

## 7. 表达式

除 E 只计算一次外。编译器可以将 E as T 优化为最多执行一次动态类型检查，而不是上述展开所隐含的两次动态类型检查。

如果 E 的编译时类型为 dynamic，则与强制转换运算符不同，as 运算符不会被动态绑定（§7.2.2）。因此，这种情况下的展开为

```
E is T ? (T)object(E) : (T)null
```

请注意，有些转换（如用户定义的转换）无法使用 as 运算符完成，此时应改用强制转换表达式。

在下面的示例中

```
class X
{
    public string F(object o) {
        return o as string;
        // Okay: string is a reference type
    }

    public T G<T>(object o) where T: Attribute {
        return o as T;
        // Okay: T has a class constraint
    }

    public U H<U>(object o) {
        return o as U;
        // Error: U is unconstrained
    }
}
```

G 的类型参数 T 已知是引用类型，因为它具有 class 约束。但是，H 的类型参数 U 并非已知；因此，在 H 中使用 as 运算符是不允许的。

> **CHRIS SELLS** 如果你正在使用 FxCop（而且你应该使用！）开箱即用，当你这样做时它并不喜欢：
>
> ```csharp
> if( x is Foo ) { ((Foo)x).DoFoo(); }
> ```
>
> 相反，它更倾向于你这样写：
>
> ```csharp
> Foo foo = x as Foo;
> if( foo != null ) { foo.DoFoo(); }
> ```
>
> 为什么？因为 is、as 和强制转换本质上都是相同的底层 .NET 操作，所以最好是只执行一次操作，检查结果是否为 null，然后对非 null 结果进行操作，而不是执行两次操作。

> **JOSEPH ALBAHARI** 尽管克里斯在技术上是对的，但这是一个微优化。引用转换的成本很低。

> **CHRIS SELLS** 尽管约瑟夫完全正确，但我更多是希望能摆脱 FxCop 的纠缠，而不是为了性能优化。

> **JOSEPH ALBAHARI** 有些人出于风格偏好，更喜欢使用 as 运算符而不是强制转换运算符。as 运算符的一个优点是，使用它可以清楚地表明该转换不是数值转换或用户定义的转换。然而，普遍偏爱将 as 运算符用于引用转换的问题在于，转换失败时计算结果为 null 并不总是可取的。为了说明这一点，请考虑以下代码的结果，如果 s 引用的对象不是字符串：
>
> ```csharp
> int length1 = ((string) s).Length;  // Throws InvalidCastException
> int length2 = (s as string).Length;  // Throws NullReferenceException
> ```
>
> 第一行会抛出包含有用信息的 InvalidCastException，而第二行会抛出（含义模糊的）NullReferenceException。（s 是 null 还是类型错误？）

> **JON SKEET** as 运算符几乎总是随后会进行空值测试——以至于它几乎值得拥有自己的语句类型：
>
> ```csharp
> // Would be equivalent to the code in Chris's annotation
> asif (Foo foo = x)
> {
>     foo.DoFoo();
> }
> ```
>
> 引入一种全新的语句类型可能有些过头——但当前这种模式的笨拙确实令人恼火。

## 7.11 逻辑运算符

&、^ 和 | 运算符称为逻辑运算符。

and-expression:
    equality-expression
    and-expression & equality-expression

```
exclusive-or-expression:
    and-expression
    exclusive-or-expression ^ and-expression

inclusive-or-expression:
    exclusive-or-expression
    inclusive-or-expression | exclusive-or-expression
```

如果逻辑运算符的某个操作数的编译时类型为 dynamic，则该表达式会被动态绑定（§7.2.2）。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时使用那些编译时类型为 dynamic 的操作数的运行时类型进行。

对于形式为 x op y 的操作，其中 op 是逻辑运算符之一，将应用重载决策（§7.3.4）来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型即为该运算符的返回类型。

预定义逻辑运算符将在以下各节中描述。

### 7.11.1 整数逻辑运算符

预定义的整数逻辑运算符如下所列：

```
int operator &(int x, int y);
uint operator &(uint x, uint y);
long operator &(long x, long y);
ulong operator &(ulong x, ulong y);

int operator |(int x, int y);
uint operator |(uint x, uint y);
long operator |(long x, long y);
ulong operator |(ulong x, ulong y);

int operator ^(int x, int y);
uint operator ^(uint x, uint y);
long operator ^(long x, long y);
ulong operator ^(ulong x, ulong y);
```

& 运算符计算两个操作数的按位逻辑 AND，| 运算符计算两个操作数的按位逻辑 OR，^ 运算符计算两个操作数的按位逻辑异或。这些运算不会发生溢出。

### 7.11.2 枚举逻辑运算符

每个枚举类型 E 都隐式提供以下预定义逻辑运算符：

```
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```

计算 `x op y` 的结果，其中 x 和 y 是底层类型为 U 的枚举类型 E 的表达式，且 `op` 是逻辑运算符之一，与计算 `(E)((U)x op (U)y)` 的结果完全相同。换句话说，枚举类型逻辑运算符只是对两个操作数的底层类型执行逻辑运算。

### 7.11.3 布尔逻辑运算符

预定义的布尔逻辑运算符如下所列：

```csharp
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```

如果 x 和 y 都为 true，则 `x & y` 的结果为 true；否则结果为 false。

如果 x 或 y 中有一个为 true，则 `x | y` 的结果为 true；否则结果为 false。

如果 x 为 true 且 y 为 false，或者 x 为 false 且 y 为 true，则 `x ^ y` 的结果为 true；否则结果为 false。当操作数为 `bool` 类型时，`^` 运算符计算出的结果与 `!=` 运算符相同。

### 7.11.4 可空布尔逻辑运算符

可空布尔类型 `bool?` 可以表示三个值：true、false 和 null。它在概念上类似于 SQL 中用于布尔表达式的三值类型。为了确保 `&` 和 `|` 运算符为 `bool?` 操作数产生的结果与 SQL 的三值逻辑一致，提供了以下预定义运算符：

```csharp
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

下表列出了这些运算符对 true、false 和 null 所有值组合产生的结果。

| x | y | x & y | x \| y |
|---|---|---|---|
| true | true | true | true |
| true | false | false | true |
| true | null | null | true |
| false | true | false | true |
| false | false | false | false |
| false | null | false | null |
| null | true | null | true |
| null | false | false | null |
| null | null | null | null |

## 7.12 条件逻辑运算符

&& 和 || 运算符称为条件逻辑运算符。它们也被称为“短路”逻辑运算符。

```
conditional-and-expression:
    inclusive-or-expression
    conditional-and-expression && inclusive-or-expression

conditional-or-expression:
    conditional-and-expression
    conditional-or-expression || conditional-and-expression
```

&& 和 || 运算符是 & 和 | 运算符的条件版本：

- 操作 `x && y` 对应于操作 `x & y`，不同之处在于仅当 x 不为 false 时才计算 y。
- 操作 `x || y` 对应于操作 `x | y`，不同之处在于仅当 x 不为 true 时才计算 y。

如果条件逻辑运算符的某个操作数的编译时类型为 dynamic，则该表达式会被动态绑定（§7.2.2）。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时使用那些编译时类型为 dynamic 的操作数的运行时类型进行。

形式为 x && y 或 x || y 的操作通过应用重载决策（§7.3.4）来处理，如同该操作写为 x & y 或 x | y 一样。然后，

- 如果重载决策无法找到唯一的最佳运算符，或者重载决策选择了预定义整数逻辑运算符之一，则会发生绑定期错误。
- 否则，如果所选运算符是预定义布尔逻辑运算符（§7.11.3）或可空布尔逻辑运算符（§7.11.4）之一，则按 §7.12.1 中描述的方式处理该操作。
- 否则，所选运算符是用户定义的运算符，则按 §7.12.2 中描述的方式处理该操作。

无法直接重载条件逻辑运算符。但是，由于条件逻辑运算符是根据常规逻辑运算符进行求值的，因此在某些限制下，常规逻辑运算符的重载也被视为条件逻辑运算符的重载。这种情况将在 §7.12.2 中进一步描述。

