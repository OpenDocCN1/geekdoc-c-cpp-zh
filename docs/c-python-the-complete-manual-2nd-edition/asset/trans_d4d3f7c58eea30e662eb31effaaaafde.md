

## 循环与
决策

循环和重复是任何编程语言最重要的因素之一。合理使用循环可以创建一个程序，它完全按照你的期望执行，并在没有问题或错误的情况下提供所需的结果。

如果代码中没有循环和决策事件，你的程序将永远无法为用户提供任何选择。正是对选择的这种理解提升了你作为程序员的技能，并使代码变得更好。

- 126 While 循环
- 128 For 循环
- 130 Do... While 循环
- 132 If 语句
- 134 If... Else 语句

## While 循环

while 循环的功能是在某个条件保持为真时重复一条语句或一组语句。当 while 循环开始时，它通过测试循环的条件和其中的语句来初始化自身，然后执行循环的其余部分。

### TRUE OR FALSE？

while 循环是 C++ 代码中最受欢迎的循环形式之一。它在条件为真时反复运行循环内的代码。一旦条件证明为假，代码就会照常继续。

### STEP 1

清除你迄今为止所做的工作并创建一个新的 C++ 文件。目前不需要任何额外的头文件，所以按通常的方式添加标准头文件：

```
#include <iostream>
using namespace std;

int main ()
{
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_125_0.png)

### STEP 2

创建一个简单的 while 循环。输入下面的代码，构建并运行（我们在屏幕截图中添加了注释）：

```
{
    int num = 1;
    while (num < 30 )
    {
        cout << "Number: " << num << endl;
        num = num +1;
    }
    return 0;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_125_1.png)

### STEP 3

首先你需要创建一个条件，所以使用一个名为 num 的变量并赋值为 1。现在创建 while 循环，说明只要 num 小于 30，循环就为真。在循环内，num 的值会被显示并加 1，直到它大于 30。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_125_2.png)

### STEP 4

我们在这里引入了一些新元素。首先是 while 循环的开头和结尾大括号。这是因为我们的循环是一个复合语句，意味着一组语句；请注意，while 语句后面没有分号。你现在也有了 return 0，这是一种干净且首选的结束代码的方式。

```
int num = 1; // Create the condition
while (num < 30) // The condition remains true while num is less than 30
{
    cout << "Number: " << num << endl; // Displays the current value of num
    num = num +1; // Adds 1 to the value of num
}
return 0; // Correctly closes the code and finishes the program
```

### STEP 5

如果你不需要看到 num 不断增加的值，你可以放弃复合 while 语句，而只是单独使用 num，直到它达到 30，然后再显示该值：

```
{
    int num = 1;
    while (num < 30 )
        num++;
    cout << "Number: " << num << endl;
    return 0;
}
```

### STEP 6

重要的是要记住不要在 while 语句末尾添加分号。为什么呢？正如你所知，分号代表 C++ 代码行的结束。如果你把它放在 while 语句的末尾，你的循环将永久卡住，直到你关闭程序。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_126_0.png)

### STEP 7

在我们的示例中，如果我们执行代码，num 的值将为 1，如 int 语句所设置。当代码遇到 while 语句时，它会读取只要 1 小于 30 的条件为真，就循环。分号关闭该行，因此循环重复；但它永远不会给 num 加 1，因为它不会继续通过复合语句。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_126_1.png)

### STEP 8

你可以操纵 while 语句以根据循环内的代码显示不同的结果。例如，要逐字读取诗歌《Cimmeria》，你需要输入：

```
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

### STEP 9

你可以进一步扩展代码，使诗歌的每个单词每秒出现一次。为此，你需要引入一个新的库，<windows.h>。这是一个仅限 Windows 的库，在其中你可以使用 Sleep() 函数：

```
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

![](img/2f9c26fcf758b5bc56897d9c75b6347f_126_2.png)

### STEP 10

Sleep() 以毫秒为单位工作，因此 Sleep(1000) 为一秒，Sleep(10000) 为十秒，依此类推。结合 sleep 函数（以及它需要的头文件）和 while 循环，你可以制作一些有趣的倒计时代码。

```
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

## For 循环

在某些方面，for 循环的工作方式与 while 循环非常相似，尽管其结构不同。for 循环分为三个阶段：初始化器、条件和增量步骤。设置好后，循环会重复自身，直到条件变为假。

### LOOPY LOOPS

for 循环的初始化阶段只执行一次，这为循环设置了参考点。循环通过判断条件是否为真或假来评估条件，然后执行增量。循环然后重复第二和第三阶段。

### STEP 1 Create a new C++ file, with the standard headers:

```
#include <iostream>
using namespace std;

int main ()
{ 
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_127_0.png)

### STEP 2 Start simple and create a for loop that counts from 1 to 30, displaying the value to the screen with each increment:

```
{ 
    //For Loop Begins
    for( int num = 1; num < 30; num = num +1 )
    {
        cout << "Number: " << num << endl;
    }
    
    return 0;
}
```

### STEP 3 Working through the process of the for loop, begin by creating an integer called num and assigning it a value of 1. Next, set the condition, in this case num being less than 30. The last stage is where you create the increments; here it’s the value of num being added by 1.

```
{ 
    //For Loop Begins
    for( int num = 1; num < 30; num = num +1 )
```

### STEP 4 After the loop, you created a compound statement in braces (curly brackets), that displays the current value of the integer num. Every time the for loop repeats itself, the second and third stages of the loop, it adds 1 until the condition <30 is false. The loop then ends and the code continues, ending neatly with return 0.

```
{ 
    //For Loop Begins
    for( int num = 1; num < 30; num = num +1 )
    {
        cout << "Number: " << num << endl;
    }
    
    return 0;
}
```

### STEP 5 A for loop is quite a neat package in C++, all contained within its own brackets, while the other elements outside of the loop are displayed below. If you want to create a 10-second countdown, you could use:

```
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

### STEP 6

使用倒计时代码时，不要忘记包含 windows.h 库，以便你可以使用 Sleep 命令。构建并运行代码；在命令控制台中，你可以看到数字从 10 到 1 以一秒为间隔倒计时，直到达到零并出现 Blast Off！

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_0.png)

### STEP 7

自然地，你可以在 for 循环中包含更多内容，包括一些用户输入：

```
int i, n, fact = 1;
cout << "Enter a whole number: ";
cin >> n;
for (i = 1; i <= n; ++i) {
    fact *= i;
}
cout<< "\nFactorial of "<< n <<" = "<< fact << endl;
return 0;
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_1.png)

### STEP 8

步骤 7 的代码在构建并运行时，会要求输入一个数字，然后通过 for 循环显示该数字的阶乘。用户的数字存储在整数 n 中，然后是整数 i，用于检查条件是否为真或假，每次加 1 并与用户的数字 n 进行比较。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_2.png)

### STEP 9

下面是一个 for 循环显示用户输入数字的乘法表的示例。对学生很有用：

```
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

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_3.png)

### STEP 10

整数 i 的值可以从 12 扩展到你想要的任何数字，从而在过程中显示非常大的乘法表（或很小的表）。当然，for 循环中的数据类型不必是整数；只要有效，就可以使用。

```
for ( float i = 0.00; i < 1.00; i += 0.01)
{
    cout << i << endl;
}
return 0;
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_4.png)

