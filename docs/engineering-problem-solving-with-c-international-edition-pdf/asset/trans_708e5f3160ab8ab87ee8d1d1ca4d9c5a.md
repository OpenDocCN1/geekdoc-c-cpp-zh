

- 12. 从网络下载一张图像，并实现一个函数来执行你自己的创意修改。

- 13. 定义一个有理数类。有理数是由两个整数组成并指示除法的数，如 1/2、2/3、4/5。有理数使用两个整数对象定义：分子和分母。重载 << 和 >> 运算符以及算术运算符，以执行以下操作：

  a/b + c/d = (a*d + b*c) / (b*d)（加法）
  a/b - c/d = (a*d - b*c) / (b*d)（减法）
  (a/b) * (c/d) = (a*c)/(b*d)（乘法）
  (a/b) / (c/d) = (a*d) / (c*b)（除法）

- 14. 战争（WAR）游戏是一个两人简单的纸牌游戏。每位玩家获得一副52张的牌。每副牌都被洗牌并面朝下放在玩家面前。然后游戏以一系列回合进行。在每个回合中，两名玩家从自己的牌堆中抽出顶部的牌并面朝上放置。拥有最高等级牌的玩家赢得两张牌。如果两张牌等级相同，则发生战争。在战争的情况下，两名玩家各自从牌堆中抽出五张牌并面朝下放置。抽出第七张牌并翻面朝上。拥有最高等级牌的玩家赢得所有已出的牌。如果两张牌等级相同，则发生战争。传统游戏在一名玩家出完牌时结束，但你可以通过在所有52张牌各玩一次后结束游戏来简化游戏。最后拥有最多牌的玩家获胜。编写一个程序来模拟战争游戏，使用第8章开发的卡牌类。

- 15. 为高科技自动售货机编写一个模拟程序。在为机器建立初始状态后（即待售物品、它们的成本和初始库存数量），用户可以与模拟程序进行交互式对话。在此对话中，用户可以查看机器的当前状态、向机器存入金钱（美分）、购买机器中的物品、获得物品以及应找回的零钱，并执行硬币退回功能以取回所有存入的钱。为简单起见，假设自动售货机恰好有九种待售物品。物品可以使用三个对象定义：
  - 字符串，表示物品的名称
  - 物品的成本（美分）
  - 初始可供出售的物品数量

  以下数据可用于建立机器的初始状态：

| 物品 | 成本 | 数量 |
|------|------|------|
| Tortilla_Chips | 60 | 3 |
| Pretzels | 60 | 10 |
| Popcorn | 60 | 5 |
| Cheese_Crackers | 40 | 2 |
| Creme_Cookies | 65 | 1 |
| Mint_Gum | 25 | 5 |
| Chocolate_Bar | 55 | 3 |
| Licorice | 85 | 9 |
| Fruit_Chews | 55 | 7 |

  从概念上讲，物品可以组织为如下的3乘3矩阵：

```
A1 A2 A3
B1 B2 B3
C1 C2 C3
```

  定义两个类，一个物品类和一个机器类，以实现此模拟。

- 16. 修改程序 chapter10_9 以允许超过两名玩家进行 IPD 游戏。这可以被视为 IPD 锦标赛，其中每个玩家与其他每个玩家进行 IPD 游戏。在此情况下，你可能希望你的策略因对手而异。获胜者是在锦标赛中累积最多积分的玩家。

- 17. 修改 IPD 锦标赛程序以允许玩家在锦标赛中多次相遇。在此游戏中，你可以通过“记住”对手的策略来改进你的策略，以便下次相遇时使用。

- 18. 定义一个 Image 类。Image 具有一个二维像素数组以及支持图像平滑和亮度调整的成员函数。

## 附录 A C++ 标准库

本附录对 C++ 标准库中众多头文件中的几个头文件所定义的信息进行了简要讨论。这些简要讨论并非旨在提供使用函数所需的所有细节，而是提供足够的信息，以便你可以确定函数是否可能在特定应用中有用；然后你可以从网络上获取更多细节。一个良好的网络资源是 http://www.cplusplus.com/ref/。

### <cassert>

```
<cassert>
```

头文件 <cassert> 提供了 assert 函数的定义，可用于在测试程序时提供诊断信息。这种系统相关的诊断信息存储在标准错误文件中，可在程序完成后访问。

### <cctype>

```
<cctype>
```

头文件 <cctype> 定义了用于测试和转换字符的几个函数。函数原型语句和相应的讨论使用以下定义：

| 术语 | 定义 |
|---|---|
| 数字 | 字符 0123456789 之一 |
| 十六进制数字 | 一个数字或字符 ABCDEFabcdef 之一 |
| 大写字母 | 字符 ABCDEFGHIJKLMNOPQRSTUVWXYZ 之一 |
| 小写字母 | 字符 abcdefghijklmnopqrstuvwxyz 之一 |
| 字母字符 | 一个大写字母或一个小写字母 |
| 字母数字字符 | 一个数字或一个字母字符 |
| 标点字符 | 字符 " !#%&'()*+, -./:;<=>?@[\]^_{|}~ 之一 |
| 图形字符 | 一个字母数字字符或一个标点字符 |
| 可打印字符 | 一个图形字符或空格字符 |
| 运动控制字符 | 控制字符之一：换页（FF）、换行（NL）、回车（CR）、水平制表（HT）、垂直制表（VT） |
| 空白 | 空格字符或运动控制字符之一 |
| 控制字符 | 运动控制字符之一，或响铃（BEL）或退格（BS） |

我们现在列出每个函数原型，并为相应的函数给出简要定义：

```
int isalnum(int c);
returns a nonzero (true) value if and only if the input character is a digit or an uppercase or lowercase letter
```

```
int isalpha(int c);
returns a nonzero (true) value if and only if the input character is an uppercase or lowercase letter
```

- int iscntrl(int c);
  仅当输入字符是控制字符之一时，返回非零（真）值

- int isdigit(int c);
  仅当输入字符是数字时，返回非零（真）值

- int isgraph(int c);
  仅当输入字符是图形字符时，返回非零（真）值

- int islower(int c);
  仅当输入字符是小写字母时，返回非零（真）值

- int isprint(int c);
  仅当输入字符是可打印字符时，返回非零（真）值

- int ispunct(int c);
  仅当输入字符是标点字符时，返回非零（真）值

- int isspace(int c);
  仅当输入字符是空白字符时，返回非零（真）值

- int isupper(int c);
  仅当输入字符是大写字符时，返回非零（真）值

- int isxdigit(int c);
  仅当输入字符是十六进制字符时，返回非零（真）值

- int tolower(int c);
  将大写字母转换为小写字母

- int toupper(int c);
  将小写字母转换为大写字母

### <climits>

头文件 <climits> 提供了几个宏，用于给出整数值的各种限制和特性。这些宏及其定义如下：

- int CHAR_BIT;
  最小非位值的位数

- int CHAR_MIN;
  int CHAR_MAX;
  类型 char 的最小值和最大值

- int INT_MIN;
  int INT_MAX;
  类型 int 的最小值和最大值

- int LONG_MIN;
  int LONG_MAX;
  类型 long int 的最小值和最大值

- int MB_LEN_MAX;
  多字节字符中的最大字节数

- int SCHAR_MIN;
  int SCHAR_MAX;
  类型 signed char 的最小值和最大值

- int SHRT_MIN;
  int SHRT_MAX;
  类型 short int 的最小值和最大值

- int UCHAR_MAX;
  类型 unsigned char 的最大值

- int UINT_MAX;
  类型 unsigned int 的最大值

- int ULONG_MAX;
  类型 unsigned long int 的最大值

- int USHRT_MAX;
  类型 unsigned short int 的最大值

### <cmath>

头文件 <cmath> 定义了许多对科学编程有用的函数。

- double acos(double x);
  计算 x 的反余弦或逆余弦，其中 x 必须在范围 [-1, 1] 内；返回范围 [0, π] 内的弧度角

- double asin(double x);
  计算 x 的反正弦或逆正弦，其中 x 必须在范围 [-1, 1] 内；返回范围 [-π/2, π/2] 内的弧度角

- double atan(double x);
  计算 x 的反正切或逆正切；返回范围 [-π/2, π/2] 内的弧度角

- double atan2(double y, double x);
  计算 y/x 的反正切或逆正切，返回范围 [-π, π] 内的弧度角

- int ceil(double x);
  将 x 舍入到最接近的整数，方向趋向于 ∞（无穷大）

- double cos(double x);
  计算 x 的余弦，其中 x 以弧度为单位

- double cosh(double x);
  计算 x 的双曲余弦，等于 (e^x + e^-x)/2

- double exp(double x);
  计算 e^x 的值，其中 e 是自然对数的底数，约为 2.718282

- double fabs(double x);
  计算 x 的绝对值

- int floor(double x);
  将 x 舍入到最接近的整数，方向趋向于 -∞（负无穷大）

