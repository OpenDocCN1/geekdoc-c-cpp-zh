
不被搜索。再次，通过 Xcode，你可以指定要搜索的目录。

导入文件功能最棒的特性之一是它允许你对定义进行集中管理，从而使得所有程序都引用同一个值。此外，在包含文件中包含的某个值中发现的错误只需要在一处进行修正，从而避免了修正每个使用该值的程序。任何引用了错误值的程序只需要重新编译，而无需进行编辑。

# Conditional-C 编译

Objective-C 预处理器提供了一种名为“条件编译”的功能。条件编译通常用于创建一个可以编译并运行在不同计算机系统上的程序。它还经常被用于在程序中开启或关闭各种语句，例如打印变量值的调试语句或跟踪程序执行流的语句。

## #ifdef, #endif, #else, 和 #ifndef 语句

不幸的是，不幸的是，程序有时必须依赖于系统相关的参数，这些参数在不同设备（例如，iPhone 与 iPad）上或特定的操作系统版本（例如，Leopard 与 Snow Leopard）上需要不同的指定方式。

如果你有一个对计算机系统特定硬件和软件有许多依赖的大型程序（你应该尽可能地减少这种依赖），你可能会发现许多值必须更改才能在另一个环境中运行。

你可以利用预处理器的条件编译能力来帮助减少更改这些值的问题，并将每种不同机器的这些定义值纳入程序中。作为一个简单的例子，以下语句的作用是：如果符号 IPAD 已经被定义，则将 kImageFile 定义为 "@barnHD.png"，否则定义为 "@barn.png"：

```
#ifdef IPAD
# define kImageFile @"barnHD.png"
#else
# define kImageFile @"barn.png"
#endif
```

如你所示，你可以在起始预处理器语句的 # 之后放置一个或多个空格。

#ifdef、#else 和 #endif 语句的行为正如你所预期。如果 #ifdef 行上指定的符号已经定义（通过 #define 语句或在编译程序时通过命令行），编译器将处理后续 #else、#elif 或 #endif 之前的行；否则，这些行将被忽略。

若要向预处理器定义符号 IPAD，可以使用以下语句：

```
#define IPAD 1
```

甚至仅仅是：

```
#define IPAD
```

如你所见，为了满足 #ifdef 测试，定义名称后不需要出现任何文本。编译器还允许你在编译程序时，通过编译器命令的特殊选项为预处理器定义一个名称。命令行：

```
gcc -framework Foundation -D IPAD program.m
```

这会将名称 IPAD 定义给预处理器，导致 program.m 内部所有的 #ifdef IPAD 语句评估为 TRUE（注意，你必须在命令行的程序名称之前输入 -D IPAD）。这种技术允许你在无须编辑源程序的情况下定义名称。

在 Xcode 中，你通过选择 Build Settings, All, Apple LLVM compiler 3.0 - Preprocessing, Preprocessor Macros 来添加新的定义名称并指定它们的编译器值。你可以在图 12.1 中看到 Xcode 4 中符号 IPAD 和 DEBUG（定义为 1）的。

# 图 12.1. 定义预处理器标识符 IPAD

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_384_0.png)

#ifndef 语句的原理与 #ifdef 类似。该语句的使用方式相似，不同之处在于指定的符号未定义，则会处理后续行。

正如前面提到的，条件编译在调试程序时非常有用。你的程序中可能嵌入了许多 NSLog 调用，用于显示中间结果和跟踪执行流。如果某个特定名称（如 DEBUG）被定义，你可以通过条件编译将其编译进程序来开启这些语句。例如，你可以使用如下语句序列，仅当程序在定义 DEBUG 的情况下编译时才显示某些变量的值：

```
#ifdef DEBUG
NSLog ("User name = %s, id = %i", userName,
userId());
#endif
```

程序中可能有很多这样的调试语句。每当对程序进行调试时，可以在定义 DEBUG 的情况下进行编译，以编译所有的调试语句。当程序正常运行时，可以在不定义 DEBUG 的情况下重新编译。这额外的好处是减小程序的大小，因为所有的调试语句都没有被编译进去。

# #if 和 #elif 预处理器语句

#if 预处理器语句提供了一种通用的方法来控制条件编译。#if 语句可以用于测试常量表达式的值是否为非零。如果表达式的结果非零，则处理后续 #else、#elif 或 #endif 之前的行；否则，跳过这些行。

作为如何使用此方法的示例，以下行出现在 Foundation 头文件 NSString.h 中：

```
#if MAC_OS_X_VERSION_MIN_REQUIRED < nMAC_OS_X_VERSION_10_5
#define NSMaximumStringLength (INT_MAX-1)
#endif
```

这测试了定义变量 MAC_OS_X_VERSION_MIN_REQUIRED 的值是否小于 MAC_OS_X_VERSION_10_5。如果前者小于后者，则将字符串的最大长度设置为整数减 1。

特殊的运算符 defined (name) 也可以用于 #if 语句。

```
#if defined(name)
...
#endif
```

以下语句出现在untime.h 中，用于根据特定的编译器定义 NS_INLINE（如果尚未定义）：

```
#if !defined(NS_INLINE)
#if defined(__GNUC__)
#define NS_INLINE static __attribute__((always_inline))
#elif defined(__MWKS__) || defined(__cplusplus)
#define NS_INLINE static inline
#elif defined(__MSC_VER__)
#define NS_INLINE static inline
#endif
```

#if 的另一种常见用法如下序列：

```
#if defined (DEBUG) && DEBUG
...
#endif
```

如果 DEBUG 已定义且值为非零。由于可以使用表达式且 0 始终为假，程序员（包括我）经常通过将代码块封装在 #if 0 ... #endif 中来注释掉代码。

# #undef 

有时你需要让已定义的名称变为未定义。可以通过 #undef 语句来实现。要移除特定名称的定义，写入：

```
#undef name
```

因此，该语句删除了 IPAD 的定义：

```
#undef IPAD
```

随后的 #ifdef IPAD 或 #if defined (IPAD) 将评估为 FALSE。

预处理器讨论结束。

# 练习

- 在你的机器上找到系统头文件 limits.h 和 float.h。检查这些文件查看内容。如果这些文件包含了其他头文件，请务必也追踪并检查它们的内容。
- 定义一个名为 MIN 的宏，获取两个值的最小值。编写一个程序来测试该宏定义。
- 定义一个名为 MAX3 的宏，获取三个值的最大值。编写一个程序来测试该定义。
- 编写一个名为 IS_UPPER_CASE 的宏，如果字符是大写字母则返回非零值。
- 编写一个名为 IS_ALPHABETIC 的宏，如果字符是字母则返回非零值。让该宏使用正文中定义的 IS_LOWER_CASE 宏和练习 4 中定义的 IS_UPPER_CASE 宏。
- 编写一个名为 IS_DIGIT 的宏，如果字符是数字 0 到 9 则返回非零值。使用此宏来定义另一个名为 IS_SPECIAL 的宏，该宏在字符是特殊字符（即既不是字母也不是数字）时给出一个非零结果。请务必使用练习 5 中开发的 IS_ALPHABETIC 宏。
- 编写一个名为 ABSOLUTE_VALUE 的宏，计算其参数的绝对值。确保该宏能够正确处理如下表达式：

