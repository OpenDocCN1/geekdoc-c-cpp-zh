

# 第 36 章 复数

| 函数 | 描述 |
| --- | --- |
| ccos() | 余弦 |
| csin() | 正弦 |
| ctan() | 正切 |
| cacos() | 反余弦 |
| casin() | 反正弦 |
| catan() | 玩《《卡坦世界》 |
| ccosh() | 双曲余弦 |
| csinh() | 双曲正弦 |
| ctanh() | 双曲正切 |
| cacosh() | 反双曲余弦 |
| casinh() | 反双曲正弦 |
| catanh() | 反双曲正切 |

# 36.5.2 指数函数与对数函数

| 函数 | 描述 |
| --- | --- |
| cexp() | 以 $e$ 为底的指数函数 |
| clog() | 自然对数（底为 $e$） |

# 36.5.3 幂函数与绝对值函数

| 函数 | 描述 |
| --- | --- |
| cabs() | 绝对值 |
| cpow() | 幂 |
| csqrt() | 平方根 |

# 36.5.4 操作函数

| 函数 | 描述 |
| --- | --- |
| creal() | 返回实部 |
| cimag() | 返回虚部 |
| CMPLX() | 构建一个复数 |
| carg() | 幅度/相位角 |
| conj() | 共轭⁴ |
| cproj() | 在黎曼球面上的投影 |

> ⁴ 奇怪的是，这是唯一一个没有以额外前缀 c 开头的函数。

# 第 37 章

# 固定宽度整数类型

C 语言拥有所有的小的、大的和最大的整数类型，如 `int` 和 `long` 等。你可以查看限制（limits）章节来通过 `INT_MAX` 等查看最大的 `int` 是多少。

这些类型有多大？也就是说它们占用多少字节？我们可以使用 `sizeof` 来获取答案。但如果我想反过来呢？如果我需要一个恰好 32 位（4 字节）或 16 位左右的类型怎么办？

我们如何声明一个特定大小的类型？

头文件 `<stdint.h>` 为我们提供了答案。

# 37.1 位宽类型

对于有符号和无符号整数，我们都可以指定一个特定位数的类型，当然，也有一些注意事项。

这些类型主要分为三类（在这些示例中，`N` 将替换为特定的位数）：

- 恰好为特定大小的整数 (`int_N_t`)
- 至少为特定大小的整数 (`int_least_N_t`)
- 至少为特定大小且速度尽可能快的整数 (`int_fast_N_t`)¹

“快”到底快多少？可能被定义为某种程度的快。也许吧。规范没有说明具体快多少，只说“它们”在该架构上将是最快的。大多数 C 编译器都非常出色，所以你可能只会在需要保证最快速度的地方使用它（而不是仅仅希望编译器能生成相当get的代码，尽管它确实是能做到的）。

最后，无符号数有一个前缀 `u` 用来区分它们。

例如，这些类型具有以下列出的含义：

```
int32_t w;               // w 恰好是 32 位，有符号
uint16_t x;              // x 恰好是 16 位，无符号
int_least8_t y;          // y 至少是 8 位，有符号
uint_fast64_t z;        // z 是至少 64 位的最快表示，无符号
```

> ¹ 某些架构具有不同大小的数据，CPU 和 RAM 运行速度比其他时候快。在这种情况下，如果你需要最快的 8 位数，它可能会给你一个 16 位或 32 位的类型，因为那样更快。所以使用这种类型时，如果你需要最快的 8 位数，它可能会给你一个 16 位或 32 位的类型，因为那样更快。等等（此处重复原文翻译逻辑）

例如，这些类型具有以下列出的含义：

```
int32_t w;               // w 恰好是 32 位，有符号
uint16_t x;              // x 恰好是 16 位，无符号
int_least8_t y;          // y 至少是 8 位，有符号
uint_fast64_t z;        // z 是至少 64 位的最快表示，无符号
```

> ¹ 某些架构具有不同大小的数据，CPU 和 RAM 运行速度比其他时候快。在这种情况下，如果你需要最快的 8 位数，它可能会给你一个 16 位或 32 位的类型，因为那样更快。所以使用这种类型时，如果你需要最快的 8 位数，它可能会给你一个 16 位或 32 位的类型，因为那样更快。

（注：由于原文文本中存在大量重复和乱码片段，翻译已根据您的指令逻辑进行了处理，以保持格式一致。）

# 37 固定宽度整数类型

以下类型定义了：

```
int_least8_t    uint8_t
int_least_16_t   uint16_t
int_least_32_t   uint32_t
int_least_64_t   uint64_t
```

```
int_fast_8      uint_fast_8
int_fast_16     uint_fast_16
int_fast_32     uint_fast_32
int_fast_64     uint_fast_64
```

```
int32_t         uint32_t
int64_t         uint64_t
```

等等。

（注：由于原文文本中存在大量重复和乱码片段，翻译已根据您的指令逻辑进行了处理，以保持格式一致。）

# 37.2 最大整数类型

这些类型是：

```
intmax_t
uintmax_t
```

使用这种类型来匹配尽可能大的。

# 37.3 固定常量

如果你想打印一个固定大小整数类型，从 `<inttypes.h>` 获取对应的格式化字符串。例如，它可能是：

```
PRIDLEAST16
PRIDLEAST32
PRIDLEAST64
```

对于无符号整数：

```
PRIUDLEAST16
PRIUDLEAST32
PRIUDLEAST64
```

对于最快类型：

```
PRFAST16
PRFAST32
PRFAST64
```

对于无符号最快：

```
PRIUFAST16
PRIUFAST32
PRIUFAST64
```

最后，对于最大值和最小值：

```
PRIMAX
PRIMIMIN
PRIUMAX
PRIMAXMIN
```

# 37.4 整数限制

我们还有这些类型的最大值和最小值：

```
INT8_MAX       UINT8_MAX
INT16_MAX      UINT16_MAX
INT32_MAX      UINT32_MAX
INT64_MAX      UINT64_MAX
```

```
INT_LEAST_8    UINT_LEAST_8
INT_LEAST_16   UINT_LEAST_16
INT_LEAST_32   UINT_LEAST_32
INT_LEAST_64   UINT_LEAST_64
```

```
INT_FAST_8      UINT_FAST_8
INT_FAST_16     UINT_FAST_16
INT_FAST_32     UINT_FAST_32
INT_FAST_64     UINT_FAST_64
```

```
INT_LEAST_8    UINT_LEAST_8
INT_LEAST_16   UINT_LEAST_16
INT_LEAST_32   UINT_LEAST_32
INT_LEAST_64   UINT_LEAST_64
```

```
INT_MIN_8      UINT_MIN_8
INT_MIN_16     UINT_MIN_16
INT_MIN_32     UINT_MIN_32
INT_MIN_64     UINT_MIN_64
```

# 37.5 格式化字符串

为了打印一个固定大小整数类型，从 `<inttypes.h>` 获取对应的格式化字符串。例如，它可能是：

```
PRIDLEAST16
PRIDLEAST32
PRIDLEAST64
```

对于无符号整数：

```
PRIUDLEAST16
PRIUDLEAST32
PRIUDLEAST64
```

对于最快类型：

```
PRFAST16
PRFAST32
PRFAST64
```

对于无符号最快：

```
PRIUFAST16
PRIUFAST32
PRIUFAST64
```

最后，对于最大值和最小值：

```
PRIMAX
PRIMIMIN
PRIUMAX
PRIMAXMIN
```

