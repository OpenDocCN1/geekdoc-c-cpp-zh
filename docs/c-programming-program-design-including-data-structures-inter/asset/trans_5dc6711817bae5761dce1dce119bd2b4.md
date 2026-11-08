
```cpp
case 'D':
case 'E':
case 'F':
    cout << 3 << endl;                  //Line 14
    break;                               //Line 15
case 'G':
case 'H':
case 'I':
    cout << 4 << endl;                  //Line 16
    break;                               //Line 17
case 'J':
case 'K':
case 'L':
    cout << 5 << endl;                  //Line 18
    break;                               //Line 19
case 'M':
case 'N':
case 'O':
    cout << 6 << endl;                  //Line 20
    break;                               //Line 21
case 'P':
case 'Q':
case 'R':
case 'S':
    cout << 7 << endl;                  //Line 22
    break;                               //Line 23
case 'T':
case 'U':
case 'V':
    cout << 8 << endl;                  //Line 24
    break;                               //Line 25
case 'W':
case 'X':
case 'Y':
case 'Z':
    cout << 9 << endl;                  //Line 26
}
else                                  //Line 27
    cout << "Invalid input." << endl;  //Line 28

cout << "\nEnter another uppercase "
     << "letter to find its "
     << "corresponding telephone digit. "
     << endl;                          //Line 29
cout << "To stop the program enter #."
     << endl;                          //Line 30

cout << "Enter a letter: ";              //Line 31
cin >> letter;                          //Line 32
cout << endl;                            //Line 33
} //end while

return 0;
}
```

**示例运行：** 在这段示例运行中，用户输入以底纹显示。

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
```

该程序的工作方式如下。第2行和第3行的语句告诉用户要做什么。第4行的语句提示用户输入一个字母；第5行的语句读取该字母并将其存储到变量letter中。第7行的while循环检查该字母不是#。如果用户输入的字母不是#，则执行while循环体。第8行的语句输出用户输入的字母。第10行的if语句检查用户输入的字母是否为大写字母。该if语句的语句体是switch语句（第11行）。如果用户输入的字母是大写字母，则if语句（第11行）中的表达式求值为true，并执行switch语句；如果用户输入的字母不是大写字母，则执行else语句（第27行）。第12行到第26行的语句确定对应的电话数字。

处理完当前字母后，第29行和第30行的语句会再次告知用户接下来要做什么。第31行的语句提示用户输入一个字母；第32行的语句读取该字母并将其存储到变量letter中。（注意，第29行的语句与第2行的语句类似，第30行到第33行的语句与第3行到第6行的语句相同。）第33行的语句（位于while循环末尾）执行后，控制权回到while循环顶部，并再次开始相同的过程。当用户输入#时，程序终止。

注意，在此程序中，变量letter是循环控制变量。首先，它在第5行由输入语句初始化，然后在第32行更新。第7行的表达式检查letter是否不是#。

> **注意：** 在示例5-5的程序中，你可以使用switch语句编写第10行到第28行之间的语句。（参见本章末尾的编程练习3。）

## 情形3：标志控制的 while 循环

一个**标志控制的 while 循环**使用bool变量来控制循环。假设found是一个bool变量。标志控制的 while 循环采用以下形式：

```text
found = false;        //initialize the loop control variable

while (!found)        //test the loop control variable
{
    .
    .
    .
    if (expression)
        found = true;  //update the loop control variable
    .
    .
    .
}
```

用于控制while循环执行的变量found称为**标志变量**。

示例5-6进一步说明了标志控制的 while 循环的用法。

## 示例5-6

### 猜数字游戏

以下程序随机生成一个大于或等于0且小于100的整数。然后程序提示用户猜这个数。如果用户猜对了这个数，程序会输出相应的消息。否则，程序检查所猜的数是否小于随机数。如果所猜的数小于程序生成的随机数，程序输出消息“你猜的数比这个数小。再猜一次！”；否则，程序输出消息“你猜的数比这个数大。再猜一次！”。然后程序提示用户输入另一个数。程序会提示用户猜这个随机数，直到用户输入正确的数。

要生成随机数，可以使用头文件cstdlib中的函数rand。例如，表达式rand()返回一个介于0和32767之间的int值。因此，语句：

```cpp
cout << rand() << ", " << rand() << endl;
```

将输出两个看起来随机的数。然而，每次运行程序时，这条语句都会输出相同的随机数。这是因为函数rand使用的算法在同一个系统上每次执行程序时都会产生相同的随机数序列。要在每次执行程序时生成不同的随机数，你还可以使用头文件cstdlib中的函数srand。函数srand接受一个unsigned int作为输入，它充当算法的种子。通过指定不同的种子值，每次执行程序时，函数rand将生成不同的随机数序列。要指定不同的种子，可以使用头文件ctime中的函数time，它返回自1970年1月1日以来经过的秒数。例如，考虑以下语句：

```cpp
srand(time(0));
num = rand() % 100;
```

第一条语句设置种子，第二条语句生成一个大于或等于0且小于100的随机数。注意函数time是如何使用的。它带有一个参数，即形参，该参数为0。

该程序使用bool变量isGuessed来控制循环。bool变量isGuessed被初始化为false。当用户猜对数字时，它被设置为true。

```cpp
//Flag-controlled while loop.
//Number guessing game.

#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main()
{
        //declare the variables
        int num;          //variable to store the random
                         //number
        int guess;        //variable to store the number
                         //guessed by the user
        bool isGuessed;   //boolean variable to control
                         //the loop

        srand(time(0));                                  //Line 1
        num = rand() % 100;                              //Line 2

        isGuessed = false;                               //Line 3

        while (!isGuessed)                               //Line 4
        {                                                 //Line 5
            cout << "Enter an integer greater"
                 << " than or equal to 0 and "
                 << " less than 100: ";                  //Line 6

            cin >> guess;                                //Line 7
            cout << endl;                                //Line 8

            if (guess == num)                            //Line 9
            {                                             //Line 10
                cout << "You guessed the correct "
                     << " number." << endl;              //Line 11
                isGuessed = true;                        //Line 12
            }                                             //Line 13
            else if (guess < num)                        //Line 14
                cout << "Your guess is lower than the "
                     << " number.\n Guess again!"
                     << endl;                             //Line 15
```
