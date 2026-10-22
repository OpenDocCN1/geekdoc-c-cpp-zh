

```
chcount++;
}
```

该代码片段回显非空格字符并对其计数。

## goto 命令

goto 语句使程序控制跳转到带有指定标签的语句。冒号用于将带标签的语句与其标签分隔开。标签名遵循变量名的命名规则。带标签的语句可以出现在 goto 之前或之后。

## 格式

```
goto label;
label : statement
```

## 示例

```
top : ch = getchar();
    if (ch != 'y')
    goto top;
```

## 第 V 节：标准 ANSI C 库（含 C99 和 C11 增补）

ANSI C 库将函数分为若干组，每组都有对应的头文件。本附录对库进行概述，列出了头文件并简要描述其相关函数。其中一些函数（例如几个 I/O 函数）在正文中有更详细的讨论。更一般地，要获取完整描述，请查阅你的实现的文档、参考手册，或尝试在线参考，例如：http://www.acm.uiuc.edu/webmonkeys/book/c_guide/

## 诊断：assert.h

该头文件将 assert() 定义为一个宏。在包含 assert.h 头文件之前定义宏标识符 NDEBUG 会使 assert() 宏失效。用作参数的表达式通常是关系表达式或逻辑表达式，如果程序运行正常，该表达式在程序中的那个位置应为真。表 RS.V.1 描述了 assert() 宏。

## 对称点的连线与对称轴有什么关系？

探究：如图13.1-4，在硬纸板上画一个三角形，并画出它的对称轴 l，分别作出这个三角形关于直线 l 对称的图形。

(1) △ABC 与 △A'B'C' 关于直线 l 对称，延长对应点 A 和 A' 的连线，你发现了什么？

(2) 量一量对应点 A 和 A' 到对称轴 l 的距离，你发现了什么？

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_955_0.png)

图13.1-4

可以发现：对应点 A 和 A' 的连线与对称轴 l 垂直，并且被对称轴 l 平分。

> 如果两个图形关于某条直线对称，那么对称轴是任何一对对应点所连线段的垂直平分线。

类似的，轴对称图形的对称轴，是任何一对对应点所连线段的垂直平分线。

例如，图13.1-3中，l 垂直平分 AA'，也垂直平分 BB'。

如果有一个图形和一条直线，如何画出这个图形关于这条直线对称的图形呢？

例1 如图13.1-5，已知△ABC 和直线 l，画出与△ABC 关于直线 l 对称的图形。

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_955_1.png)

| 原型 | 描述 |
|---|---|
| double carg(double complex z); | 返回 z 的相位角（或辐角），单位为弧度。 |
| double cimag(double complex z); | 以实数形式返回 z 的虚部。 |
| double complex conj(double complex z); | 返回 z 的共轭复数。 |
| double complex cproj(double complex z); | 返回 z 在黎曼球面上的投影。 |
| double complex CMPLX(double x,double y); | 返回一个复数，其实部为 x，虚部为 y（C11）。 |
| double creal(double complex z); | 以实数形式返回 z 的实部。 |

## 字符处理：ctype.h

这些函数接受 int 参数，这些参数应能表示为 unsigned char 值或 EOF；提供其他值的效果未定义。在表 RS.V.4 中，“true”用作“非零值”的简写。某些定义的解释取决于当前的区域设置（locale），该设置由 locale.h 的函数控制；表中显示的是“C”区域设置下的解释。

## 表 RS.V.4 字符处理函数

| 原型 | 描述 |
|---|---|
| int isalnum(int c); | 如果 c 是字母数字（字母或数字），则返回真。 |
| int isalpha(int c); | 如果 c 是字母，则返回真。 |
| int isblank(int c); | 如果 c 是空格或水平制表符，则返回真。（C99） |
| int iscntrl(int c); | 如果 c 是控制字符（如 Ctrl+B），则返回真。 |
| int isdigit(int c); | 如果 c 是数字，则返回真。 |
| int isgraph(int c); | 如果 c 是除空格以外的任何可打印字符，则返回真。 |
| int islower(int c); | 如果 c 是小写字符，则返回真。 |
| int isprint(int c); | 如果 c 是可打印字符，则返回真。 |
| int ispunct(int c); | 如果 c 是标点字符（除空格或字母数字字符以外的任何可打印字符），则返回真。 |

| 宏 | 表示 |
|---|---|
| FE_UPWARD | 向上取整 |
| FE_DFL_ENV | 表示默认环境，类型为 const fenv_t *。 |

表 RS.V.8 显示了 fenv.h 头文件中的标准函数原型。请注意，参数值和返回值通常与表 RS.V.7 中的宏相对应。例如，FE_UPWARD 是 fesetround() 的一个合适参数。

## 表 RS.V.8 fenv.h 类型

| 原型 | 描述 |
|---|---|
| void feclearexcept(int excepts); | 清除由 excepts 表示的异常。 |
| void fegetexceptflag(fexcept_t *flagp, int excepts); | 将 excepts 指示的浮点状态标志的状态存储到 flagp 指向的对象中。 |
| void feraiseexcept(int excepts); | 引发 excepts 指定的异常。 |
| void fesetexceptflag(const fexcept_t *flagp, int excepts); | 将 excepts 指示的浮点状态标志设置为 flagp 提供的值；flagp 应通过之前调用 fegetexceptflag() 设置。 |
| int fetestexcept(int excepts); | excepts 指定要查询的状态标志；函数返回这些指定状态标志的按位或。 |
| int fegetround(void); | 返回当前舍入方向。 |
| int fesetround(int round); | 将舍入方向设置为 round 提供的值；当且仅当成功时返回 0。 |
| void fegetenv(fenv_t *envp); | 将当前环境存储到 envp 指向的位置。 |
| int feholdexcept(fenv_t *envp); | 将当前浮点环境保存到 envp 指向的位置，清除浮点状态标志，然后如果可能，安装非停止模式，在该模式下即使出现异常也继续执行；当且仅当成功时返回 0。 |
| void fesetenv(const fenv_t *envp); | 安装由 envp 表示的浮点环境；envp 应指向由先前调用 fegetenv() 或 feholdexcept() 设置的数据对象，或指向浮点环境宏。 |

| 原型 | 描述 |
|---|---|
| void feupdateenv
(const fenv_t *envp); | 该函数将当前引发的浮点异常保存在自动存储中，安装 envp 指向的对象所表示的浮点环境，然后引发已保存的浮点异常；envp 应指向由先前调用 fegetenv() 或 feholdexcept() 设置的数据对象，或指向浮点环境宏。 |

## 浮点特性：float.h

float.h 头文件定义了几个表示各种限制和参数的宏。表 RS.V.9 列出了这些宏，其中 C11 新增部分以斜体显示。许多宏涉及以下浮点表示模型：

x = s b^e sum_{k=1}^{p} f_k b^{-k}

如果第一个数字 f1 非零（且 x 非零），则该数称为规范化浮点数。本附录的第 VIII 节更完整地解释了这一点以及其中一些宏的含义。

## 表 RS.V.9 float.h 宏

| 宏 | 表示 |
|---|---|
| FLT_ROUNDS | 默认舍入方案 |
| FLT_EVAL_METHOD | 计算浮点表达式的默认方案 |
| FLT_HAS_SUBNORM | float 次正规数存在与否 |
| DBL_HAS_SUBNORM | double 次正规数存在与否 |
| LDBL_HAS_SUBNORM | long double 次正规数存在与否 |
| FLT_RADIX | 指数表示中使用的基数（b）（最小值为 2） |
| FLT_MANT_DIG | float 的尾数中以 FLT_RADIX 为基数的位数（p） |
| DBL_MANT_DIG | double 的尾数中以 FLT_RADIX 为基数的位数（p） |
| LDBL_MANT_DIG | long double 的尾数中以 FLT_RADIX 为基数的位数（p） |
| FLT_DECIMAL_DIG | 一个 float 可以从基数 b 转换为十进制再转换回基数 b 而值不变所需的十进制位数（最小值为 6） |

