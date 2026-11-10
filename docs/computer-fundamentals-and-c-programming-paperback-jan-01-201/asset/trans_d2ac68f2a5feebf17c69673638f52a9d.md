
- `int`
- `short` 或 `short int`（`short` 是 `int` 的限定符）
- `long` 或 `long int`（`long` 是 `int` 的限定符）
- `long long` 或 `long long int`（`long long` 是 `int` 的限定符）

```c
/* sizeof.c: Displays the size of the fundamental data types
               using the sizeof operator. */
#include <stdio.h>

int main(void)
{
    printf("Size of char: %d byte\n", sizeof(char));
    printf("Size of short: %d bytes\n", sizeof(short));
    printf("Size of int: %d bytes\n", sizeof(int));
    printf("Size of long: %d bytes\n", sizeof(long));
    printf("Size of float: %d bytes\n", sizeof(float));
    printf("Size of double: %d bytes\n", sizeof(double));
    printf("Size of long double: %d bytes\n", sizeof(long double));

    /* Now use sizeof on 2 constants -- parentheses optional here */
    printf("Size of 34: %d bytes\n", sizeof 34);
    printf("Size of 3.142: %d bytes\n", sizeof(3.142));

    /* Uncomment the following line to see if long long is supported
       by your compiler. It may lead to a compiler error. */

    /* printf("Size of long long: %d bytes\n", sizeof(long long)); */

    return 0;
}
```

程序 5.2：**sizeof.c**

| *Linux (GCC)* | *Windows (Visual Studio)* |
|---|---|
| Size of char: 1 byte<br>Size of short: 2 bytes<br>Size of int: 4 bytes<br>Size of long: 4 bytes<br>Size of float: 4 bytes<br>Size of double: 8 bytes<br>Size of long double: 12 bytes<br>Size of 34: 4 bytes<br>Size of 3.142: 8 bytes<br>Size of long long: 8 bytes | Size of char: 1 byte<br>Size of short: 2 bytes<br>Size of int: 4 bytes<br>Size of long: 4 bytes<br>Size of float: 4 bytes<br>Size of double: 8 bytes<br>Size of long double: 8 bytes<br>Size of 34: 4 bytes<br>Size of 3.142: 8 bytes<br>*Visual Studio 2013 之前不支持 long long* |

程序输出：**sizeof.c**（Linux 和 Windows）

下面是我们如何声明两个类型分别为 int 和 long 的变量：

```c
int simply_int;
long simply_long = 50000;
```

列表中的最后一种类型（long long）在许多编译器中早已可用，之后才被纳入 C99。然而，Visual Studio 仅从 2013 版本开始支持它。在接下来的几节中，我们将考察这些类型，了解它们的最小大小以及这些大小之间的关系。

> 注意：-7 中的 - 是一个运算符；它将 7 乘以 -1。

### 5.6.1 ANSI 对整数的规定

ANSI 标准是在 C 应用程序已经进入商业世界之后才形成的。为了创建一个也能保护这些应用程序的标准，ANSI 有意将这些数据类型的大小规定得较为模糊。不过，它明确了两条规则：

- 各类型的最小大小：
  - short — 2 字节（16 位）
  - int — 2 字节（16 位）（现代 int 为 4 字节）
  - long — 4 字节（32 位）
  - long long — 8 字节（64 位）
- 这些类型之间存在可用以下形式表示的关系：
  - char <= short <= int <= long <= long long

第一条规则解释了为什么我们在讨论变量的内存分配时使用“至少”一词。第二条规则意味着 short 不能小于 char，int 不能小于 short，依此类推。这两条规则使得 int 和 long 在一台机器上可以具有相同大小，而 short 和 int 在另一台机器上可以具有相同大小。我们在这里纳入 char 数据类型，因为 char 本质上是一种整数类型，尽管它几乎只用于表示字符。

> 要点：你无法确保任何类型都具有固定大小，但 ANSI 保证了最小大小。它还规定了这些大小之间的关系。

### 5.6.2 有符号和无符号整数

默认情况下，四种 int 类型都是有符号的，这意味着它们可以处理正整数和负整数。可以通过在关键字前使用 unsigned 限定符来覆盖此默认行为。例如，以下语句

```c
unsigned int count;
```

允许 count 只存储正整数。由于有符号数据类型使用一位来存储符号，有符号类型范围的正值侧是其无符号类型的一半（3.3）。例如，unsigned short 使用的两个字节可以表示 0 到 $2^{16}-1$ 之间的值，即 65,535。对于 signed short，这个范围变为 -32,768 到 32,767（$-2^{15}$ 到 $2^{15}-1$）。

表 5.1 显示了这些整数的基本属性、它们的无符号最大值以及 `printf` 和 `scanf` 用于处理它们的格式说明符。注意，无符号格式说明符将 d 替换为 u。因此，`%ld` 变成 `%lu`，`%d` 变成 `%u`，依此类推。

**表 5.1** 整数的属性

| 子类型 | ANSI 规定的最小大小 | 无符号最大值 | `printf`/`scanf` 格式说明符（有符号/无符号） |
|---|---:|---:|---|
| short | 2 | 65,535 | `%hd` / `%hu` |
| int | 2 | 65,535 | `%d` / `%u` |
| long | 4 | 4,294,967,295（40 亿） | `%ld` / `%lu` |
| long long | 8 | 18,446,744,073,709,551,615 | `%lld` / `%llu` |

### 5.6.3 具体的整数类型

**short 类型** 该类型缩写自 `short int`，其最小大小和典型大小均为 2 字节。对于它所提供的范围（-32,768 到 32,767），`short` 适用于年龄、分数和家庭人数等非负整数实体。如果需要大于 32,767 但小于 65,535 的整数，请使用 `unsigned short`。

**int 类型** 这是标准整数类型，反映机器的字长。与 `short` 一样，其最小大小为 2 字节，但由于当今大多数计算机是 32 位机器，`int` 也是 32 位（4 字节）。有符号 `int` 可以处理最高 20 亿的数字（正负两侧均如此），而无符号类型可以保存最高 40 亿的数字。常用且经常被误用的 `%d` 格式说明符实际上适用于 `int`。

**long 类型** long 类型（缩写自 `long int`）用于保存比 `int` 更大的数字。然而，在 32 位系统上并非总是如此。在大多数情况下，`int` 和 `long` 大小相同——4 字节，但在某些系统上可能看到 8 字节的 long。此外，大多数 64 位编程模型使用 8 字节长整数。8 字节长整数可以处理百亿亿量级的值。

**long long 类型** C99 将此类型加入语言，以容纳 64 位整数。在大多数支持此类型的系统上，`long long` 为 8 字节。由于大多数 64 位模型中的 `long` 已设为 8 字节，现在断言 `long long` 的最终大小还为时过早。

> **注意：** 有符号整数数据类型的基本格式说明符是 `%d`。对于 `short`（`h`）、`long`（`l`）和 `long long`（`ll`），需要修饰符。对于无符号类型，将 `%d` 替换为 `%u`，并按需使用相同的修饰符。`printf` 和 `scanf` 使用的这些说明符的完整列表见第 9 章。

### 5.6.4 八进制和十六进制整数

除了十进制整数（基数为 10）外，C 还支持八进制（基数为 8）和十六进制（基数为 16）数。C 通过特殊前缀来识别它们：

- 当数字 0（零）作为由数字 0 到 7 组成的数的前缀时，C 将该数解释为八进制。因此，`072` 是一个八进制整数，其值为 (58)10（7 × 8¹ + 2 × 8⁰ = 58）。`printf/scanf` 组合使用 `%o` 处理八进制整数。
- 当由数字 0 到 9 以及 A 到 F 组成的数前面带有 0x 或 0X 时，C 将该数解释为十六进制。因此，C 将 0x72 理解为基数为 16 的数，其值为 (114)10（7 × 16¹ + 2 × 16⁰）。使用 `%x` 或 `%X` 格式说明符处理十六进制整数。

系统程序员需要熟悉这些数制，因为许多程序会以这些形式输出数字。

## 5.7 all_about_int.c：理解整数

程序 5.3 部分总结了我们对四种整数数据类型的认识。它演示了 `printf` 如何在不同的数制之间转换数据。该程序还展示了数据溢出的后果，以及使用错误格式说明符如何影响转换。

其中两个变量是有符号的，一个是无符号的。由于 `short x` 是有符号的，它使用 15 位，因此 32767 是它能保存的最大值。八进制表示证实了这一点：最大的八进制数字（7）占据了全部五个位置。前三个 `printf` 语句使用了正确的格式说明符。

接下来，我们通过给 `short_x` 加 1 来制造溢出情况。有符号 short 的范围是 -32,768 到 32,767。相加得到的数字 32768 比最大正值大 1。这会导致溢出，将符号位置为 1，其余位设为 0。所得数字 (1000 0000 0000 0000)₂ 表示有符号 short 的最小值（-32768）。

> **工作原理：选择哪种整数类型？**
> 
> ANSI 的规定导致类型大小存在重叠。有些机器上 `short` 和 `int` 的大小相同，或者 `int` 和 `long` 的大小相同。那么，如何确定用于整数的正确类型呢？如果你的应用程序需要可移植，以下准则应有所帮助：
> 
> *如果你需要 2 字节，而你的机器上 `short` 和 `int` 都是这个大小，那么使用 `short`。当程序移到 `int` 扩展为 4 字节的 32 位机器上时，你的程序不会浪费内存。然而，如果你需要 4 字节，而 `int` 和 `long` 都是这个大小，那么使用 `long`，因为当应用程序移到更小的机器上时，`int` 可能缩减为 2 字节。*
> 
> 上述经验法则可以保护你的应用程序，但不能保证防止浪费。如果你因为能保证得到 4 字节而使用 `long`，那么在 64 位机器上就要准备好得到 8 字节。
