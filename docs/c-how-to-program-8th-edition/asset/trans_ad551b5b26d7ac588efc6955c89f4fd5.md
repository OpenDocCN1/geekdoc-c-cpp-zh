
## 代码评审规范

本规范适用于所有项目的代码评审流程，旨在提高代码质量、统一评审标准、促进团队协作。

- 评审范围
- 评审流程
- 评审标准

| 等级 | 说明 |
| --- | --- |
| P0 | 必须修复 |
| P1 | 建议修复 |
| P2 | 可选建议 |

> 评审不是为了挑错，而是为了共同进步。

评审完成后，需要在系统中填写评审记录，并跟踪问题修复情况。

![](img/bfd978e7e9b192bab46ec2a89e481263_350_0.png)

## 7.3

```cpp
a) const int arraySize = 10;
b) double fractions[ arraySize ] = { 0.0 };
c) fractions[ 3 ]
d) fractions[ 4 ]
e) fractions[ 9 ] = 1.667;
f) fractions[ 6 ] = 3.333;
g) cout << fixed << setprecision( 2 );
   cout << fractions[ 6 ] << ' ' << fractions[ 9 ] << endl;
   Output: 3.33 1.67.

h) for ( int i = 0; i < arraySize; ++i )
       cout << "fractions[" << i << "] = " << fractions[ i ] << endl;
   Output:
   fractions[ 0 ] = 0.0
   fractions[ 1 ] = 0.0
   fractions[ 2 ] = 0.0
   fractions[ 3 ] = 0.0
   fractions[ 4 ] = 0.0
   fractions[ 5 ] = 0.0
   fractions[ 6 ] = 3.333
   fractions[ 7 ] = 0.0
   fractions[ 8 ] = 0.0
   fractions[ 9 ] = 1.667
```

## 7.4

```cpp
a) int table[ arraySize ][ arraySize ];
b) Nine.
c) for ( i = 0; i < arraySize; ++i )
       for ( j = 0; j < arraySize; ++j )
           table[ i ][ j ] = i + j;
d) cout << "     [0] [1] [2]" << endl;

   for ( int i = 0; i < arraySize; ++i ) {
       cout << '[' << i << "] ";

       for ( int j = 0; j < arraySize; ++j )
           cout << setw( 3 ) << table[ i ][ j ] << " ";
       cout << endl;
   }

   Output:
       [0]  [1]  [2]
   [0]   1    8    0
   [1]   2    4    6
   [2]   5    0    0
```

## 7.5

- a) *错误：* `#include` 预处理指令末尾有分号。  
  *更正：* 删除分号。

- b) *错误：* 使用赋值语句给常量变量赋值。  
  *更正：* 在 `const int arraySize` 声明中初始化该常量变量。

- c) *错误：* 引用数组边界之外的数组元素（b[10]）。  
  *更正：* 将控制变量的最终值改为 9，或将 `<=` 改为 `<`。

- d) *错误：* 数组下标使用不正确。  
  *更正：* 将该语句改为 `a[ 1 ][ 1 ] = 5;`

```cpp
for ( row = 0; row < 3; ++row )
   for ( column = 0; column < 5; ++column )
      sales[ row ][ column ] = 0;
```

## **7.17** (*掷骰子*)

编写一个模拟掷两个骰子的程序。程序应使用 `rand` 掷第一个骰子，并再次使用 `rand` 掷第二个骰子。然后应计算两个值之和。[*注：* 每个骰子可以显示 1 到 6 的整数值，因此两个值之和将在 2 到 12 之间变化，其中 7 是最常见的和，2 和 12 是最不常见的和。] 图 7.26 显示了两个骰子的 36 种可能组合。你的程序应掷两个骰子 36,000 次。使用一维数组统计每个可能和出现的次数。以表格格式打印结果。同时，判断总计是否合理（即，掷出 7 有六种方式，因此所有投掷中大约六分之一应为 7）。

![](img/bfd978e7e9b192bab46ec2a89e481263_354_0.png)

**图 7.26**  掷两个骰子的 36 种可能结果。

## **7.18** (*这段代码做什么？*) 下面的程序做什么？

```cpp
// Ex. 7.18: Ex07_18.cpp
// What does this program do?
#include <iostream>
using namespace std;

int whatIsThis( int [], int ); // function prototype

int main()
{
   const int arraySize = 10;
   int a[ arraySize ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

   int result = whatIsThis( a, arraySize );

   cout << "Result is " << result << endl;
} // end main

// What does this function do?
int whatIsThis( int b[], int size )
{
   if ( size == 1 ) // base case
      return b[0];
   else // recursive step
      return b[ size - 1 ] + whatIsThis( b, size - 1 );
} // end function whatIsThis
```

## **7.19**  *(掷骰子游戏修改)*

修改图 6.11 的程序，使其进行 1000 局掷骰子游戏。程序应记录统计信息并回答以下问题：

- a) 在第 1 次投掷、第 2 次投掷……第 20 次投掷以及第 20 次投掷之后，分别赢了多少局？
- b) 在第 1 次投掷、第 2 次投掷……第 20 次投掷以及第 20 次投掷之后，分别输了多少局？
- c) 掷骰子游戏的获胜概率是多少？*[注：你应该会发现掷骰子游戏是赌场中最公平的游戏之一。你认为这意味着什么？]*
- d) 一局掷骰子游戏的平均长度是多少？
- e) 获胜概率会随着游戏长度增加而提高吗？

## **7.20**  *(航空公司预订系统)*

一家小型航空公司刚刚为其新的自动预订系统购买了一台计算机。你被要求为新系统编写程序。你要编写一个程序，为航空公司唯一飞机的每个航班分配座位（容量：10 个座位）。

你的程序应显示以下备选菜单——请输入 1 表示“头等舱”，输入 2 表示“经济舱”。如果此人输入 1，你的程序应在头等舱区域分配一个座位（座位 1–5）。如果此人输入 2，你的程序应在经济舱区域分配一个座位（座位 6–10）。你的程序应打印登机牌，标明此人的座位号以及该座位位于飞机的头等舱还是经济舱区域。

使用一维数组表示飞机的座位图。将数组的所有元素初始化，以表示所有座位均为空。每分配一个座位时，将数组的对应元素设置为 true，以表示该座位不再可用。

当然，你的程序绝不应分配已经分配过的座位。当头等舱区域满员时，你的程序应询问此人是否可接受被安排到经济舱区域（反之亦然）。如果同意，则进行适当的座位分配。如果不同意，则打印消息“下一班航班将在 3 小时后起飞。”

## **7.21**  *(这段代码做什么？)*

下面的程序做什么？

```cpp
// Ex. 7.21: Ex07_21.cpp
// What does this program do?
#include <iostream>
using namespace std;

void someFunction( int [], int, int ); // function prototype

int main()
{
   const int arraySize = 10;
   int a[ arraySize ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

   cout << "The values in the array are:" << endl;
   someFunction( a, 0, arraySize );
   cout << endl;
} // end main

// What does this function do?
void someFunction( int b[], int current, int size )
{
   if ( current < size )
   {
      someFunction( b, current + 1, size );
      cout << b[ current ] << ' ';
   } // end if
} // end function someFunction
```

```text
5, 12
1
6
9
```

当海龟落笔移动时，将数组 floor 的相应元素设置为 true。当给出 6 命令（打印）时，在数组中为 true 的位置显示星号或你选择的其他字符。在为零的位置显示空白。编写一个程序实现这里讨论的海龟图形功能。编写几个海龟图形程序来绘制有趣的形状。添加其他命令以增强你的海龟图形语言的能力。

## 7.24 (骑士巡游)

对国际象棋爱好者来说，更有趣的谜题之一是骑士巡游问题。问题是：被称为骑士的棋子能否在空棋盘上移动，并且恰好一次访问 64 个方格中的每一个？我们在本练习中深入研究这个有趣的问题。

骑士走 L 形移动（先沿一个方向移动两格，再沿垂直方向移动一格）。因此，从空棋盘中央的方格出发，骑士可以做出八种不同的移动（编号 0 到 7），如图 7.28 所示。

- a) 在一张纸上画一个 8×8 棋盘，并尝试手工完成骑士巡游。在你移动到的第一个方格中写 1，第二个方格写 2，第三个写 3，依此类推。开始巡游前，估计你认为自己能走多远，记住完整巡游包含 64 步。你走了多远？这接近你的估计吗？

- b) 现在让我们开发一个程序，让骑士在棋盘上移动。棋盘用 8×8 二维数组 board 表示。每个方格初始化为零。我们用水平和垂直分量描述八种可能的移动。例如，如图 7.28 所示，类型 0 的移动由水平向右移动两格、垂直向上移动一格组成。移动 2 由水平向左移动一格、垂直向上移动两格组成。向左的水平移动和向上的垂直移动用负数表示。这八种移动可以用两个一维数组 horizontal 和 vertical 描述如下：

```cpp
horizontal[ 0 ] =  2    vertical[ 0 ] = -1
horizontal[ 1 ] =  1    vertical[ 1 ] = -2
horizontal[ 2 ] = -1    vertical[ 2 ] = -2
horizontal[ 3 ] = -2    vertical[ 3 ] = -1
horizontal[ 4 ] = -2    vertical[ 4 ] =  1
horizontal[ 5 ] = -1    vertical[ 5 ] =  2
horizontal[ 6 ] =  1    vertical[ 6 ] =  2
horizontal[ 7 ] =  2    vertical[ 7 ] =  1
```

![](img/bfd978e7e9b192bab46ec2a89e481263_357_0.png)

图 7.28 | 骑士的八种可能移动。

