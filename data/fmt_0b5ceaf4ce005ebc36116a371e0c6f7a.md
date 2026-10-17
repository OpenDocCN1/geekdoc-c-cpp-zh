
描述

`signal`函数选择了处理信号编号`sig`的三种方式之一。如果`func`的值为`SIG_DFL`，将发生该信号的默认处理。如果`func`的值为`SIG_IGN`，则该信号将被忽略。否则，`func`应指向一个在信号发生时被调用的函数。这种信号的调用是由或

<sup>20}</sup>"未来方向" (7.33.10)。

（递归地）通过调用任何进一步函数（标准库中的函数除外），$^{291}$被称为`sig handler`（信号处理函数）。

当信号发生且`func`指向一个函数时，执行等同于`signal(sig, SIG_DFL)`的操作，还是由实现防止定义的信号集（包括`sig`）在信号处理完成之前发生，是由实现定义的（implementation-defined）的：在这种情况下，对于`SIGILL`，实现也可以交替定义为不采取任何操作。随后，执行等同于`<+func (sig)`的操作。当函数返回时，如果`sig`的值为`SIGFPE`、`SIGSEGV`或任何与计算出的异常对应的实现定义的返回值，则其行为是未定义的；程序将从被中断的点继续执行。

如果信号是由于调用`abort`或`raise`函数而产生的，则信号处理函数不应调用`raise`函数。

如果信号不是由于调用`abort`或`raise`函数而产生的，如果信号处理函数引用了任何具有静态存储时间或线程存储时间的对象，且该对象不是无锁原子对象，也不是声明为`constptr`存储类的值（除非通过给`volatile sig_atomic_t`赋值），或者信号处理函数调用了标准库中的任何函数（以下函数外），则其行为是未定义的：

- `abort`函数，
- `_Exit`函数，
- `quick_exit`函数，
- `<stdatomic.h>`中的函数（在明确有其他说明的情况下，当原子参数是无锁的），
- 带有任何原子参数的`atomic_is_lock_free`函数，或
- 第一个参数等于导致处理器被调用的信号数的`signal`函数。此外，如果对`signal`函数的此类调用导致`SIGERR`，则由`errno`指定的对象具有不确定的表示。$^{292}$

在程序启动时，对于按照实现定义定义的某些信号，等同于

```
signal(sig, SIG_IGN);
```

的操作可能会以实现定义选定的方式被执行；而等同于

```
signal(sig, SIG_DFL);
```

的操作对于实现定义的所有其他信号将被执行。

在多线程程序中使用此操作会导致未定义的行为。实现的行为应当表现为没有库函数调用`signal`函数。

## 返回值

如果请求可以被，`signal`函数返回对于指定信号`sig`的最近一次成功调用`signal`时`func`的值。否则，返回`SIG_ERR`值，并在`errno`中存储一个正值。

前向引用：`abort`函数 (7.24.5.1)，`exit`函数 (7.24.5.4)，`_Exit`函数 (7.24.5.5)，`quick_exit`函数 (7.24.5.7)。

> $^{291}$这包括通过标准库函数间接调用的函数（例如，通过`abort`函数调用的`SIGABRT`处理函数）。
> $^{292}$如果任何信号是由异步信号处理函数生成的，其行为是未定义的。

# ISO/IEC 9899:2024(en)

## 7.14.3 发送信号 (Send signal)

### 7.14.3.1 raise 函数

概要

```
#include <signal.h>

int raise(int sig);
```

描述

`raise`函数对信号`sig`执行 7.14.2.1 中描述的操作。如果调用了信号处理函数，则`raise`函数在信号处理函数返回之前不应返回。

返回值

`raise`函数成功时返回零，失败时返回非零。

## 7.15 对齐 (Alignment) <stdalign.h>

头文件 `<stdalign.h>` 不提供内容。

# ISO/IEC 9899:2024(en)

## 7.16 变量 (Variable) <stdarg.h>

### 7.16.1 通用

`<stdarg.h>`声明了宏，用于处理可变参数列表。`va_list`是一个用于保存可变参数信息的类型。`va_start`、`va_arg`、`va_end`和`va_copy`宏用于操作可变参数。`va_start`宏初始化`ap`以供后续的`va_arg`和`va_end`使用。在没有`va_end`用的情况下，不应调用`va_start`或`va_copy`宏重新初始化`ap`。`va_start`宏只评估第一个参数。如果任何额外的参数展开为不平衡的括号，或无法转换为标记的预处理标记，其行为是未定义的。

### 7.16.2 可变参数 (Variable arguments)

#### 7.16.2.1 通用

`<stdarg.h>`声明了宏，用于处理可变参数列表。`va_list`是一个用于保存可变参数信息的类型。`va_start`、`va_arg`、`va_end`和`va_copy`宏用于操作可变参数。`va_start`宏初始化`ap`以供后续的`va_arg`和`va_end`使用。在没有`va_end`用的情况下，不应调用`va_start`或`va_copy`宏重新初始化`ap`。`va_list`是一个用于保存可变参数信息的类型。`va_start`、`va_arg`、`va_end`和`va_copy`宏用于操作可变参数。`va_start`宏初始化`ap`以供后续的`va_arg`和`va_end`使用。在没有`va_end`用的情况下，不应调用`va_start`或`va_copy`宏重新初始化`ap`。

（注：此处原文文本似乎存在部分重复或逻辑混乱，已根据上下文尽可能翻译并对齐）

#### 7.16.2.2 va_arg 宏

概要

```
#include <stdarg.h>

type va_arg(va_list ap, ...);
```

描述

`va_arg`宏展开为具有指定类型的表达式。`ap`必须由`va_start`宏或`va_copy`宏初始化。在没有`va_end`用的情况下，不应调用`va_arg`。如果类型根据默认规则进行提升，其行为是未定义的，除非：

- 类型类型都是指针；
- 一个类型是有符号整数类型，另一个是无符号整数类型，且值在两种类型中均可表示；
- 一个类型是`void`指针，另一个是字符类型；

返回值

在`va_start`之后的第一次调用`va_arg`返回第一个参数的值。后续调用返回后续参数的值。

#### 7.16.2.3 va_copy 宏

概要

```
#include <stdarg.h>

void va_copy(va_list dest, va_list src);
```

描述

`va_copy`宏将`dest`初始化为`src`的拷贝，就像对`dest`应用了`va_start`随后按照相同的序列调用`va_arg`到当前状态一样。在没有`va_end`用的情况下，不应调用`va_copy`或`va_start`宏重新初始化`dest`。

返回值

`va_copy`宏不返回值。

#### 7.16.2.4 va_end 宏

概要

```
#include <stdarg.h>

void va_end(va_list ap);
```

描述

`va_end`宏允许从`va_start`宏展开的可变参数列表函数或从`va_copy`宏展开的函数正常返回。`va_end`宏可能会修改`ap`使其不再可用（除非被`va_start`或`va_copy`宏重新初始化）。如果没有相应的`va_start`或`va_copy`宏调用，或者在返回之前没有调用`va_end`宏，其行为是未定义的。

返回值

`va_end`宏不返回值。

#### 7.16.2.5 va_start 宏

概要

```
#include <stdarg.h>

void va_start(va_list ap, ...);
```

描述

`va_start`宏初始化`ap`以供后续的`va_arg`和`va_end`宏使用。在没有`va_end`用的情况下，不应调用`va_start`或`va_copy`宏重新初始化`ap`。传递给`va_start`的第一个参数会被求值。如果任何额外的参数展开为不平衡的括号，或无法转换为标记的预处理标记，其行为是未定义的。

# ISO/IEC 9899:2024(en)

注意 该宏仅允许为`va_start`传递额外的参数，以兼容库的旧版本。

返回值

`va_start`宏不返回任何值。

推荐做法

除`va_start`宏的第一个参数之外的额外参数可能会被展开并在未评估的未知上下文中中使用。例如，实现会对`va_start`调用中的潜在错误输入进行诊断，如下：

```c
#include <stdarg.h>

void miaou (...) {
    va_list vl;
    va_start(vl, 1, 3.0, "12", xd); // 鼓励进行诊断
    /* ... */
    va_end(vl);
}
```

同时，与此文档较旧版本一致的`va_start`使用不应产生诊断：

```c
#include <stdarg.h>

void neigh (int last_arg, ...) {
    va_list vl;
    va_start(vl, last_arg); // 无诊断
    /* ... */
    va_end(vl);
}
```

示例 1 函数`f1`将参数收集到一个指向字符串的数组中（但不超过`MAXARGS`），然后将该数组作为单个参数传递给函数`f2`。第一个参数指定的指针数量为`f1`。

```c
#include <stdarg.h>
#define MAXARGS 31
void f1(int n_ptrs, ...) {
    va_list ap;
    char *array[MAXARGS];
    int ptr_no = 0;
    if (n_ptrs > MAXARGS) {
        n_ptrs = MAXARGS;
        va_start(ap);
        while (ptr_no < n_ptrs)
            array[ptr_no++] = va_arg(ap, char);
        va_end(ap);
    }
    f2(n_ptrs, array);
}
```

每次调用`f1`都要求具有该函数的定义或如下的声明：

```c
void f1(int, ...);
```

示例 2 函数`f3`类似，但在指定数量的参数后保存了可变参数列表的状态；该列表已调用过一次，列表的末尾部分再次收集并传递给函数`f4`。

```c
#include <stdarg.h>
#define MAXARGSGS 31
void f3(int n_ptrs, int f4_after, ...)
{
    va_list ap, ap_save;
    char *array[MAXARGSGS];
    int *ptr_no = 0;
    if (n_ptrs > MAXARGSGS)
        n_ptrs = MAXARGSGS;
    va_start(ap);
    while (*ptr_no < n_ptrs) {
        array[*ptr_no++] = va_arg(ap, char *);
        if (*ptr_no == f4_after)
            va_copy(ap_save, ap);
    }
    va_end(ap);
    f2(n_ptrs, array);
    // 现在处理保存的副本。
    n_ptrs -= f4_after;
    ptr_no = 0;
    while (*ptr_no < n_ptrs)
        array[*ptr_no++] = va_arg(ap_save, char *);
    va_end(ap_save);
    f4(n_ptrs, array);
}
```

示例 3 函数`f5`与`f1`类似，但不是通过第一个参数传递显式的字符串数量，而是用空指针终止参数列表。

```c
#include <stdarg.h>
#define MAXARGSGS 31
void f5(...)
{
    va_list ap;
    char *array[MAXARGSGS];
    int *ptr_no = 0;
    va_start(ap);
    while (*ptr_no < MAXARGSGS) {
        char *ptr = va_arg(ap, char *);
        if (!ptr)
            break;
        array[*ptr_no++] = ptr;
    }
    va_end(ap);
    f6(ptr_no, array);
}
```

每次调用`f5`都要求具有该函数的定义或如`void f5(...);`的声明，并且隐含要求最后一个参数为空指针。

## 7.17 原子操作 <stdatomic.h>

### 7.17.1 介绍

`<stdatomic.h>`头文件定义了多个宏以及用于线程间共享数据原子操作的类型和函数。

定义了`__STDC_NO_ATOMICS__`的实现不提供此头文件，也不支持其任何功能。

宏

```
__STDC_VERSION_H__
```

是一个值等于`2023L`的整数常量。定义的宏是无锁的

```
ATOMIC_BOOL_T_FREE
ATOMIC_CHAR_T_FREE
ATOMIC_CHAR8_T_FREE
ATOMIC_CHAR16_T_FREE
ATOMIC_CHAR32_T_FREE
ATOMIC_SHORT_T_FREE
ATOMIC_INT_T_FREE
ATOMIC_LONG_T_FREE
ATOMIC_POINTER_T_FREE
```

展开为适用于预处理器的常量表达式，并指示原子类型（有符号和无符号）的无锁属性。

```ATOMIC_FLAG_INIT
```

展开为`atomic_flag`类型对象的初始化器

类型包括

```
memory_order
```

这是一个标识排序约束的枚举类型；

```
atomic_flag
```

是一个表示无锁原语原子标志的结构；以及多种整数类型的原子变体。

在以下概要中：

- `A`指一个原子类型。
- `C`指其对应的非原子类型。
- 对于原子操作，`M`指参数的类型。对于指针类型，`M`指`ptrdiff_t`。

以`_explicit`结尾的函数与`memory_order_seq_cst`参数对应的`_explicit`函数具有相同的语义。

（参见“未来方向”）

## 7.17.2 初始化

### 7.17.2.1 通用

自动存储期的对象未初始化，或具有分配存储期的对象具有不确定表示；同样，对任何原子对象的非原子存储（直接通过`memcpy`或`memset`）具有不确定表示。静态或线程存储期原子对象的显式或默认初始化保证产生`volatile`值。

在通过原子操作设置为有效值之前对原子对象的并发访问会导致数据竞态。如果在调用`abort`或`raise`函数的结果之外发生了信号，且信号处理程序读取或修改了具有不确定表示的原子对象，则行为是未定义的。

示例 如果`guide`和`head`在文件作用域或块作用域，以下定义确保了有效状态。无论如何初始化，对它们执行的原子操作都是定义的。

```c
atomic_int guide = 42;
static atomic_void head;
```

### 7.17.2.2 atomic_init 函数

```c
#include <atomic.h>
void atomic_init(volatile A *obj, C value);
```

描述

`atomic_init`函数将`obj`指向的原子对象初始化为`value`，同时初始化实现可能需要携带的状态。如果对象没有声明类型，调用后类型为`A`。

尽管此函数初始化了原子对象，但它并没有避免数据竞态；即使通过原子操作并发访问正在初始的对象会导致数据竞态。

如果在调用`abort`或`raise`函数的结果之外发生了信号，且信号处理程序调用了`atomic_init`函数，则行为是未定义的。

返回值

`atomic_init`函数不返回任何值。

示例

```c
atomic_int guide;
atomic_init(&guide, 42);
```

（参见“未来方向”（7.33.11））

## 7.17.3 顺序与一致性

### 7.17.3.1 通用

枚举类型`memory_order`指定了在 5.2.2.5 中定义的详细常规（非原子）内存同步操作，并提供操作排序。它的枚举常量如下：

```
memory_order_relaxed
memory_order_consume
memory_order_acquire
memory_order_release
memory_order_acq_rel
memory_order_seq_cst
```
