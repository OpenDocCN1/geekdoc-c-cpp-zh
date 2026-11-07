

## 示例 5-5

### 电话数字

下面的程序读取字母代码 A 到 Z，并打印相应的电话数字。该程序使用一个哨兵控制的 while 循环。要停止程序，系统会提示用户输入哨兵，即 #。这也是一个嵌套控制结构的示例，其中 if...else、switch 和 while 循环嵌套在一起。

```cpp
//************************************************************
// Program: Telephone Digits
// This is an example of a sentinel-controlled loop. This
// program converts uppercase letters to their corresponding
// telephone digits.
//************************************************************

#include <iostream>

using namespace std;

int main()
{
        char letter;                                      //Line 1

        cout << "Program to convert uppercase "
             << "letters to their corresponding "
             << "telephone digits." << endl;              //Line 2

        cout << "To stop the program enter #."
             << endl;                                     //Line 3

        cout << "Enter a letter: ";                       //Line 4
        cin >> letter;                                    //Line 5
        cout << endl;                                     //Line 6

        while (letter != '#')                             //Line 7
        {
                cout << "The letter you entered is: "
                     << letter << endl;                  //Line 8
                cout << "The corresponding telephone "
                     << "digit is: ";                    //Line 9

                if (letter >= 'A' && letter <= 'Z')       //Line 10
                    switch (letter)                      //Line 11
                    {
                        case 'A':
                        case 'B':
                        case 'C':
                            cout << 2 << endl;             //Line 12
                            break;                       //Line 13
                        case 'D':
                        case 'E':
                        case 'F':
                            cout << 3 << endl;             //Line 14
                            break;                        //Line 15
                        case 'G':
                        case 'H':
                        case 'I':
                            cout << 4 << endl;             //Line 16
                            break;                        //Line 17
                        case 'J':
                        case 'K':
                        case 'L':
                            cout << 5 << endl;             //Line 18
                            break;                        //Line 19
                        case 'M':
                        case 'N':
                        case 'O':
                            cout << 6 << endl;             //Line 20
                            break;                        //Line 21
                        case 'P':
                        case 'Q':
                        case 'R':
                        case 'S':
                            cout << 7 << endl;             //Line 22
                            break;                        //Line 23
                        case 'T':
                        case 'U':
                        case 'V':
                            cout << 8 << endl;             //Line 24
                            break;                        //Line 25
                        case 'W':
                        case 'X':
                        case 'Y':
                        case 'Z':
                            cout << 9 << endl;             //Line 26
                    }
                else
                    cout << "Invalid input." << endl;      //Line 27

                cout << "\nEnter another uppercase "
                     << "letter to find its "
                     << "corresponding telephone digit."
                     << endl;                              //Line 29
                cout << "To stop the program enter #."
                     << endl;                              //Line 30

                cout << "Enter a letter: ";                 //Line 31
                cin >> letter;                              //Line 32
                cout << endl;                               //Line 33
        } //end while

        return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Program to convert uppercase letters to their corresponding telephone digits.
To stop the program enter #.
Enter a letter: A
The letter you entered is: A
The corresponding telephone digit is: 2

Enter another uppercase letter to find its corresponding telephone digit.
To stop the program enter #.
Enter a letter: D
The letter you entered is: D
The corresponding telephone digit is: 3

Enter another uppercase letter to find its corresponding telephone digit.
To stop the program enter #.
Enter a letter: #
Program terminates.
```

此程序的工作方式如下。第 2 行和第 3 行的语句告诉用户该做什么。第 4 行的语句提示用户输入一个字母；第 5 行的语句将该字母读取并存储到变量 letter 中。第 7 行的 while 循环检查该字母是否为 #。如果用户输入的字母不是 #，则执行 while 循环体。第 8 行的语句输出用户输入的字母。第 10 行的 if 语句检查用户输入的字母是否为大写字母。if 语句的语句部分是 switch 语句（第 11 行）。如果用户输入的字母是大写字母，则 if 语句中的表达式（第 10 行）计算结果为 true，并执行 switch 语句；如果用户输入的字母不是大写字母，则执行 else 语句（第 27 行）。第 12 行到第 26 行的语句确定相应的电话数字。

一旦当前字母被处理，第 29 行和第 30 行的语句再次告知用户下一步该做什么。第 31 行的语句提示用户输入一个字母；第 32 行的语句将该字母读取并存储到变量 letter 中。（注意，第 29 行的语句与第 2 行的语句类似，第 30 行到第 33 行的语句与第 3 行到第 6 行的语句相同。）第 33 行的语句（在 while 循环的末尾）执行后，控制权回到 while 循环的开头，并再次开始相同的过程。当用户输入 # 时，程序终止。

请注意，在此程序中，变量 letter 是循环控制变量。首先，它在第 5 行由输入语句初始化，然后在第 32 行更新。第 7 行的表达式检查 letter 是否为 #。

> **注意：** 在示例 5-5 的程序中，你可以使用 switch 结构来编写第 10 行到第 28 行之间的语句。（请参阅本章末尾的编程练习 3。）

## 案例 3：标志控制的 *while* 循环

**标志控制的 while 循环**使用一个 *bool* 变量来控制循环。假设 *found* 是一个 *bool* 变量。标志控制的 while 循环形式如下：

```cpp
found = false;        //initialize the loop control variable
while (!found)        //test the loop control variable
{
    .
    .
    if (expression)
        found = true; //update the loop control variable
    .
    .
}
```

变量 found 用于控制 while 循环的执行，称为**标志变量**。

示例 5-6 进一步说明了标志控制的 while 循环的使用。

### 示例 5-6：猜数字游戏

以下程序随机生成一个大于或等于 0 且小于 100 的整数。然后程序提示用户猜这个数字。如果用户猜对了数字，程序输出一条适当的信息。否则，程序检查猜的数字是否小于随机数。如果猜的数字小于程序生成的随机数，程序输出消息“你的猜测低于该数字。再猜一次！”；否则，程序输出消息“你的猜测高于该数字。再猜一次！”。然后程序提示用户输入另一个数字。系统会一直提示用户猜测随机数，直到用户输入正确的数字。

要生成随机数，可以使用头文件 `cstdlib` 中的函数 `rand`。例如，表达式 `rand()` 返回一个介于 0 和 32767 之间的 `int` 值。因此，语句：

```cpp
cout << rand() << " , " << rand() << endl;
```

将输出两个看似随机的数字。然而，每次运行程序时，此语句都会输出相同的随机数。这是因为函数 `rand` 使用一种算法，在相同系统上每次执行程序时都会产生相同的随机数序列。为了在每次执行程序时生成不同的随机数，还需要使用头文件 `cstdlib` 中的函数 `srand`。函数 `srand` 接受一个 `unsigned int` 作为输入，该值充当算法的种子。通过指定不同的种子值，每次执行程序时，函数 `rand` 将生成不同的随机数序列。要指定不同的种子，可以使用头文件 `ctime` 中的函数 `time`，它返回自 1970 年 1 月 1 日以来经过的秒数。例如，请考虑以下语句：

