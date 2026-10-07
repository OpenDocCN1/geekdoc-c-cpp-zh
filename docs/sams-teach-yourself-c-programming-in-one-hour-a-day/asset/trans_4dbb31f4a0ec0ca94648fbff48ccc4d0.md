

# ASCII 图表 58

| 十进制 | 十六进制 | ASCII | 十进制 | 十六进制 | ASCII |
|---|---|---|---|---|---|
| 201 | C9 | ÿ | 232 | E8 | Φ |
| 202 | CA |  잔 | 233 | E9 | θ |
| 203 | CB | ¶ | 234 | EA | Ω |
| 204 | CC | Ç | 235 | EB | δ |
| 205 | CD | = | 236 | EC | ∞ |
| 206 | CE | ╣ | 237 | ED | ø |
| 207 | CF | � | 238 | EE | µ |
| 208 | D0 | � | 239 | EF | ∪ |
| 209 | D1 | � | 240 | F0 | Ä |
| 210 | D2 | ═ | 241 | F1 | ± |
| 211 | D3 | ╝ | 242 | F2 | ≥ |
| 212 | D4 | ╚ | 243 | F3 | ≤ |
| 213 | D5 | ¶ | 244 | F4 | | |
| 214 | D6 | ═ | 245 | F5 | J |
| 215 | D7 | ¶ | 246 | F6 | ÷ |
| 216 | D8 | # | 247 | F7 | = |
| 217 | D9 |   | 248 | F8 | ° |
| 218 | DA |   | 249 | F9 | • |
| 219 | DB |   | 250 | FA | . |
| 220 | DC | ■ | 251 | FB | √ |
| 221 | DD |   | 252 | FC | n |
| 222 | DE |   | 253 | FD | 2 |
| 223 | DF | ■ | 254 | FE | ■ |
| 224 | E0 | α | 255 | FF | | |
| 225 | E1 | β | | | | |
| 226 | E2 | Γ | | | | |
| 227 | E3 | π | | | | |
| 228 | E4 | Σ | | | | |
| 229 | E5 | σ | | | | |
| 230 | E6 | μ | | | | |
| 231 | E7 | γ | | | | |

本页特留。

# 附录 B
C/C++ 保留字

表 B.1 中列出的标识符是 C 的保留关键字。你不应该在 C 程序中将它们用于任何用途。当然，它们在双引号内是被允许的。

还包含了一列表在 C 中未保留但在 C++ 中是保留关键字的单词。这里没有描述这些单词，但如果你的 C 程序最终可能会迁移到 C++，你也需要避免这些单词。

| 关键字 | 说明 |
| --- | --- |
| asm | 表示内联汇编代码的关键字。 |
| auto | 默认存储类。意味着在进入块时创建变量，在离开块时销毁它。 |
| break | 无条件退出 for、while、switch 和 do...while 语句的命令。 |
| case | 在 switch 语句内部使用的命令。 |
| char | 最简单的 C 数据类型。 |
| const | 防止变量被更改的数据修饰符。参见 volatile。 |
| continue | 将 for、while 或 do...while 语句重置为下一次迭代的命令。 |
| default | 在 switch 语句内部用于捕获任何未用 case 语句指定的实例。 |
| do | 与 while 语句配合使用的循环命令。循环将至少执行一次。 |
| double | 可以存储双精度浮点数的数据类型。 |
| else | 当 if 语句评估为假时指示执行备选语句的语句。 |

# 附录 B

| 关键字 | 说明 |
| --- | --- |
| enum | 允许声明仅接受特定值的数据类型。 |
| extern | 指示变量将在程序其他区域声明的数据修饰符。 |
| float | 用于浮点数的数据类型。 |
| for | 包含初始化、递增和条件部分的循环命令。 |
| goto | 导致跳转到预定义标签的命令。 |
| if | 根据真/假决策用于更改程序流的命令。 |
| inline | 用于将函数声明为内联。内联函数可以复制到列表中，而不是像普通函数那样调用。 |
| int | 用于整数值的数据类型。 |
| long | 用于比 int 更大整数的数据类型。 |
| register | 指定应尽可能将变量存储在寄存器中的存储修饰符。 |
| restrict | 与指针使用的访问修饰符。 |
| return | 导致程序流退出当前函数并返回到调用函数的命令。它也可以用于返回单个值。 |
| short | 用于较小整数的数据类型。 |
| signed | 指示值可以是正也可以是负的修饰符。 |
| sizeof | 返回对象按字节计算的大小的运算符。 |
| static | 指示变量或函数生命周期或作用域的修饰符。 |
| struct | 用于将相关变量组合在一起的数据类型。 |
| switch | 用于根据多个 case 控制流的命令。 |
| typedef | 用于创建数据类型别名的的关键字。 |
| union | 允许不同类型共享相同内存位置的数据类型。 |
| unsigned | 指示值仅为正数的修饰符。 |
| void | 用于无返回值的数据类型。 |
| volatile | 指示变量可以被外部因素更改的修饰符。 |

| 关键字 | 说明 |
| --- | --- |
| _Bool | 表示布尔值的数据类型。 |
| while | 只要条件为真就执行的循环命令。 |
| _Complex | 用于复数的数据类型。 |
| _Imaginary | 用于虚数的数据类型。 |
| catch | 用于异常处理的关键字。 |
| delete | 用于 C++ 中释放内存的运算符。 |
| finally | 用于异常处理以确保代码运行的关键字。 |
| friend | 用于访问成员的关键字。 |
| private | C++ 私有访问修饰符。 |
| public | C++ 公有访问修饰符。 |
| try | 用于异常处理的关键字。 |
| throw | 用于抛出异常的关键字。 |
| virtual | C++ 虚函数关键字。 |

# 附录 C

| 函数 | 头文件 | 原型 |
|---|---|---|
| abort | stdlib.h | void; |
| abs | stdlib.h | int; |
| acos | math.h | double; |
| actime | time.h | char *; |
| asin | math.h | double; |
| assert | assert.h | void; |
| atan | math.h | double; |
| atan2 | math.h | double; |
| atext | stdlib.h | void; |
| atof | stdlib.h | double; |
| atof | math.h | double; |

| 函数 | 头文件 | 原型 |
| --- |---|---|
| atoi | stdlib.h | int; |
| bsearch | stdlib.h | void *, const void *, size_t, int (*); |
| calloc | stdlib.h | void *; |
| ceil | math.h | double; |
| clearerr | stdio.h | void; |
| clock | time.h | clock_t; |
| cos | math.h | double; |
| cosh | math.h | double; |
| ctime | time.h | char *; |
| difftime | time.h | double; |
| div | stdlib.h | int; |
| exit | stdlib.h | void; |
| exp | math.h | double; |
| fabs | math.h | double; |
| fclose | stdio.h | int; |
| fcloseall | stdio.h | int; |
| feof | stdio.h | int; |
| fflush | stdio.h | int; |
| fgetc | stdio.h | int; |
| getpos | stdio.h | int *; |
| fgets | stdio.h | char *; |
| floor | math.h | double; |
| flushall | stdio.h | int; |
| fmod | math.h | double; |
| fopen | stdio.h | FILE *; |
| fprintf | stdio.h | int; |
| fputc | stdio.h | int; |
| fputs | stdio.h | int; |
| fread | stdio.h | size_t; |
| free | stdlib.h | void; |
| freopen | stdio.h | FILE *; |
| frexp | math.h | double; |
| sscanf | stdio.h | int; |

