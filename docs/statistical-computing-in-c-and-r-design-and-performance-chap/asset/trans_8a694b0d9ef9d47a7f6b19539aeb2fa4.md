

# 练习题 31

![](img/b50973a0535e1d41c799ab78355b19f6_47_0.png)

图 2.3 West 算法的边界与实证结果

例如，用于创建材料中部分内容的的机器.机器信息显示为

```
noquote((Format(.Machine))
double.eps double.neg.eps double.xmin
2.220446e-16 1.110223e-16 2.225074e-308
double.xmax double.base double.digits
1.797693+308 2 53
double.rounding double.guard
5 0 -52
double.neg.ulpdigits double.exponent double.min
53 11 -1022
double.max.exp integer.max size.long
1024 2147483648 4
size.oflong size.double size.pointer
8 16 44
```

列表组件的某些名称可以通过查找 .Machine 的 R 帮助页面来解读。而其他名称的含义则可以舍入。特别是，.double.digits 变量的值 53 表示双精度浮点数（double）尾数部分由 53 位组成（即 52 位加上一个用于归一化尾数的隐含位），这对应于 IEEE 浮点标准。

R 语言中有几个实用的特性用于生成 .Machine 中信息的打印表示。首先，`format` 函数对其输入进行排序以实现“美化打印”。随后，`noquote` 函数消除了在打印输出中引号的使用。

# 2.8 练习题

- 2.1. 证明在 $m$ 位中可以存储的最大整数是 $2^m - 1$。

# 32 数字的计算机表示

2. 编写、编译并运行 C++ 代码，在屏幕上打印 "Hello World!"。然后，修改你的程序，使其使用你的名字问候世界。为了实现这一点，请使用列表 2.3 中的 `argv`。如果你在命令行输入你的名字，它将可用 `argv[1]`，因此你可以使用输出插入运算符 `<<` 将 "Hello World from" 和 `argv[1]` 写在一起。你会如何修改它以在问候中使用全名？

2.3. 设 $x$ 为 $[0,1)$ 中的一个数，令 $y$ 表示小于或等于该实数的整数。

a) 证明以下算法将返回 $x$ 的二进制表示中的前 $m$ 个项 $b_1, \dots, b_m$。(Conte and De Boer 1972)

```
Algorithm 2.4 二进制表示算法
c = x
for j = 2 to m do
  bj = [2c]
  c = 2c - bj
end
```

b) C 语言中用于 $||$ 的函数是 `floor`。使用它创建一个程序，该程序接受一个位于 $[0,1)$ 之间的浮点型变量 $x$ 作为输入，并返回其二进制展开的前五个系数 (2.2)。现在，在使用 `floor` 时，你需要通过语句 `#include <cmath>` 包含数学库。

2.4. 另一个位运算符是异或（XOR）运算符 `^`。如果 $k1$ 和 $k2$ 是整数，当 $k1$ 或 $k2$ 中对应的位之一为 1 时，$k1 \wedge k2$ 的位为 1，否则为 0。

a) 使用 C++ 开发一个基于部分 a 的二进制算法。在两个位的相加中引入一个进位位。

b) 在 C++ 中实现部分 a 中的算法。假设你处理的是长度位的数字，并使用无符号整数进行计算。

2.5. 考虑两个浮点数集合 $\tilde{x}_1, \dots, \tilde{x}_n$ 和 $\tilde{y}_1, \dots, \tilde{y}_k$ 的除法，它们具有 $m$ 位尾数。

假设精确舍入，

$(\tilde{x}_1 \dots \tilde{x}_n)/(\tilde{y}_1 \dots \tilde{y}_k) = ((\tilde{x}_1 \dots \tilde{x}_n)/(\tilde{y}_1 \dots \tilde{y}_k))(1+E)$

其中

$1-2^{-(m+1)}^{(k+1)} \le E \le (1+2^{-(m+1)})^{(k+1)}$

b) 使用部分 a 中得到的 $1+E$ 的边界，证明如果 $n-k$ 相对于 $2^{m+1}$ 较小，则除法的相对误差应该表现像 $(n-k)2^{-(m+1)}$ 的倍数。

2.6. 证明浮点除法的结果。证明或反驳 $\tilde{x}(\tilde{y}\tilde{z}) = \tilde{(\tilde{x}\tilde{y})z}$。

2.7. 对于正数 $x$，令 $y=1+x$。如果 $y$ 根据 IEEE 标准被存储为浮点型 $\hat{y}$，在什么种条件下 $\hat{y}=1$？

2.8. 在 IEEE 标准下，双精度浮点数（double）的尾数分配了 52 位。

a) 给出与舍入和截断（chopping）相关的相关的相对误差边界。

b) 可以期望获得多少位小数精度？

c) 在 IEEE 标准下，double 的尾数分配了 52 位。

a) 给出与舍入最近值和截断相关的相对误差边界。

b) 可以期望获得多少位小数精度？

c) 在 IEEE 标准下，double 的尾数分配了 52 位。

