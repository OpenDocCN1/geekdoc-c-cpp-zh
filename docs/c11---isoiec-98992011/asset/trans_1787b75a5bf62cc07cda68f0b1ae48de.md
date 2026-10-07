

## 7.12.14 比较宏

关系运算符和相等运算符支持数值值之间常见的数学关系。对于任何一个有序的数值对，小于、大于和相等这些关系中恰好有一个为真。当参数值值为 NaN 时，关系运算符可能会抛出“无效（invalid）”浮点异常。对于一个 NaN 和一个数值，或者对于两个 NaN，无序关系（unordered relationship）为真。²⁴⁴ 以下子句提供了关系运算符的静默（quiet，即不抛出浮点异常）版本的宏，其他宏有助于编写高效代码，而不会遭受“无效（invalid）”浮点异常。该子句中的概要，`real-floating` 指明参数应为实数浮点类型的表达式²⁴⁵（两个参数不需要具有相同的类型）。²⁴⁶

### 7.12.14.1 isgreater 宏

#### 概要

```c
#include <math.h>
int isgreater(real-floating x, real-floating y);
```

#### 描述

`isgreater` 宏确定其第一个参数是否大于其第二个参数。`isgreater(x, y)` 的值始终等于 `(x > y)`；然而，与 `(x) > (y)` 不同，当 x 和 y 无序时，`isgreater(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

`isgreater` 宏返回 `(x) > (y)` 的值。

### 7.12.14.2 isgreaterqual 宏

#### 概要

```c
#include <math.h>
int isgreaterqual(real-floating x, real-floating y);
```

> 244) IEC 60559 要求内置关系运算符在操作数无序比较时抛出“无效（invalid）”浮点异常，作为未考虑 NaN 的编写程序的错误指示；在这些情况下，结果为假。

> 245) 如果任何参数为整数类型或任何非实数浮点类型的类型，行为是未定义的。

> 246) 用比其语义类型更宽的格式表示的参数如何转换为语义类型是不指定的。

# ISO/IEC 9899:2011 (E)

#### 描述

**isgreaterequal** 宏确定其第一个参数是否大于或等于第二个参数。**isgreaterequal(x, y)** 的值始终等于 **(x) >= (y)**；然而，与 **(x) >= (y)** 不同，**isgreaterequal(x, y)** 在 **x** 和 **y** 无序时不会抛出“无效（invalid）”浮点异常。

#### 返回

**isgreaterequal** 宏返回 **(x) >= (y)** 的值。

### 7.12.14.3 isless 宏

#### 概要

```c
#include <math.h>
int isless(real-floating x, real-floating y);
```

#### 描述

**isless** 宏确定其第一个参数是否小于其第二个参数。**isless(x, y)** 的值始终等于 **(x) < (y)**；然而，与 `(x) < (y)` 不同，当 x 和 y 无序时，`isless(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

**isless** 宏返回 **(x) < (y)** 的值。

### 7.12.14.4 islesqual 宏

#### 概要

```c
#include <math.h>
int islesqual(real-floating x, real-floating y);
```

#### 描述

**islesqual** 宏确定其第一个参数是否小于或等于第二个参数。**islesqual(x, y)** 的值始终等于 **(x) <= (y)**；然而，与 `(x) <= (y)` 不同，当 x 和 y 无序时，`islesqual(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

**islesqual** 宏返回 **(x) <= (y)** 的值。

### 7.12.14.5 islessgreater 宏

#### 概要

```c
#include <math.h>
isslessgreater(real-floating x, real-floating y);
```

#### 描述

`islessgreater` 宏确定其第一个参数是否小于或大于第二个参数。`islessgreater(x, y)` 宏类似于 `(x) < (y) || (x) > (y)`；然而，当 x 和 y 无序时，`islessgreater(x, y)` 不抛出“无效（invalid）”浮点异常。

#### 返回

`islessgreater` 宏返回表达式 `(x) < (y) || (x) > (y)` 的值。

### 7.12.14.6 unordered 宏

#### 概要

```c
#include <math.h>
int unordered(real-floating x, real-floating y);
```

#### 描述

`unordered` 宏确定参数是否无序。

#### 返回

如果参数无序返回 1，否则返回 0。

# ISO/IEC 9899:2011 (E)

#### 描述

关系运算符和相等运算符支持数值值之间常见的数学关系。对于任何一个有序的数值对，小于、大于和相等这些关系中恰好有一个为真。当参数值为 NaNs 时，关系运算符可能会抛出“无效（invalid）”浮点异常。对于一个 NaN 和一个数值，或者对于两个 NaN，无序关系为真。²⁴⁴ 以下子句提供了关系运算符的静默（quiet，即不抛出浮点异常）版本的宏，其他宏有助于编写高效代码，而不会遭受“无效（invalid）”浮点异常。该子句中的概要，`real-floating` 指明参数应为实数浮点类型的表达式²⁴⁵（两个参数不需要具有相同的类型）。²⁴⁶

### 7.12.14.1 isgreater 宏

#### 概要

```c
#include <math.h>
int isgreater(real-floating x, real-floating y);
```

#### 描述

`isgreater` 宏确定其第一个参数是否大于其第二个参数。`isgreater(x, y)` 的值始终等于 `(x > y)`；然而，与 `(x) > (y)` 不同，当 x 和 y 无序时，`isgreater(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

`isgreater` 宏返回 `(x) > (y)` 的值。

### 7.12.14.2 isgreaterqual 宏

#### 概要

```c
#include <math.h>
int isgreaterqual(real-floating x, real-floating y);
```

> 244) IEC 60559 要求内置关系运算符在操作数无序比较时抛出“无效（invalid）”浮点异常，作为未考虑 NaN 的编写程序的错误指示；在这些情况下，结果为假。

> 245) 如果任何参数为整数类型或任何非实数浮点类型的类型，行为是未定义的。

> 246) 用比其语义类型更宽的格式表示的参数如何转换为语义类型是不指定的。

# ISO/IEC 9899:2011 (E)

#### 描述

**isgreaterequal** 宏确定其第一个参数是否大于或等于第二个。**isgreaterequal(x, y)** 的值始终等于 **(x) >= (y)**；然而，与 **(x) >= (y)** 不同，**isgreaterequal(x, y)** 在 **x** 和 **y** 无序时不会抛出“无效（invalid）”浮点异常。

#### 返回

**isgreaterequal** 宏返回 **(x) >= (y)** 的值。

### 7.12.14.3 isless 宏

#### 概要

```c
#include <math.h>
int isless(real-floating x, real-floating y);
```

#### 描述

**isless** 宏确定其第一个参数是否小于其第二个参数。**isless(x, y)** 的值始终等于 **(x) < (y)**；然而，与 `(x) < (y)` 不同，当 x 和 y 无序时，`isless(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

**isless** 宏返回 **(x) < (y)** 的值。

### 7.12.14.4 islesqual 宏

#### 概要

```c
#include <math.h>
int islesqual(real-floating x, real-floating y);
```

#### 描述

**islesqual** 宏确定其第一个参数是否小于或等于第二个参数。**islesqual(x, y)** 的值始终等于 **(x) <= (y)**；然而，与 `(x) <= (y)` 不同，当 x 和 y 无序时，`islesqual(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

**islesqual** 宏返回 **(x) <= (y)** 的值。

### 7.12.14.5 islessgreater 宏

#### 概要

```c
#include <math.h>
isslessgreater(real-floating x, real-floating y);
```

#### 描述 

`islessgreater` 宏确定其第一个参数是否小于或大于第二个参数。`islessgreater(x, y)` 宏类似于 `(x) < (y) || (x) > (y)`；然而，当 x 和 y 无序时，`islessgreater(x, y)` 不抛出“无效（invalid）”浮点异常。

#### 返回

`islessgreater` 宏返回表达式 `(x) < (y) || (x) > (y)` 的值。

### 7.12.14.6 unordered 宏

#### 概要

```c
#include <math.h>
int unordered(real-floating x, real-floating y);
```

#### 描述 

`unordered` 宏确定参数是否无序。

#### 返回

如果参数无序返回 1，否则返回 0。

# ISO/IEC 9899:2011 (E)

#### 描述 

关系运算符和相等运算符支持数值值之间常见的数学关系。对于任何一个有序的数值对，小于、大于和相等这些关系中恰好有一个为真。当参数值为 NaNs 时，关系运算符可能会抛出“无效（invalid）”浮点异常。对于一个 NaN 和一个数值，或者对于两个 NaN，无序关系为真。²⁴⁴ 以下子句提供了关系运算符的静默（quiet，即不抛出浮点异常）版本的宏，其他宏有助于编写高效代码，而不会遭受“无效（invalid）”浮点异常。该子句中的概要，`real-floating` 指明参数应为实数浮点类型的表达式²⁴⁵（两个参数不需要具有相同的类型）。²⁴⁶

### 7.12.14.1 isgreater 宏

#### 概要

```c
#include <math.h>
int isgreater(real-floating x, real-floating y);
```

#### 描述 

`isgreater` 宏确定其第一个参数是否大于其第二个参数。`isgreater(x, y)` 的值始终等于 `(x > y)`；然而，与 `(x) > (y)` 不同，当 x 和 y 无序时，`isgreater(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

`isgreater` 宏返回 `(x) > (y)` 的值。

### 7.12.14.2 isgreaterqual 宏

#### 概要

```c
#include <math.h>
int isgreaterqual(real-floating x, real-floating y);
```

> 244) IEC 60559 要求内置关系运算符在操作数无序比较时抛出“无效（invalid）”浮点异常，作为未考虑 NaN 的编写程序的错误指示；在这些情况下，结果为假。

> 245) 如果任何参数为整数类型或任何非实数浮点类型的类型，行为是未定义的。

> 246) 用比其语义类型更宽的格式表示的参数如何转换为语义类型是不指定的。

# ISO/IEC 9899:2011 (E)

#### 描述 

**isgreaterequal** 宏确定其第一个参数是否大于或等于第二个。**isgreaterequal(x, y)** 的值始终等于 **(x) >= (y)**；然而，与 **(x) >= (y)** 不同，**isgreaterequal(x, y)** 在 **x** 和 **y** 无序时不会抛出“无效（invalid）”浮点异常。

#### 返回

**isgreaterequal** 宏返回 **(x) >= (y)** 的值。

### 7.12.14.3 isless 宏

#### 概要

```c
#include <math.h>
int isless(real-floating x, real-floating y);
```

#### 描述 

**isless** 宏确定其第一个参数是否小于其第二个参数。**isless(x, y)** 的值始终等于 **(x) < (y)**；然而，与 `(x) < (y)` 不同，当 x 和 y 无序时，`isless(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

**isless** 宏返回 **(x) < (y)** 的值。

### 7.12.14.4 islesqual 宏

#### 概要

```c
#include <math.h>
int islesqual(real-floating x, real-floating y);
```

#### 描述 

**islesqual** 宏确定其第一个参数是否小于或等于第二个参数。**islesqual(x, y)** 的值始终等于 **(x) <= (y)**；然而，与 `(x) <= (y)` 不同，当 x 和 y 无序时，`islesqual(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

**islesqual** 宏返回 **(x) <= (y)** 的值。

  7.12.14.5 islessgreater 宏

#### 概要

```c
#include <math.h>
isslessgreater(real-floating x, real-floating y);
```

#### 描述 

`islessgreater` 宏确定其第一个参数是否小于或大于第二个参数。`islessgreater(x, y)` 宏类似于 `(x) < (y) || (x) > (y)`；然而，当 x 和 y 无序时，`islessgreater(x, y)` 不抛出“无效（invalid）”浮点异常。

#### 返回

`islessgreater` 宏返回表达式 `(x) < (y) || (x) > (y)` 的值。

### 7.12.14.6 unordered 宏

#### 概要

```c
#include <math.h>
int unordered(real-floating x, real-floating y);
```

#### 描述 

`unordered` 宏确定参数是否无序。

#### 返回

如果参数无序返回 1，否则返回 0。

# 7.13.1 Save environment

#### 概要

```c
#include <jmp.h>
int setjmp(jmp_buf env);
```

#### 描述 

`setjmp` 宏将其环境保存在 `jmp_buf` 参数中，供 `longjmp` 函数以后使用。

#### 返回

如果从直接调用，`setjmp` 宏返回零。如果是从 `longjmp` 返回，`setjmp` 宏返回非零值。

# 7.13.2 Restore environment

#### 概要

```c
#include <jmp.h>
_Noreturn void longjmp(jmp_buf env, int val);
```

#### 描述 

`longjmp` 函数恢复由对应 `jmp_buf` 参数的最近一次 `setjmp` 宏保存的环境。如果没有这样的调用，或者调用来自另一个线程，或者包含 `setjmp` 宏调用的函数在此期间终止执行，或者 `setjmp` 宏调用位于变量修改类型标识符的作用域内且执行在此期间离开了作用域，行为是未定义的。

在 `longjmp` 完成后，可访问对象具有值，抽象机器的所有组件与调用 `longjmp` 函数时的状态一致，但包含对应 `setjmp` 宏调用的函数的自动存储持续期间具有 `volatile` 限定类型且在 `setjmp` 调用和 `longjmp` 调用之间更改的值是不定的。

#### 返回

在 `longjmp` 完成后，线程执行继续，仿佛 `setjmp` 宏刚刚返回了 `val` 指定的值。`longjmp` 函数不能导致 `setjmp` 宏返回 0；如果 `val` 为 0，`setjmp` 宏返回 1。

5 EXAMPLE `longjmp` 函数将控制权返回 `setjmp` 的调用点可能会导致与变长数组对象相关的内存被释放。

> 248) 对于，通过执行返回语句或因为另一个 longjmp 调用跳转到嵌套函数集中的早先 setjmp 用。

> 249) 这包括但不限于浮点状态位和打开的文件状态。

7.13.2.1

Library

