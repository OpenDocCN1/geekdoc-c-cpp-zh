
## BEGINNER TOPIC

### Parentheses, Associativity, Precedence, and Evaluation

When an expression contains multiple operators, it can be unclear precisely what the operands of each operator are. For example, in the expression `x+y*z`, clearly the expression `x` is an operand of the addition and `z` is an operand of the multiplication. But is `y` an operand of the addition or the multiplication?

`Parentheses` allow you to unambiguously associate an operand with its operator. If you wish `y` to be a summand, you can write the expression as `(x+y)*z`; if you want it to be a multiplicand, you can write `x+(y*z)`.

However, C# does not require you to parenthesize every expression containing more than one operator; instead, the compiler can use associativity and precedence to figure out from the context which parentheses you have omitted. `Associativity` determines how similar operators are parenthesized; `precedence` determines how dissimilar operators are parenthesized.

A binary operator may be “left-associative” or “right-associative,” depending on whether the expression “in the middle” belongs to the operator on the left or the right. For example, `a-b-c` is assumed to mean `(a-b)-c`, and not `a-(b-c)`; subtraction is therefore said to be “left-associative.” Most operators in C# are left-associative; the assignment operators are right-associative.

When the operators are dissimilar, the `precedence` for those operators is used to determine which side the operand in the middle belongs to. For example, multiplication has higher precedence than addition and, therefore, the expression `x+y*z` is evaluated as `x+(y*z)` rather than `(x+y)*z`.

It is often still a good practice to use parentheses to make the code more readable even when use of parentheses does not change the meaning of the

### Special Floating-Point Characteristics

The binary floating-point types: `float` and `double`, have some special characteristics, such as the way they handle precision. This section looks at some specific examples, as well as some unique floating-point type characteristics.

A `float`, with seven decimal digits of precision, can hold the value `1,234,567` and the value `0.1234567`. However, if you add these two floats together, the result will be rounded to `1234567`, because the exact result requires more precision than the seven significant digits that a `float` can hold. The error introduced by rounding off to seven digits can become large compared to the value computed, especially with repeated calculations. (See also the Advanced Topic, “Unexpected Inequality with Floating-Point Types,” later in this section.)

Internally, the binary floating-point types actually store a binary fraction, not a decimal fraction. Consequently, “representation error” inaccuracies can occur with a simple assignment, such as `double number = 140.6F`. The exact value of `140.6` is the fraction `703/5`, but the denominator of that fraction is not a power of `2`, so it cannot be represented exactly by a binary floating-point number. The value actually represented is the closest fraction with a power of `2` in the denominator that will fit into the `16` bits of a `float`.

Since the `double` can hold a more accurate value than the `float` can store, the C# compiler will actually evaluate this expression to `double number = 140.600006103516` because `140.600006103516` is the closest binary fraction to `140.6` as a `float`. This fraction is slightly larger than `140.6` when represented as a `double`.

> **Guidelines**
> 
> **AVOID** binary floating-point types when exact decimal arithmetic is required; use the `decimal` floating-point type instead.

## ADVANCED TOPIC

### Unexpected Inequality with Floating-Point Types

Because floating-point numbers can be unexpectedly rounded off to non-decimal fractions, comparing floating-point values for equality can be quite confusing. Consider Listing 3.7.

#### OUTPUT 3.6

```
4.2 != 4.200000047683716

4.2 != 4.200000047683716

(float)4.2M != 4.2F

4.200000047683716 != 4.20000028610229

4.200000047683716 != 4.2

4.2F != 4.2D

4.19999980926514 != 4.2

4.2F != 4.2D
```

The `Assert()` methods alert the developer whenever arguments evaluate to false. However, of all the comparisons in this code listing, none of them are in fact equal. In spite of the apparent equality of the values in the code listing, they are not actually equivalent due to the inaccuracies associated with `float` values.

#### Guidelines

AVOID using equality conditionals with binary floating-point types. Either subtract the two values and see if their difference is less than a tolerance, or use the `decimal` type.

You should be aware of some additional unique floating-point characteristics as well. For instance, you would expect that dividing an integer by zero would result in an error—and it does with data types such as `int` and `decimal`. The `float` and `double` types, however, allow for certain special values. Consider Listing 3.8, and its resultant output, Output 3.7.

#### LISTING 3.8: Dividing a Float by Zero, Displaying NaN

```
float n=0f;

// Displays: NaN

System.Console.WriteLine(n / 0);
```

#### OUTPUT 3.7

```
NaN
```

In mathematics, certain mathematical operations are undefined, including dividing zero by itself. In C#, the result of dividing the `float` zero by zero results in a special “Not a Number” value; all attempts to print the output of such a number will result in `NaN`. Similarly, taking the square root of a negative number with `System.Math.Sqrt(-1)` will result in `NaN`.

A floating-point number could overflow its bounds as well. For example, the upper bound of the `float` type is approximately `3.4 × 10³⁸`. Should the number overflow that bound, the result would be stored as “positive infinity” and the output of printing the number would be `Infinity`. Similarly, the lower bound of a `float` type is `−3.4 × 10³⁸`, and computing a value below that bound would result in “negative infinity,” which would be represented by the string `-Infinity`. Listing 3.9 produces negative and positive infinity, respectively, and Output 3.8 shows the results.

#### LISTING 3.9: Overflowing the Bounds of a float

```
// Displays: -Infinity

System.Console.WriteLine(-1f / 0);

// Displays: Infinity

System.Console.WriteLine(3.402823E+38f * 2f);
```

#### OUTPUT 3.8

```
-Infinity

Infinity
```

Further examination of the floating-point number reveals that it can contain a value very close to zero, without actually containing zero. If the value exceeds the lower threshold for the `float` or `double` type, the value of the number can be represented as “negative zero” or “positive zero,” depending on whether the number is negative or positive, and is represented in output as `-0` or `0`.

### Compound Assignment Operators (`+=`, `-=`, `*=`, `/=`, `% =`)

Chapter 1 discussed the simple assignment operator, which places the value of the right-hand side of the operator into the variable on the left-hand side. Compound assignment operators combine common binary operator calculations with the assignment operator. For example, consider Listing 3.10.

#### LISTING 3.10: 常见增量计算

```
int x = 123;

x = x + 2;
```

在此赋值中，首先计算 `x + 2` 的值，然后将计算得到的值赋回给 `x`。由于此类操作执行得相对频繁，因此存在一个赋值运算符来用一个运算符同时处理计算和赋值。`+=` 运算符将运算符左侧变量的值增加运算符右侧的值，如 Listing 3.11 所示。

#### LISTING 3.11: 使用 `+=` 运算符

```
int x = 123;

x += 2;
```

因此，此代码等价于 Listing 3.10。

存在许多其他“复合赋值”运算符来提供类似功能。你也可以使用赋值运算符与减法、乘法、除法和余数运算符一起使用（如 Listing 3.12 所演示）。

#### LISTING 3.12: 其他赋值运算符示例

```
x -= 2;

x /= 2;

x *= 2;

x %= 2;
```

### 增量和减量运算符（`++` , `--`）

C# 包含用于递增和递减计数器的特殊一元运算符。增量运算符 `++` 每次使用时都会将变量增加一。换句话说，Listing 3.13 中显示的所有代码行都是等价的。

#### LISTING 3.13: 增量运算符

```
spaceCount = spaceCount + 1;

spaceCount += 1;

spaceCount++;
```

类似地，你可以使用减量运算符 `--` 将变量递减一。因此，Listing 3.14 中显示的所有代码行也是等价的。

#### LISTING 3.14: 减量运算符

```
lines = lines - 1;

lines -= 1;

lines--;
```

## BEGINNER TOPIC

### 循环中的减量示例

增量和减量运算符在循环中尤其常见，例如本章后面描述的 `while` 循环。例如，Listing 3.15 使用减量运算符按字母表的逆序遍历每个字母。

#### LISTING 3.15: 以降序显示每个字符的 Unicode 值

```
char current;

int unicodeValue;
```
