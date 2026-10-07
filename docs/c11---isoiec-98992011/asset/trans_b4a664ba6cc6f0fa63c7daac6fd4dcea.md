
算术操作数。^{22}

实现可能会为 0 和非浮点数值（如无穷大和 NaN）赋予可能的符号，或将其保持为无符号。在任何此类值均为无符号的地方，本国际标准中关于检索符号的任何要求都应产生一个未指定的符号，且任何设置符号的要求都应被忽略。

浮点类型可表示值的最小范围，是从该类型中可表示的最负有限浮点数到该类型中可表示的最正有限浮点数。此外，如果该类型可以表示负无穷，则该范围扩展到所有实数；同样地，如果该类型可以表示正无穷，则该范围扩展到所有正实数。

<math.h> 和 <complex.h> 中返回浮点结果的库函数其浮点运算 (+, -, *, /) 的准确性是实现定义的，<stdio.h>、<stdlib.h> 和 <wchar.h> 中的库函数执行的浮点表示与字符串表示之间转换的准确性也是实现定义的。实现可以声明准确性未知。

<float.h> 头文件中的所有整数值（除 FLT_ROUNDS 外）应为常数表达式，用于 #if 处理指令；所有浮点值应为常数表达式。除 DECIMAL_DIG、FLT_EVAL_METHOD、FLT_RADIX 和 FLT_ROUNDS 外，三种浮点类型均有独立的名称。除 FLT_EVAL_METHOD 和 FLT_ROUNDS 外，为所有值都提供了浮点模型表示。

浮点加法的舍入模式由实现定义的 FLT_ROUNDS 值表征。^{23}

- -1 不确定
- -0 向零舍入
- -1 近舍入
- -2 向正无穷方向
- -3 向负无穷方向

FLT_ROUNDS 的所有其他值都表征了实现定义的舍入行为。

> 22) IEC 60559:1989 规定了静默 NaN 和信号型 NaN。对于不支持 IEC 60559:1989 的实现，quiet NaN 和 signaling NaN 类型适用于具有相似行为的编码。

> 23) float 的求值通过 <env.h> 中的函数 fetenv 正确反映了执行时舍入模式的任何变化。

## 5.2.4.2

环境 29

## ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留所有

除赋值和强制转换（它们会移除所有额外的范围和精度）外，具有浮点操作数的运算符产生的值、普通算术转换的值以及浮点常数，其求值格式的格式范围和精度可能大于类型所需的范围。求值格式的使用由实现定义的 FLT_EVAL_METHOD 值表征^{(24)

- - 不可终止的；
- 仅按类型的范围和精度求值所有操作和常量；
- 将类型 float 和 double 的操作和常量求值到 double 类型的范围和精度，将类型 long double 的操作和常量求值到 long double 类型的范围和精度；
- 将所有操作和常量求值到 long double 类型的范围和精度

FLT_EVAL_METHOD 的所有其他值表征了实现的行为。

次规格数（subnormals）的存在与否由实现定义的 FLT_HAS_SUBNORM、DBL_HAS_SUBNORM 和 LDBL_HAS_SUBNORM 值表征：

- - 不终止的^{(25)}
- - 缺失^{(6)}（类型不支持次规格数）
- 1（类型支持次规格数）

下列表给出的值应被具有实现定义的常数表达式替换，其值（绝对值）与所示值大或相等，且符号相同：

- - 指数表示的基数，b
FLT_RADIX

> 24) 如果 FLT_EVAL_METHOD 为 1，则求值方法决定表达式的求值格式，此时两个 float _Complex 操作数的积以 double _Complex 格式表示，其部分被求值到 double。

> 25) 表征为“不确定”是指浮点运算不一致地将次规格数表示解释为零，或非零。

> 26) 表征为“缺失”是指浮点运算从非次规格数输入返回次规格数结果，即使该类型包含了次规格数的表示。

## 30 环境
§5.2.4.2

浮点尾数中基为 FLT_RADIX 的位数个数，$p$

- - FLT_MANT_DIG
DBL_MANT_DIG
LDBL_MANT_DIG

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_DECIMAL_DIG
DBL_DECIMAL_DIG
LDBL_DECIMAL_DIG

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_DECIMAL_DIG
DBL_DECIMAL_DIG
LDBL_DECIMAL_DIG

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_DIG
DBL_DIG
LDBL_DIG

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_EXP
DBL_EXP
LDBL_EXP

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_MIN
DBL_MIN
LDBL_MIN

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

## ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

## ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- - FLT_MAX_10_EXP

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_MAX
DBL_MAX
LDBL_MAX

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_MAX
DBL_MAX
LDBL_MAX

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_RADIX
DBL_RADIX
LDBL_RADIX

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_EPSILON
DBL_EPSILON
LDBL_EPSILON

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$

- - FLT_DIG
DBL_DIG
LDBL_DIG

十位数，$n$，使得任何具有 $p$ 个基 $b$ 位的浮点数都可以舍入为具有 $n$ 个十位数的浮点数并转换回而不改变值，

$$
\begin{cases} p \log_{10} b & \text{如果 } b \text{ 是 } 10 的幂} \\ [1 + p \log_{10} b] & \text{否则} \end{cases}
$$
© ISO/IEC 2011 – 保留 ISO/IEC 9899:2011 (E)

环境 29

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

© ISO/IEC 9899:2011 (E)
1 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 2012011 ( 保)

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

- ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 保留

