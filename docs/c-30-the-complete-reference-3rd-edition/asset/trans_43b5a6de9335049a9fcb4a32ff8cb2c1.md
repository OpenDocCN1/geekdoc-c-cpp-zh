
然而，要理解，在递增或递减形式中，x 只被求值一次，而不是两次。这在某些情况下可以提高效率。

递增和递减运算符都可以位于操作数之前（前缀）或之后（后缀）。例如

```
x = x + 1;
```

可以写成

```
++x; // prefix form
```

或者写成

```
x++; // postfix form
```

在前面的示例中，递增作为前缀还是后缀应用没有区别。然而，当递增或递减作为更大表达式的一部分使用时，就存在重要区别。当递增或递减运算符位于其操作数之前时，运算结果是递增后操作数的值。如果运算符位于其操作数之后，则运算结果是递增前操作数的值。考虑以下代码：

```
x = 10;
y = ++x;
```

在这种情况下，y 将被设为 11。这是因为 x 先递增，然后返回其值。然而，如果代码写成

```
x = 10;
y = x++;
```

那么 y 将被设为 10。在这种情况下，先获取 x 的值，然后递增 x，再返回 x 的原始值。在这两种情况下，x 仍然被设为 11。区别在于该运算返回什么。

能够控制递增或递减运算发生的时机具有显著优势。考虑以下程序，它生成一系列数字：

```
// Demonstrate the difference between prefix and
// postfix forms of ++.

using System;

class PrePostDemo {
    static void Main() {
        int x, y;
        int i;

        x = 1;
        Console.WriteLine("Series generated using y = x + x++;");
        for(i = 0; i < 10; i++) {

            y = x + x++; // postfix ++
            Console.WriteLine(y + " ");
        }
        Console.WriteLine();

        x = 1;
        Console.WriteLine("Series generated using y = x + ++x;");
        for(i = 0; i < 10; i++) {
            y = x + ++x; // prefix ++
            Console.WriteLine(y + " ");
        }
        Console.WriteLine();
    }
}
```

输出如下所示：

```
Series generated using y = x + x++;
2
4
6
8
10
12
14
16
18
20
```

```
Series generated using y = x + ++x;
3
5
7
9
11
13
15
17
19
21
```

正如输出所确认的，语句

```
y = x + x++;
```

将 x 的原始值加到 x 上，并将该结果赋给 y。x 的值在获取之后才递增。然而，语句

```
y = x + ++x;
```

获取 x 的值，递增 x，然后将该值加到 x 的原始值上。结果赋给 y。正如输出所示，仅将 ++x 改为 x++，就会使数字序列从偶数变为奇数。

关于前面的示例还有一点：不要让类似

```
x + ++x
```

这样的表达式吓到你。尽管两个运算符背靠背乍看有点令人不安，但编译器会正确处理。只需记住，这个表达式只是将 x 的值加到递增后的 x 值上。

## 关系运算符和逻辑运算符

在“关系运算符”和“逻辑运算符”这两个术语中，关系指的是值彼此之间可能具有的关系，逻辑指的是真值和假值可以连接在一起的方式。由于关系运算符产生 true 或 false 结果，它们经常与逻辑运算符一起使用。因此，这里将它们一起讨论。

关系运算符如下：

| 运算符 | 含义 |
|---|---|
| == | 等于 |
| != | 不等于 |
| > | 大于 |
| < | 小于 |
| >= | 大于或等于 |
| <= | 小于或等于 |

逻辑运算符如下所示：

| 运算符 | 含义 |
|---|---|
| & | 与 |
| \| | 或 |
| ^ | 异或（XOR） |
| \|\| | 短路或 |
| && | 短路与 |
| ! | 非 |

关系运算符和逻辑运算符的结果是一个 bool 值。

一般来说，可以使用 == 和 != 比较对象是否相等或不相等。然而，比较运算符 <、>、<= 或 >= 只能应用于支持排序关系的那些类型。因此，所有关系运算符都可以应用于所有数值类型。然而，bool 类型的值只能比较相等或不相等，因为 true 和 false 值没有顺序。例如，true > false 在 C# 中没有意义。

对于逻辑运算符，操作数必须是 bool 类型，逻辑运算的结果也是 bool 类型。逻辑运算符 &、&&、|、||、^ 和 ! 根据以下真值表支持基本逻辑运算 AND、OR、XOR 和 NOT：

| p | q | p & q | p \| q | p ^ q | !p |
|---|---|---|---|---|---|
| 假 | 假 | 假 | 假 | 假 | 真 |
| 真 | 假 | 假 | 真 | 真 | 假 |
| 假 | 真 | 假 | 真 | 真 | 真 |
| 真 | 真 | 真 | 真 | 假 | 假 |

如表所示，当且仅当一个操作数为 true 时，异或运算的结果为 true。

下面是一个演示若干关系运算符和逻辑运算符的程序：

```
// Demonstrate the relational and logical operators.

using System;

class RelLogOps {
  static void Main() {
    int i, j;
    bool b1, b2;

    i = 10;
    j = 11;
    if(i < j) Console.WriteLine("i < j");
    if(i <= j) Console.WriteLine("i <= j");
    if(i == j) Console.WriteLine("this won't execute");
    if(i != j) Console.WriteLine("i != j");
    if(i > j) Console.WriteLine("this won't execute");
    if(i >= j) Console.WriteLine("this won't execute");

    b1 = true;
    b2 = false;
    if(b1 & b2) Console.WriteLine("this won't execute");
    if(!(b1 & b2)) Console.WriteLine("!(b1 & b2) is true");
    if(b1 | b2) Console.WriteLine("b1 | b2 is true");
    if(b1 ^ b2) Console.WriteLine("b1 ^ b2 is true");
  }
}
```

该程序的输出如下所示：

```
i < j
i <= j
i != j
!(b1 & b2) is true
b1 | b2 is true
b1 ^ b2 is true
```

C# 提供的逻辑运算符执行最常用的逻辑运算。然而，形式逻辑规则还定义了其他若干运算。这些其他逻辑运算可以使用 C# 支持的逻辑运算符来构造。因此，C# 提供了一组足以构造任何其他逻辑运算的逻辑运算符。例如，另一种逻辑运算是蕴含。蕴含是一种二元运算，只有当左操作数为 true 且右操作数为 false 时，结果才为 false。（蕴含运算反映了 true 不能蕴含 false 这一思想。）因此，蕴含运算符的真值表如下所示：

| p | q | p 蕴含 q |
|---|---|---|
| 真 | 真 | 真 |
| 真 | 假 | 假 |
| 假 | 假 | 真 |
| 假 | 真 | 真 |

蕴含运算可以使用 ! 和 | 运算符的组合来构造，如下所示：

```
!p | q
```

以下程序演示了这种实现：

```
// Create an implication operator in C#.

using System;

class Implication {
    static void Main() {
        bool p=false, q=false;
        int i, j;

        for(i = 0; i < 2; i++) {
            for(j = 0; j < 2; j++) {
                if(i==0) p = true;
                if(i==1) p = false;
                if(j==0) q = true;
                if(j==1) q = false;

                Console.WriteLine("p is " + p + ", q is " + q);
                if(!p | q) Console.WriteLine(p + " implies " + q + " is " + true);
                Console.WriteLine();
            }
        }
    }
}
```

输出如下所示：

```
p is True, q is True
True implies True is True

p is True, q is False

p is False, q is True
False implies True is True

p is False, q is False
False implies False is True
```

## 短路逻辑运算符

C# 提供了其 AND 和 OR 逻辑运算符的特殊短路版本，可用于生成更高效的代码。要理解原因，请考虑以下情况。在 AND 运算中，如果第一个操作数为 false，那么无论第二个操作数是什么值，结果都为 false。在 OR 运算中，如果第一个操作数为 true，那么无论第二个操作数的值是什么，运算结果都为 true。因此，在这两种情况下，都不需要求值第二个操作数。通过不求值第二个操作数，可以节省时间并生成更高效的代码。

短路 AND 运算符是 &&，短路 OR 运算符是 ||。如前所述，它们的普通对应运算符是 & 和 |。普通版本和短路版本之间的唯一区别是，普通运算符总是会求值每个操作数，而短路版本仅在必要时才求值第二个操作数。

下面是一个演示短路 AND 运算符的程序。该程序判断 d 中的值是否为 n 的因子。它通过执行取模运算来实现。如果 n / d 的余数为零，则 d 是因子。然而，由于取模运算涉及除法，因此使用 AND 的短路形式来防止除零错误。

```
// Demonstrate the short-circuit operators.

using System;

class SCops {
    static void Main() {
        int n, d;

        n = 10;
        d = 2;
        if(d != 0 && (n % d) == 0)
            Console.WriteLine(d + " is a factor of " + n);

        d = 0; // now, set d to zero

        // Since d is zero, the second operand is not evaluated.
        if(d != 0 && (n % d) == 0)
            Console.WriteLine(d + " is a factor of " + n);

        // Now, try the same thing without short-circuit operator.
        // This will cause a divide-by-zero error.
        if(d != 0 & (n % d) == 0)
            Console.WriteLine(d + " is a factor of " + n);
    }
}
```

为防止除零错误，if 语句首先检查 d 是否等于零。如果为零，那么短路 AND 就在该处停止，不执行取模
