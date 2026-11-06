
## while 循环

### 第6步

务必记住，不要在 while 语句末尾添加分号。为什么？如你所知，分号表示 C++ 代码行的结束。如果你在 while 语句末尾放置一个分号，你的循环将永久卡住，直到你关闭程序。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_56_0.png)

### 第7步

在我们的示例中，如果执行代码，num 的值将是 1，这是由 int 语句设置的。当代码执行到 while 语句时，它读取到：只要 1 小于 30 的条件为真，就循环。分号结束了这一行，因此循环会重复；但它永远不会给 num 加 1，因为它不会继续执行复合语句。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_56_1.png)

### 第8步

你可以调整 while 语句，根据循环内的代码显示不同结果。例如，要逐词读取诗歌《辛梅里亚》，你会输入：

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main ()
{
    string word;
    ifstream newfile ("C:\\users\\david\\Documents\\Cimmeria.txt");

    cout << "Cimmeria, by Robert E Howard: \n" << endl;

    while (newfile >> word)
    {
        cout << word << endl;
    }

    return 0;
}
```

### 第9步

你可以进一步扩展代码，使诗歌中的每个单词每隔一秒出现。为此，你需要引入一个新库 <windows.h>。这是一个仅限 Windows 的库，在其中可以使用 Sleep() 函数：

```cpp
#include <iostream>
#include <fstream>
#include <windows.h>
using namespace std;

int main ()
{
    string word;
    ifstream newfile ("C:\\users\\david\\Documents\\Cimmeria.txt");

    cout << "Cimmeria, by Robert E Howard: \n" << endl;

    while (newfile >> word)
    {
        cout << word << endl;
        Sleep(1000);
    }

    return 0;
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_56_2.png)

### 第10步

Sleep() 以毫秒为单位工作，因此 Sleep(1000) 是一秒，Sleep(10000) 是十秒，依此类推。将 sleep 函数（以及它所需的头文件）与 while 循环结合，可以编写出一些有趣的倒计时代码。

```cpp
#include <iostream>
#include <windows.h>
using namespace std;

int main ()
{
    int a = 10;

    while (a != 0)
    {
        cout << a << endl;
        a = a - 1;
        Sleep(1000);
    }

    cout << "\nBlast Off!" << endl;

    return 0;
}
```

## for 循环

在某些方面，for 循环的工作方式与 while 循环非常相似，尽管其结构不同。for 循环分为三个阶段：初始化、条件和增量步进。一旦设置好，循环会重复执行，直到条件变为假。

### 循环的循环

for 循环的初始化阶段只执行一次，它设置循环的起始参考点。循环会评估条件以判断其为真还是假，然后执行增量。随后循环重复第二阶段和第三阶段。

### 第1步

创建一个新的 C++ 文件，包含标准头文件：

```cpp
#include <iostream>
using namespace std;

int main ()
{

}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_57_0.png)

### 第2步

从简单开始，创建一个从 1 数到 30 的 for 循环，每次递增时在屏幕上显示该值：

```cpp
{
    //For Loop Begins
    for( int num = 1; num < 30; num = num +1 )
    {
        cout << "Number: " << num << endl;
    }
    return 0;
}
```

### 第3步

逐步分析 for 循环的过程：首先创建一个名为 num 的整数，并赋值为 1。接下来设置条件，这里是 num 小于 30。最后阶段是创建增量；这里是让 num 的值加 1。

```cpp
{
    //For Loop Begins
    for( int num = 1; num < 30; num = num +1 )
```

### 第4步

在循环之后，你在大括号中创建了一个复合语句，用于显示整数 num 的当前值。每次 for 循环重复自身（即循环的第二和第三阶段）时，它都会加 1，直到 <30 的条件为假。然后循环结束，代码继续执行，最后以 return 0 干净地结束。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_57_1.png)

### 第5步

在 C++ 中，for 循环是一个相当整洁的封装，全部包含在其自身的括号内，而循环外部的其他元素则显示在下方。如果你想创建一个 10 秒倒计时，可以使用：

```cpp
#include <iostream>
#include <windows.h>
using namespace std;

int main ()
{
    //For Loop Begins
    for( int a = 10; a != 0; a = a -1 )
    {
        cout << a << endl;
        Sleep(1000);
    }

    cout << "\nBlast Off!" << endl;
    return 0;
}
```

### 第6步

对于倒计时代码，不要忘记包含 windows.h 库，以便使用 Sleep 命令。构建并运行代码；在命令控制台中，你可以看到数字从 10 到 1 以一秒为增量倒计时，直到到达零并出现 Blast Off!。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_58_0.png)

### 第7步

当然，你可以在 for 循环中加入更多内容，包括一些用户输入：

```cpp
int i, n, fact = 1;

cout << "Enter a whole number: ";
cin >> n;

for (i = 1; i <= n; ++i) {
    fact *= i;
}

cout << "\nFactorial of " << n << " = " << fact << endl;

return 0;
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_58_1.png)

### 第8步

第 7 步的代码在构建并运行后，会要求输入一个数字，然后通过 for 循环显示该数字的阶乘。用户的数字存储在整数 n 中，随后整数 i 用于检查条件为真还是假，每次加 1 并与用户的数字 n 进行比较。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_58_2.png)

### 第9步

下面是一个 for 循环示例，显示用户输入数字的乘法表。对学生来说很方便：

```cpp
{
    int n;

    cout << "Enter a number to view its times table: ";
    cin >> n;

    for (int i = 1; i <= 12; ++i) {
        cout << n << " x " << i << " = " << n * i << endl;
    }

    return 0;
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_58_3.png)

### 第10步

整数 i 的值可以从 12 扩展到任意你想要的数字，并在此过程中显示一个非常大的乘法表（或较小的乘法表）。当然，for 循环中的数据类型不必是整数，只要是有效的，就可以工作。

```cpp
for ( float i = 0.00; i < 1.00; i += 0.01)
{
    cout << i << endl;
}

return 0;
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_58_4.png)

## do... while 循环

do... while 循环与 for 甚至 while 循环略有不同。for 和 while 都在循环开始时（或者如果你愿意，在循环顶部）设置并检查条件状态。然而，do... while 循环与 while 循环类似，但它是在循环底部检查条件。

### do 循环

do... while 循环的好处是它保证至少执行一次。其结构是：do，后接语句，while 条件为真。它的工作方式如下。

### 第1步

——从一个新的空白 C++ 文件开始，并输入标准头文件：

```cpp
#include <iostream>
using namespace std;

int main ()
{
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_59_0.png)

### 第2步

——从一个简单的数字计数开始：

```cpp
{
    int num = 1;
    do
    {
        cout << "Number: " << num << endl;
        num = num + 1;
    }
    while (num < 30 );

    return 0;
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_59_1.png)

### 第3步

——现在来看看 do... while 循环的结构。首先创建一个名为 num 的整数，值为 1。现在 do... while 循环开始。循环体内的代码至少执行一次，然后检查条件为真还是假。

```cpp
// Create integer with the value of 1
int num = 1;

// Do... While loop begins
do
{
    cout << "Number: " << num << endl; // Display the current value of num
    num = num + 1; // Adds 1 to the value of num
}
while (num < 30 ); // Tests the condition of num (true or false)
```

### 第4步

——如果条件为真，则执行循环。这一过程持续到条件为假。当条件被表示为假时，循环终止，代码继续执行。这意味着你可以创建一个循环，让代码持续执行，直到用户输入某个特定字符。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_59_2.png)

