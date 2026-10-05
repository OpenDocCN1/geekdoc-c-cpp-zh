

# 926 附录 4 某些库函数

## 赋值/修改符

| 操作 | 描述 |
| :--- | :--- |
| string_Object1 = string_Object2; | 分配空间并初始化为 string_Object2 的数据，释放为 string_Object1 分配的内存，将 string_Object1 的大小设置为 string_Object2 的大小。 |
| string_Object1 += string_Object2; | 将 string_Object2 的字符数据拼接到 string_Object1 的末尾；适当设置大小。 |
| string_Object.empty() | 如果 string_Object 是空字符串则返回 true；否则返回 false。 |
| string_Object1 + string_Object2 | 返回一个字符串，其 string_Object2 的数据拼接在 string_Object1 数据的末尾。适当设置大小。 |
| string_Object1.insert(Position, string_Object2); | 从 Position 开始将 string_Object2 插入 string_Object1 中。 |
| string_Object1.remove(Position, Length); | 从 Position 开始删除长度为 Length 的子字符串。 |

## 比较

| 比较 | 描述 |
| :--- | :--- |
| string_Object1 == string_Object2<br>string_Object1 != string_Object2 | 比较相等或不相等；返回一个布尔值。 |
| string_Object1 < string_Object2<br>string_Object1 > string_Object2<br>string_Object1 <= string_Object2<br>string_Object1 >= string_Object2 | 字典序比较。 |

## 查找

| 方法 | 描述 |
| :--- | :--- |
| string_Object1.find(string_Object2) | 返回 string_Object2 在 string_Object1 中首次出现的索引。 |
| string_Object1.find(string_Object2, Position) | 返回 string_Object2 在 string_Object1 中首次出现的索引；搜索从 Position 开始。 |
| string_Object1.find_first(string_Object2, Position) | 返回 string_Object1 中 string_Object2 任意任意字符的首次出现索引，从 Position 开始搜索。 |
| string_Object1.find_first_not_of(string_Object2, Position) | 返回 string_Object1 中不在 string_Object2 中的任意字符的首次出现索引，从 Position 开始搜索。 |

*某些实现将其放在 cmath 中。*

# 某些库函数 附录 4 927

## 随机数生成器

| 函数声明 | 描述 | 头文件 |
| :--- | :--- | :--- |
| int random(int); | 调用 random(n) 返回一个大于或等于 0 且小于或等于 n - 1 的伪随机整数。（并非所有实现都可用。如果不可，则必须使用 rand。） | cstdlib |
| int rand(); | 调用 rand() 返回一个大于或等于 0 且小于或等于 RAND_MAX 的伪随机整数。RAND_MAX 是在 cstdlib 中定义的预定义整数常量。RAND_MAX 的值取决于实现，但至少为 32767。 | cstdlib |
| void srand(unsigned int); | 重新初始化随机数生成器。参数是种子。多次使用相同参数调用 srand 会导致 rand 或 random（取决于使用哪一个）产生相同的伪随机数序列。如果在没有之前调用过 srand 的情况下调用 rand 或 random，则产生的数字序列与调用参数为 1 的 srand 相同。 | cstdlib |

## 三角函数

这些函数使用弧度，而不是度数。

| 函数声明 | 描述 | 头文件 |
| :--- | :--- | :--- |
| double acos(double); | 反余弦 | cmath |
| double asin(double); | 反正弦 | cmath |
| double atan(double); | 反正切 | cmath |
| double cos(double); | 余弦 | cmath |
| double cosh(double); | 双曲余弦 | cmath |
| double sin(double); | 正弦 | cmath |
| double sinh(double); | 双曲正弦 | cmath |
| double tan(double); | 正切 | cmath |
| double tanh(double); | 双曲正切 | cmath |

# 新旧头文件 5

在书中，我们使用了属于新 ANSI/ISO C++ 标准部分的标准库头文件。如果您使用较旧的编译器，可能需要使用旧的头文件。在接下来，我们列出了书中使用的新头文件名称及其旧头文件名称。如果您的编译器需要旧头文件名称且不支持命名空间，您应该考虑获取一个更接近标准的编译器。

| 新头文件 | 对应的旧文件 |
| :--- | :--- |
| c-assert | assert.h |
| cctype | ctype.h |
| cstddef | stddef.h |
| cstdlib | stdlib.h |
| cmath | math.h |
| cstring | string.h |
| fstream | fstream.h |
| iomanip | iomanip.h |
| iostream | iostream.h |
| string | 无库 |

# 索引 # 符号

- !, 47
- !=, 404, 793, 859
- %, 21
- &, 149, 155, 424
- &&, 46–47, 336
- *, 参见解引用 (*), 36
- *=, 14
- ', 17
- (), 20, 28, 47, 50, 58
- ;, 77, 242, 246
- /, 21, 22, 164–165
- //, 36
- /, 17
- \, 17, 18
- ', 18
- ?, 18
- 0, 369, 370, 371–372
- a, 18
- \b, 18
- \f, 18
- \n, 6, 18, 29–30, 382, 383, 386–387
- \r, 18
- \t, 18
- \v, 18, 243–244, 255, 257, 734–735
- +, 323, 395
- ++, 参见递增 (++)
- +=, 14
- --, 323
- --, 参见递减 (--)
- [], 187, 197, 308, 883
- ~, 7
- [], 58, 242, 488
- ||, 48, 336
- ~, 459, 460
- <, 48, 404
- <<, 28
- overloading, 346–352, 354, 519
- <=, 46
- = 参见赋值 (=)
- -=, 14
- ==, 59, 323, 793, 859
- with C-strings
- class, 404
- >, 48, 404
- ->, 448, 735
- >=, 46
- >>, 376, 399
- :, 255, 256, 519, 492, 500

# A

- abs, 102, 103
- , 102, 103
- 绝对值函数, 102, 103
- 抽象类, 264, 265
- 算法, 700
- 抽象数据类型 (ADTs), 258, 264

# 抽象
- 算法, 700
- 数据, 258
- 过程, 127

# 访问
- 容器, 894
- 对象的, 335
- 私有成员, 650
- 随机的, 865–867
- 文件的, 555–557
- 访问器, 262–263
- 激活帧, 583

# 地址. 参见指针
- 字节, 190
- 指针, 420–444
- 变量, 151, 190–191
- 地址符 (&) 运算符, 422, 424

# 算法
- 算法, 700
- 二分查找, 595
- 通用, 889
- 链式查找, 748
- 修改序列, 999
- 选择, 713

# 数组
- 参数, 196
- 数组, 101
- 基本类型, 187
- 比较, 712
- 声明, 186
- 声明的, 108
- 动态, 参见数组
- 元素, 187
- 作为函数参数, 196
- 构造函数, 461
- 拷贝构造函数, 463
- 派生类, 636–637
- 在动态数据结构中的, 747
- 事实上的, 195–207
- 返回函数的, 202
- 索引越界, 192
- 索引, 189
- 初始化, 192–193
- 引言, 186
- 使用 for 循环, 189
- 在内存中的, 190–198
- 多维, 218–225, 444–447
- 部分填充的, 207–210, 456–458, 638–640, 719–723
- 生产图示例, 202–206
- 使用程序的, 188
- 编程使用, 207
- 引用, 186–190
- 搜索, 211–213, 595
- 大小, 187, 189
- 排序, 213–217
- 类似于字符串对象, 401–402
- 变量, 437–438

