

## 习题

- 9.1 将下列中缀表达式改写成前缀和后缀形式，并画出语法树：`(3 - 4) / 5 + 6 * 7`

- 9.2 写出（a）后缀算术表达式和（b）前缀算术表达式的 BNF 描述。

- 9.3 修改图 6.12 中的递归下降计算器，使其能将中缀表达式翻译为后缀表达式。

- 9.4 在 LISP 中，下列不带括号的前缀表达式是有歧义的：`+ 3 * 4 5 6`。为什么？给出两种可能的加括号解释。

- 9.5 文中给出了说明短路与运算有用性的例子。请给出一个例子，说明短路或运算的有用性。

- 9.6 编写一个程序，证明 C/C++ 的逻辑运算符采用了短路求值。

- 9.7 编写一个程序，确定你的 C/C++/Ada 编译器对函数实参的求值顺序。

- 9.8 Java 规定所有表达式（包括调用中的实参）都从左到右求值。为什么 Java 这样做，而 C/C++ 不这样做？

- 9.9 我们在第 5 章中指出，`+` 运算符是左结合的，因此在表达式 `a + b + c` 中，先计算 `a + b`，再与 `c` 相加。然而我们在 9.1 节中又指出，表达式 `a + b` 可以先计算 `b` 再计算 `a`。这里存在矛盾吗？你的答案是否也适用于减法运算符？请解释。

- 9.10 假设我们试图在 C 中把短路版本的 and 写成一个函数：`int and(int a, int b) { return a ? b : 0; }`

    - (a) 为什么这不起作用？
    - (b) 如果采用正常序求值，这会起作用吗？为什么？

- 9.11 描述正常序求值的一个好处。描述一个缺点。

- 9.12 考虑表达式 `(x != 0) and (y % x == 0)` 和 `(y % x == 0) and (x != 0)`。理论上，如果 `x == 0`，这两个表达式都可能具有值 false。

    - (a) 在 C 中，这两个表达式哪一个有值？
    - (b) 在 Ada 中，这两个表达式哪一个有值？
    - (c) 编程语言是否可能要求两个表达式都有值？请解释。

- 9.13 描述 C/C++ 运算符 `&&` 和 `||` 与运算符 `&` 和 `|` 之间的区别。后两个运算符是短路的吗？为什么是或为什么不是？

- 9.14 给定两个函数（用 C 语法）：

    ```c
    int cube(int x) { return x*x*x; }
    int sum(int x, int y, int z) { return x + y + z; }
    ```

    描述表达式 `sum(cube(2), cube(3), cube(4))` 的正常序求值过程，并将其与应用序求值进行比较。特别地，每种方法分别执行了多少次加法和乘法？

- 9.15 递归函数的正常序求值存在一个问题。以递归阶乘函数为例来描述这个问题：

    ```c
    int factorial(int n)
    { if (n == 0) return 1; else return n * factorial(n - 1); }
    ```

    提出一个可能的解决方案，并用上述函数以调用 `factorial(3)` 加以说明。

- 9.16 描述使用正常序求值表达式 `factorial(5)` 的过程。减法（如 `5 - 1`）何时执行？乘法（如 `5 * 24`）何时执行？

- 9.17 C 语言坚持在结构化语句（如 while 语句）中用花括号 `{ ... }` 包围语句序列：

    ```text
    while-stmt → while ( expression ) statement
    statement → compound-statement | ...
    compound-statement → { [ declaration-list ] [ statement-list ] }
    statement-list → statement-list statement | statement
    ```

    假设我们去掉复合语句中的花括号，将文法写成如下形式：

    ```text
    while-stmt → while ( expression ) statement
    statement → compound-statement | ...
    compound-statement → [ declaration-list ] [ statement-list ]
    statement-list → statement-list statement | statement
    ```

    证明该文法是二义的。在不回到 C 约定（花括号）的情况下，可以如何修正它？

- 9.18 在 C/C++ 中，switch 语句的 default 分支在某种程度上对应于 if 语句的 else 部分。是否存在类似于 C/C++ 中悬空 else 的“悬空 default”二义性？请解释。

- 9.19 由于 C/C++ 中 switch 语句的 default 分支类似于 if 语句的 else 部分，为什么不使用保留字 `else` 而使用新关键字 `default`？这里适用哪些设计原则？

- 9.20 说明如何用 C/C++ 的 do 语句模拟 while 语句。

- 9.21 说明如何用 C/C++ 的 do 语句模拟 for 语句。

- 9.22 说明如何用 C/C++ 的 for 语句模拟 while 语句。

- 9.23 说明如何用 C/C++ 的 for 语句模拟 do 语句。

- 9.24 你在本章（以及习题 8.14）中看到，语言中存在 if 表达式是有意义的。

    - (a) 存在 while 表达式有意义吗；也就是说，while 表达式能否返回一个值，如果能，返回什么值？
    - (b) 存在 case 或 switch 表达式有意义吗；也就是说，case 表达式能否返回一个值，如果能，返回什么值？
    - (c) 存在 do 或 repeat 表达式有意义吗；也就是说，do 表达式能否返回一个值，如果能，返回什么值？

- 9.25 我们在文中指出，在采用正常序求值的语言中，if 表达式可以写成普通函数。在这样的语言中，while 表达式能否写成普通函数？请解释。

- 9.26 给出适合使用 break 语句和 return 语句退出循环的情形示例。

- 9.27 C/C++ 和 Ada 中 case 语句语义的一个重要区别是：在 Ada 中，未列出的情形会导致运行时错误，而在 C/C++ 中，执行会“贯穿”到 case 语句之后的语句。从第 2 章的设计原则出发，比较这两种约定。哪些原则适用？

- 9.28 （Aho、Sethi 和 Ullman [1986]）C/C++ 中悬空 else 的问题可以通过编写更复杂的语法规则来修复。一种尝试可能如下：

    ```text
    statement → if ( expression ) statement | matched-statement
    matched-statement →
        if ( expression ) matched-statement else statement | ...
    ```

    - (a) 证明该文法仍然是二义的。
    - (b) 如何修正它，使文法无歧义地表达最近嵌套规则？

- 9.29 找到 Java 语言的文法，并描述它如何修复悬空 else 二义性。为此它多用了多少条文法规则？

- 9.30 下面是 C/C++/Java 语法中三种可能的 switch 语句：

    ```c
    int x = 2;
    switch (x) x++;

    int x = 2;
    switch (x)
    { x ++; }

    int x = 2;
    switch (x)
    { case 1: if (x > 2)
      case 2:  x++;
      default: break;
    }
    ```

    - (a) 在 C/C++ 中哪些是合法的？对于合法的，执行后 `x` 的值是多少？
    - (b) 在 Java 中哪些是合法的？对于合法的，执行后 `x` 的值是多少？

- 9.31 下面是 C/C++ 中一个合法的 switch 语句：

    ```c
    int n = ...;
    int q = (n + 3) / 4;
    switch (n % 4)
    {
      case 0:  do {
        n++;
      case 3:
        n++;
      case 2:
        n++;
      case 1:
        n++;
      } while (--q > 0);
    }
    ```

    假设 `n` 的值为 (a) 0；(b) 1；(c) 5；(d) 8。在上述 switch 语句执行后，每种情况下 `n` 的值是多少？你能给出此代码执行后 `n` 值的一般规则吗？如果能，请给出。如果不能，请解释原因。

- 9.32 描述图 9.9（第 9.4 节）中 FORTRAN 意大利面条式代码的效果。编写等价的、不使用 GOTO 的 C/C++ 语句。

- 9.33 Clark [1973] 幽默地将“come from”语句描述为 GOTO 语句的替代品：

    ```text
    10 J = 1
    11 COME FROM 20
    12 PRINT *, J
        STOP
    13 COME FROM 10
    20 J = J + 2
    ```

    这个 FORTRAN 语法的示例程序打印 3 然后停止。为 COME FROM 语句开发一种语义描述。翻译器在为这种语句生成代码时可能遇到什么问题？

- 9.34 C++ 和 Java 的循环常常通过把所有副作用放在测试条件中来写成空循环体，例如下面两个例子：

    ```c
    i = 0;
    while (a[i++] != 0);

    for (i = 0; a[i] != 0; i++);
    ```

    - (a) 这些循环等价吗？
    - (b) 使用这种代码风格有什么优点或缺点？请解释。

