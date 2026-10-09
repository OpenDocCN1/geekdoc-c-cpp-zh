
```cpp
cout << "Type in maximum integer to test:" << endl;

cout << "(program will test all whole numbers up to and including this)" << endl;

cin >> userInput;

//---------------------------------------

if ( userInput < 2 ) {

cout << "Max integer must be whole number, 2 or above.";

cout << "Program aborted." << endl;

exit( 1);

} // end of if

//---------------------------------------

for ( unsigned long long loop = 2; loop <= userInput; loop++) {

// Display whether this number is prime or not.

cout << endl << "Testing: " << loop << endl;

cout << loop << " is ";

if ( testForPrime( loop )) {

primesFound++;

} else

cout << "not";

}

} // end of loop that drives the function

//---------------------------------------

// Finished testing the range of numbers,
// display the total number of primes found in this range.

cout << endl << endl;

cout << "FOUND " << primesFound << " PRIMES IN THIS RANGE.";

cout << endl << endl;

return 0;

}
```

以下是要求程序搜索包含 5 在内的所有质数时的运行情况：

![](img/0c86cf81300257fe2415e40f8fb03508_342_0.png)

如果你愿意，可以要求它搜索更大的极大质数，但查找结果将花费更长时间。以下是要求查找一百万以内所有质数时显示的部分结果和最终总结：

## 验证二进制位序列

这里是另一个使用的函数。它检查字符串值是否为有效的 8 位数——即完全由字符 0 或 1 组成且长度正好为八个字符的模式。如果发现字符串值是有效的 8 位二进制模式，则调用 `convertStringToDecimal()` 函数将其转换为十进制（base-10）数字。

示例 10.10 — `function_binary.cpp`

```cpp
#include <iostream> // 程序将使用键盘和屏幕

#include <cmath> // 程序使用 pow() 函数

using namespace std; // 将使用标准标识符 string, cin, cout, endl;

// ------------------------------------------------
```

```cpp
int convertBinStringToDenary( string bitPattern ) 
{
    int result = 0;
    for ( int place = 0; place < 8; place++) {
        if (bitPattern.at(place) == '1')
            result += pow(2, 7 - place); // Pos 0 处的数字表示 2 的 8 次方
    }
    return result;
}
//
```

```cpp
int main() {
    // 输入数字字符串
    cout << "Type in 8-bit binary number..." << endl;
    string binString;
    cin >> binString;
    // 起初假设字符串是正确的
    bool valid = true;
    // 检查字符串是否为 8 个字符
    int stringLen = binString.length();
    if ( stringLen != 8 ) {
        cout << "Not 8 characters long." << endl;
        valid = false;
    } else {
        // 使用循环检查任何不是 0 或 1 的字符
        char thisChar;
        for ( int pos = 0; pos < 8; pos++) {
            thisChar = binString.at(pos);
            if (thisChar != '0' && thisChar != '1') {
                cout << "Invalid: " << thisChar << endl;
                valid = false;
            } // end of if decision
        } // end of for loop
    } // end of if-else decision
    // 告诉用户字符串是否有效
    if ( valid ) {
        cout << "This is a valid 8-bit binary number." << endl;
        cout << "In-base10 it is: ";
        cout << convertStringToDenary ( binString );
    }
    else
        cout << "Not a valid 8-bit binary number.";
    cout << endl;
    // 将成功/错误状态传给 Linux
    return ( valid ? 0 : 1 ); // 如果有效返回 0，如果无效返回 1
}
```

程序首先要求用户输入一个 8 位二进制模式，该模式存储在字符串值 `binString` 中。

然后确定字符串的长度，判断是否恰好为 8 个字符。如果不是，则显示错误消息，并通过将 `valid` 布尔变量设置为 `false` 来将字符串标记为无效。

或者，如果 `binString` 恰好包含 8 个字符，则 `for` 循环从头到尾遍历它们，检查每个单独字符是否为 1 或 0。

如果发现任何字符不是 1 或 0，则该模式标记为无效，并在屏幕上显示违规字符。

下面，你可以看到通过将每个字符移动一个位置来打乱消息的效果：

| 请输入一行文本： |
| :--- |
| My Raspberry Pi fell down from the sky. |

| 乱码/解密位移的个数： |
| 1 |

这变成了...
Nz!SbtqfcsszQ|jgflmmepxo|gspnuifltz/ | |

当给程序一个负数作为乱码/解密的位移个数时，会发生以下情况，这会导致它再次解密消息：

| 请输入一行文本： |
| :--- |
| Nz!SbtqfcsszQ|jgflmmepxo|gspnuifltz/| |

| 乱码/解密位移的个数： |
| -1 |

这变成了...
My Raspberry Pi fell down from the sky. | |

你可以看到，使用大数字乱码的字符会被调整，以确保它们保持在可打印字符的范围内——即 32（空格）到 126（~ 波浪号）之间：

| 请输入一行文本： |
| :--- |
| The Pi in the sky (is a bit dented) |

| 乱码/解密位移的个数： |
| 30 |

这变成了...
r$>n)(->3)$'2>B$F(2)!(3#-$3#G | |

同样的情况也适用于需要解密的消息：

| 请输入一行文本： |
| :--- |
| r$>n)(->3)$'2>B$F(2)!(3#-$3#G | |

| 乱码/解密位移的个数： |
| -30 |

这变成了...
The Pi in the sky (is a bit dented) | |

## 不返回任何结果的函数

尽管许多函数在完成执行后返回某些数据，但某些函数完全不返回任何内容！不返回值的函数被称为“void”（空）函数。这种函数不需要在体内部包含 `return` 语句，因为它不会向其调用的代码提供任何结果。

C++ `void` 函数的操作方式与你在许多其他编程语言中创建创建“过程”（procedures）相同。你可以将它们视为命名的指令序列，可以从程序的其他地方进行调用。

这是一个 `void` 函数的示例：

```cpp
void startNewGame() {
  score = 0;
  lives = 3;
  // 不需要 return 语句 -这是一个 "void" 函数
}
```

示例 10.12 展示了如何在 `main()` 内部调用并激活名为 `sayHi()` 的 `void` 函数：

```cpp
#include <iostream> // 程序将使用键盘和屏幕
using namespace std; // 将使用标准标识符 cout 和 endl
//------------------------------------------------------------------
void sayHi(int times) {
  int completed = 0;
  while (completed < times) {
    cout << "*** *** *********" << endl;
    cout << "********* *** *********" << endl;
    cout << "***" << endl;
    cout << "********* *** ***" << endl;
    cout << "*** *** **********" << endl;
    cout << "*** *** **********" << endl << endl << endl;
    completed++;
  } // while 循环结束
//----------------------------------------------------------------
```

```cpp
int main() {
  sayHi(3); // 单次调用函数以显示消息 3 次
  return 0;
}
```

当程序运行时，对函数 `sayHi()` 的调用将值 `3` 作为参数传递。这告诉函数要反复显示三次消息。然而，它并没有尝试返回任何结果，因为 `sayHi()` 函数执行的所有有用工作都已显示在屏幕上。

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

sayHi()

sayHi()

sayHi()

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

***

(程序以代码：0 退出)

按回车键继续

## 导航源代码以查找特定函数

注意，如果你正在使用 Geany，你会在窗口左侧看到 **Symbols**（符号）面板，无需在文本编辑器窗格中上下滚动，即可跳转到你编写的特定函数的源代码。

如果你在 **Functions**（函数）标题下查看，你应该能看到你在程序中创建的每个函数的**名称**，包括 **main()** 函数。与之显示的是该函数在源代码中开始的**行号**（显示在方括号中）。你只需要点击你想要跳转的函数名称即可。随着程序变大，这可以让你找到想要处理的内容容易得多。

![](img/0c86cf81300257fe2415e40f8fb03508_349_0.png)

如果由于某些原因你看不到侧边栏或 **Symbols** 面板，请前往 Geany 窗口的 **View** 菜单并选择 **Symbols** 侧边栏。

在后面的“第十三章：对象和类”中，你将学习**类**。**classes** 侧边栏将显示类的方法。

## 更多函数参数 - 拷贝

当你激活函数并传递数据值作为参数时，除非你另有说明，否则这些值被称为函数的“局部”变量。这些局部值只在函数激活时存在。一旦函数结束，数据值将不再存在。

如果你将变量的值作为输入（参数）传递给函数会发生什么？让我们详细考虑参数的情况。

假设有这样一个程序：

```cpp
#include <iostream>    // 程序将在屏幕上显示一些文本
using namespace std; // 将使用标准标识符和 endl
int main() {
    int myNumber = 25;
    cout << "原始变量的值为 " << myNumber << endl;
    displayTimesBigger(myNumber);
    // 按值传递 25 对原始变量没有影响
    cout << "原始变量的值为 \n" << myNumber << endl;
    return 0;
}
```

现在，这是从 `main()` 用的 `displayTimesBigger()` 函数的代码：

```cpp
void displayTimesBigger(int numberToMakeBigger) {
    numberToMakeBigger *= 10;
    cout << "乘以10 得到 " << numberToMakeBigger << endl;
}
```

注意，在 `displayTimesBigger()` 函数内部，变量 `numberToMakeBigger` 的值被改变并显示在屏幕上。

但是作为参数传递给 `displayTimesBigger()` 函数的 `main()` 函数中原始变量 `myNumber` 的值发生了什么？答案是：什么都没有。

`main` 中的 `myNumber` 值不受 `displayTimesBigger()` 函数内部操作的影响。这是因为函数处理的是 `myNumber` 值的拷贝。

## 使用值的 & 引用直接操作其输入数据的函数

通过对之前的函数 `displayTimesBigger()` 进行细微修改，我们可以告诉计算机对作为输入值的实际变量进行操作，而不是对变量的副本进行操作。

在定义函数参数时，可以将 `&`（“引用”）符号放在任何变量名的开头。

这意味着函数将不再对参数的副本进行操作，而是对实物进行操作，引用我们作为输入所提供的实际值。为了实现这一点，你的树莓派将使用该变量在内存中的地址：

```cpp
void displayTimesBigger(int &numberToMakeBigger)
{
    numberToMakeBigger *= 10;
    cout << numberToMakeBigger << endl;
}
```

这一次，实际变量 `myNumber` 的内存地址作为输入传递给 `displayTimesBigger()` 函数进行处理，而不是传递其值的副本。

如果 `myNumber` 的原始值为 25，该函数会将变量的值乘以 10，得到 250 的结果。即使在函数执行完毕，该变量也将保留此值。当使用变量引用作为函数参数时，函数内部发生的操作在函数执行结束后可能会产生持久的影响。

```cpp
int myNumber = 25;
// 在调用函数 displayTenTimesBigger 之前显示 25
cout << myNumber << endl;
// 调用函数将数字放大 10 倍并显示它
displayTenTimesBigger(myNumber);
// 将显示 250，因为函数更改的是实际变量而非其副本
cout << myNumber << endl;
```

这非常有用，特别是在编写处理组织好的数据值集合（如数组）的函数时。例如，正如我们在章早些时候看到的，可以通过将数组的引用传递给排序函数来对值按顺序排序，从而永久地排序值。

## 将数组作为函数的输入

此程序将一些数据存储在一个名为 `cityName` 的数组中。除了 `main()` 之外，它还包含两个函数：

- `displayArray()` 显示字符串值数组的内容。
- `sortArray()` 对字符串值数组执行简单的“冒泡排序”。

示例 10.14 - `function_bubble_sort.cpp`

```cpp
#include <iostream>    // 程序将在屏幕上显示一些文本作为输出
```
