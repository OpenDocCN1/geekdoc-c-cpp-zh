
我们在 for 和 while 循环中广泛使用自增和自减运算符。

虽然 ++m 和 m++ 作为独立语句时含义相同，但当它们用在赋值语句右侧的表达式中时，行为是不同的。请看下面的例子：

```
m = 5;
y = ++m;
```

在这种情况下，y 和 m 的值将都为 6。假如我们将上述语句重写为

```
m = 5;
y = m++;
```

那么，y 的值将为 5，而 m 的值将为 6。前缀运算符先将操作数加 1，然后将结果赋给左侧的变量；相反，后缀运算符先将值赋给左侧的变量，然后再将操作数加 1。程序 5.3 对此进行了说明。

## 程序 5.3 增量运算符示例

```
class IncrementOperator
{
    public static void Main()
    {
        int m = 10, n = 20;
        System.Console.WriteLine(" m = " + m);
        System.Console.WriteLine(" n = " + n);
        System.Console.WriteLine(" ++m = " + ++m);
        System.Console.WriteLine(" n++ = " + n++);
        System.Console.WriteLine(" m = " + m);
        System.Console.WriteLine(" n = " + n);
    }
}
```

程序 5.3 的输出如下：

- m = 10
- n = 20
- ++m = 11
- n++ = 20
- m = 11
- n = 21

当我们在下标变量中使用 ++（或 --）时，情况也类似。也就是说，语句

```
a[i++] = 10
```

等价于

```
a[i] = 10
i = i + 1
```

## 5.7 条件运算符

字符对 ? : 是 C# 中提供的三元运算符。该运算符用于构造如下形式的条件表达式：

exp1 ? exp2 : exp3

其中，exp1、exp2 和 exp3 都是表达式。

运算符 ? : 的工作方式如下：首先对 exp1 求值。如果 exp1 为 true，则对表达式 exp2 求值，并将结果作为条件表达式的值；如果 exp1 为 false，则对 exp3 求值，其值作为条件表达式的值。请注意，两个表达式（exp2 或 exp3）中只有一个会被求值。例如，考虑下面的语句：
a = 10;
b = 15;
x = (a>b) ? a : b;

在本例中，x 将被赋值为 b 的值。这可以通过 if...else 语句来实现，如下所示：
if(a > b)
    x = a;
else
    x = b;

## 5.8 位运算符

C# 支持可用于在位级别操作数据的运算符。这些运算符可用于测试位，或将位向右或向左移动。位运算符不能应用于浮点数据。表 5.7 列出了按位逻辑运算符和移位运算符。

程序 5.4 执行了 C# 中可用的位运算，例如 AND、OR、XOR、左移、右移和按位取反。

## 程序 5.4 位运算符示例

```
using System;
class BitWiseOperator
{
public static void Main()
{
byte bwAnd, bwOr, bwXor;
int bwLeft,bwRight,bwComp;
bwAnd = 15 & 3;
bwOr = 15 | 3;
bwXor = 15 ^ 3;
bwLeft=15<<5;
bwRight=15>>3;
bwComp=~15;
System.Console.WriteLine("—To demonstrate the use of Bitwise Operators available in C# \n");
System.Console.WriteLine("Bitwise AND Operator Result: = {0} \nBitwise OR Operator Result : = {1}",bwAnd, bwOr);
System.Console.WriteLine("Bitwise XOR Operator Result: = {0} \nBitwise SHIFT LEFT Operator Result: = {1}",bwXor,bwLeft);
System.Console.WriteLine("Bitwise SHIFT LEFT Operator Result: = {0}\nBitwise ONE'S COMPLEMENT Operator Result: = {1}",bwRight,bwComp);
}
}
```

## 表 5.7 位运算符

| 运算符 | 含义 |
|---|---|
| & | 按位逻辑与 |
| \| | 按位逻辑或 |
| ^ | 按位逻辑异或 |
| ~ | 按位取反 |
| << | 左移 |
| >> | 右移 |

## 5.9 特殊运算符

C# 支持以下特殊运算符。

- is（关系运算符）
- as（关系运算符）
- typeof（类型运算符）
- sizeof（大小运算符）
- new（对象创建运算符）
- .（点号）（成员访问运算符）
- checked（溢出检查）
- unchecked（禁止溢出检查）

这些运算符将在后续遇到时再逐一讨论。

## 5.10 算术表达式

算术表达式是按照语言语法排列的变量、常量和运算符的组合。到目前为止，我们在已讨论的示例中已经使用了许多简单表达式。C# 可以处理任何复杂的数学表达式。表 5.8 给出了一些 C# 表达式的示例。请记住，C# 没有用于幂运算的运算符。

程序 5.5 对 C# 中可用的各种数值类型（如整型、浮点型、双精度型和十进制型）进行了基本除法运算和取模除法运算。

## 表 5.8 表达式

| 代数表达式 | C# 表达式 |
|---|---|
| axb-c | a*b-c |
| (m+n)(x+y) | (m+n)*(x+y) |
| ab/c | a*b/c |
| 3x²+2x+1 | 3*x*x+2*x+1 |
| x/y + c | x/y+c |

## 程序 5.5 除法示例

```
using System;
class DivisionExample
{
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_79_0.png)

```
static void Main( )
{
    int firstInt, secondInt;
    float firstFloat, secondFloat;
    double firstDouble, secondDouble;
    decimal firstDecimal, secondDecimal;
    firstInt = 12;
    secondInt = 5;
    firstFloat = 12;
    secondFloat = 5;
    firstDouble = 12.55;
    secondDouble = 5;
    firstDecimal = 12;
    secondDecimal = 5;
    Console.WriteLine("--Division Operator usage in Different Types of Numeric Data--");
    Console.WriteLine("\nInteger Division: {0}",firstInt / secondInt );
    Console.WriteLine(" Float Division : {0}",firstFloat / secondFloat);
    Console.WriteLine(" Double Division : {0}",firstDouble / secondDouble);
    Console.WriteLine("Decimal Division: {0}",firstDecimal / secondDecimal);
    Console.WriteLine("\n--Modulo Division Operator usage in Different Types of Numeric Data--");
    Console.WriteLine("\nInteger Modulo Division: {0}",firstInt % secondInt );
    Console.WriteLine(" Float Modulo Division : {0}",firstFloat % secondFloat );
    Console.WriteLine(" Double Modulo Division : {0}",firstDouble % secondDouble );
    Console.WriteLine(" Decimal Modulo Division: {0}", firstDecimal % secondDecimal );
}
```

```
C:\WINNT\system32\cmd.exe

C:\Chapter 5>DivisionExample
--Division Operator usage in Different Types of Numeric Data--
Integer Division: 2
Float Division  : 2.4
Double Division : 2.51
Decimal Division: 2.4

--Modulo Division Operator usage in Different Types of Numeric Data--
Integer Modulo Division: 2
Float Modulo Division  : 2
Double Modulo Division : 2.55
Decimal Modulo Division: 2

C:\Chapter 5>_
```

## 5.11 表达式的求值

表达式通过如下形式的赋值语句进行求值：
variable = expression;
variable 是任何有效的 C# 变量名。当遇到该语句时，首先对表达式求值，然后用其结果替换左侧变量先前的值。在尝试求值之前，必须先为表达式中使用的所有变量赋值。求值语句的示例如下：

```
x = a*b-c;
y = b/c*a;
z = a-b/c+d;
```

运算符周围的空格是可选的，添加空格只是为了提高可读性。当这些语句在程序中使用时，变量 a、b、c 和 d 必须先声明并在表达式中使用前赋值。同样，变量 x、y 和 z 必须事先声明其类型。

## 5.12 算术运算符的优先级

不带任何括号的算术表达式将按照运算符的优先级规则从左到右进行求值。C# 中算术运算符有两个不同的优先级：

- 高优先级  * / %
- 低优先级  + -

基本的求值过程包括对表达式进行两次从左到右的扫描。在第一次扫描中，遇到高优先级运算符（如果有的话）就进行相应运算。在第二次扫描中，遇到低优先级运算符（如果有的话）就进行相应运算。考虑下面的求值语句：

```
x = a-b/3+c*2-1
```

当 a = 9，b = 12，c = 3 时，该语句变为

```
x = 9-12/3+3*2-1
```

并按如下方式求值：

第一遍扫描

- 步骤1：x = 9-4+3*2-1    （12/3 已求值）
- 步骤2：x = 9-4+6-1    （3*2 已求值）

第二遍扫描

- 步骤3：x = 5+6-1    （9-4 已求值）
- 步骤4：x = 11-1    （5+6 已求值）
- 步骤5：x = 10    （11-1 已求值）

不过，通过在表达式中加入括号，可以改变求值顺序。考虑带有括号的同一个表达式，如下所示：

```
9-12/(3+3)*(2-1)
```

使用括号时，括号内的表达式具有最高优先级。如果如上所示连续出现两组或更多组括号，则先对最左边括号内的表达式求值，最后对最右边括号内的表达式求值。下面给出了新的步骤。

第一遍扫描

- 步骤1：9-12/6*(2-1)
- 步骤2：9-12/6*1

第二遍扫描

- 步骤3：9-2*1
- 步骤4：9-2

第三遍扫描

- 步骤5：7

这一次，求值过程由三次从左到右的扫描组成。不过，求值步骤的数量仍为 5 个（即与算术运算符的数量相等）。
