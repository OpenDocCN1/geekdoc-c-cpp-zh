

```cpp
// Fig. 6.9: fig06_09.cpp
// Craps simulation.
#include <iostream>
#include <cstdlib> // contains prototypes for functions srand and rand
#include <ctime> // contains prototype for function time
using namespace std;

unsigned int rollDice(); // rolls dice, calculates and displays sum

int main() {
   // scoped enumeration with constants that represent the game status
   enum class Status {CONTINUE, WON, LOST}; // all caps in constants

   // randomize random number generator using current time
   srand(static_cast<unsigned int>(time(0)));

   unsigned int myPoint{0}; // point if no win or loss on first roll
   Status gameStatus; // can be CONTINUE, WON or LOST
   unsigned int sumOfDice{rollDice()}; // first roll of the dice

   // determine game status and point (if needed) based on first roll
   switch (sumOfDice) {
      case 7: // win with 7 on first roll
      case 11: // win with 11 on first roll
         gameStatus = Status::WON;
         break;
      case 2: // lose with 2 on first roll
      case 3: // lose with 3 on first roll
      case 12: // lose with 12 on first roll
         gameStatus = Status::LOST;
         break;
      default: // did not win or lose, so remember point
         gameStatus = Status::CONTINUE; // game is not over
         myPoint = sumOfDice; // remember the point
         cout << "Point is " << myPoint << endl;
         break; // optional at end of switch
   }

   // while game is not complete
   while (Status::CONTINUE == gameStatus) { // not WON or LOST
      sumOfDice = rollDice(); // roll dice again

      // determine game status
      if (sumOfDice == myPoint) { // win by making point
         gameStatus = Status::WON;
      }
      else {
         if (sumOfDice == 7) { // lose by rolling 7 before point
            gameStatus = Status::LOST;
         }
      }
   }

   // display won or lost message
   if (Status::WON == gameStatus) {
      cout << "Player wins" << endl;
   }
   else {
      cout << "Player loses" << endl;
   }
}

// roll dice, calculate sum and display results
unsigned int rollDice() {
   int die1{1 + rand() % 6}; // first die roll
   int die2{1 + rand() % 6}; // second die roll
   int sum{die1 + die2}; // compute sum of die values

   // display results of this roll
   cout << "Player rolled " << die1 << " + " << die2
        << " = " << sum << endl;
   return sum;
}
```

```
Player rolled 2 + 5 = 7
Player wins
```

```
Player rolled 6 + 6 = 12
Player loses
```

```
Player rolled 1 + 3 = 4
Point is 4
Player rolled 4 + 6 = 10
Player rolled 2 + 4 = 6
Player rolled 6 + 4 = 10
Player rolled 2 + 3 = 5
Player rolled 2 + 4 = 6
Player rolled 1 + 1 = 2
Player rolled 4 + 4 = 8
Player rolled 4 + 3 = 7
Player loses
```

```
Player rolled 3 + 3 = 6
Point is 6
Player rolled 5 + 3 = 8
Player rolled 4 + 5 = 9
Player rolled 2 + 1 = 3
Player rolled 1 + 5 = 6
Player wins
```

图 6.9 Craps 游戏模拟。

## C++11：*有作用域的* `enum`

玩家可能在第一次掷骰子时获胜或失败，也可能在之后的任意一次掷骰子时获胜或失败。程序通过变量 `gameStatus` 跟踪这一状态，该变量声明为新类型 `Status`（第 18 行）。第 12 行声明了一种名为**有作用域的枚举**（C++11）的用户定义类型，它由关键字 `enum class`、类型名称（`Status`）以及一组表示整数常量的标识符组成。这些**枚举常量**的值属于 `int` 类型，从 `0` 开始（除非另有指定），并以 `1` 为增量递增。在前面的枚举中，常量 `CONTINUE` 的值为 0，`WON` 的值为 1，`LOST` 的值为 2。`enum class` 中的标识符必须是*唯一的*，但不同的枚举常量*可以*具有相同的整数值。用户定义类型 `Status` 的变量只能被赋予枚举中声明的三个值之一。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_744_0.png)

### 良好的编程实践 6.2

*按照惯例，应将 `enum class` 名称的首字母大写。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_744_1.png)

### 良好的编程实践 6.3

*枚举常量名称只使用大写字母。这样可以使这些常量在程序中更加醒目，并提醒你枚举常量不是变量。*

要引用有作用域的 `enum` 常量，必须使用该有作用域 `enum` 的类型名称（`Status`）和作用域解析运算符（`::`）限定该常量，例如 `Status::CONTINUE`。游戏获胜时，程序将变量 `gameStatus` 设置为 `Status::WON`（第 25 行和第 45 行）。游戏失败时，程序将变量 `gameStatus` 设置为 `Status::LOST`（第 30 行和第 49 行）。否则，程序将变量 `gameStatus` 设置为 `Status::CONTINUE`（第 33 行），表示必须再次掷骰子。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_745_0.png)

### 防错提示 6.6

*使用类型名称和 `::` 限定 `enum class` 的常量，可以明确标识该常量属于指定 `enum class` 的作用域。如果另一个 `enum class` 包含同名常量，那么由于必须使用类型名称和 `::`，因此始终可以清楚地知道使用的是哪个版本的常量。*

另一种常见的有作用域枚举是

```cpp
enum class Months { JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG,
    SEP, OCT, NOV, DEC };
```

它创建了用户定义类型 `Months`，其中的枚举常量表示一年中的各个月份。在前面的枚举中，第一个值被显式设置为 `1`，因此其余值从 `1` 开始递增，最终得到 `1` 到 `12` 的值。在枚举定义中，可以为任意枚举常量指定整数值；在下一个显式设置之前，后续每个枚举常量的值都比列表中前一个常量高 1。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_746_0.png)

### 防错提示 6.7

*为 `enum` 的常量使用唯一的值，以帮助避免难以发现的逻辑错误。*

### 第一次掷骰子时获胜或失败

第一次掷骰子后，如果游戏获胜或失败，程序会跳过 `while` 语句（第 40—52 行）的主体，因为 `gameStatus` 不等于 `Status::CONTINUE`。程序继续执行第 55—60 行的 `if...else` 语句：当 `gameStatus` 等于 `WON` 时打印**“玩家获胜”**，当 `gameStatus` 等于 `Status::LOST` 时打印**“玩家失败”**。

### 继续掷骰子

第一次掷骰子后，如果游戏尚未结束，程序会将总和保存到 `myPoint` 中（第 34 行）。由于 `gameStatus` 为 `Status::CONTINUE`，程序继续执行 `while` 语句。在 `while` 的每次迭代中，程序调用 `rollDice` 生成新的 `sum`。如果 `sum` 与 `myPoint` 匹配，程序会将 `gameStatus` 设置为 `Status::WON`（第 45 行），`while` 测试失败，`if...else` 语句打印**“玩家获胜”**，程序执行结束。如果 `sum` 等于 `7`，程序会将 `gameStatus` 设置为 `Status::LOST`（第 49 行），`while` 测试失败，`if...else` 语句打印 `"Player loses"`，程序执行结束。

Craps 程序使用了两个函数——`main` 和 `rollDice`——以及 `switch`、`while`、`if...else`、嵌套的 `if...else` 和嵌套的 `if` 语句。我们将在练习中进一步研究 Craps 游戏。

### C++11 之前的枚举类型

在 C++11 之前，枚举使用关键字 `enum` 定义，后面跟着类型名称以及一组由标识符表示的整数常量，例如：

```cpp
enum Status {CONTINUE, WON, LOST};
```

这些常量是*无作用域的*——只需使用 `CONTINUE`、`WON` 和 `LOST` 即可引用它们。如果两个或更多无作用域的 `enum` 包含同名常量，就可能导致命名冲突和编译错误。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_747_0.png)

### 防错提示 6.8

使用有作用域的 `enum`，以避免无作用域枚举常量可能引发的命名冲突。

### C++11——指定 `enum` 常量的类型（可选）

枚举常量具有整数值。*无作用域* `enum` 的底层类型取决于其常量的值，并且保证足够大，可以存储这些常量的值。*有作用域* `enum` 的底层整数类型是 `int`，但可以在类型名称后面添加冒号（`:`）和整数类型来指定其他类型。例如，可以将 `enum class Status` 中的常量指定为 `unsigned int` 类型，如下所示：

```cpp
enum class Status : unsigned int {CONTINUE, WON, LOST};
```

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_748_0.png)

### 常见编程错误 6.5

如果 `enum` 常量的值超出其底层类型能够表示的范围，就会发生编译错误。

