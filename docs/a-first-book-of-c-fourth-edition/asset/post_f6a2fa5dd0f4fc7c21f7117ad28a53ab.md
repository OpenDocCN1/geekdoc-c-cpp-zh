
## Modularity Using Functions

![](img/202cface8244f523c2641baa2e00d7dd_289_0.png)

Because each function “knows” only its own local variables, main() can send only the value of its secnum to cout, and valfun() can send only the value of its secnum to cout. Therefore, whenever secnum is obtained from main(), the value of 20 is displayed, and whenever secnum is obtained from valfun(), the value 30 is displayed. C++ doesn’t confuse the two secnum variables because only one function can execute at a time. While a function is executing, only variables and parameters that are “in scope” for that function (global and local) can be accessed.

The scope of a variable in no way influences or restricts its data type. Just as a local variable can be a character, integer, Boolean, double, or any other data type that’s been introduced, global variables can be all these data types, as shown in Figure 6.12. A variable’s scope is determined by the placement of the definition statement that reserves storage for it and optionally by a declaration statement that makes it visible, whereas a variable’s data type is determined by using a keyword (char, int, bool, double, and so on) before the variable’s name in a declaration statement.

![](img/202cface8244f523c2641baa2e00d7dd_289_1.png)

### 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂布局的PDF文件中提取结构化信息。

随着数字化办公的普及，PDF文档已成为信息交换的主要载体之一。然而，由于其格式的封闭性，直接从PDF中提取可编辑、可检索的文本信息一直是一个技术挑战。

### 2. 方法概述

本方法结合了计算机视觉与自然语言处理技术，首先通过视觉模型识别文档中的版面结构，再利用语言模型对识别出的文本块进行语义理解与重组。

- 步骤一：版面分析
- 步骤二：文本识别
- 步骤三：结构重组

| 方法 | 准确率 | 速度 |
|------|--------|------|
| 传统OCR | 85% | 慢 |
| 本方法 | 97% | 快 |

> 高效解析是智能文档处理的核心。

![](img/202cface8244f523c2641baa2e00d7dd_290_0.png)

### 1.1 认识人工智能

人工智能（Artificial Intelligence，简称AI）是研究、开发用于模拟、延伸和扩展人的智能的理论、方法、技术及应用系统的一门新的技术科学。人工智能是计算机科学的一个分支，它企图了解智能的实质，并生产出一种新的能以人类智能相似的方式做出反应的智能机器，该领域的研究包括机器人、语言识别、图像识别、自然语言处理和专家系统等。

人工智能从诞生以来，理论和技术日益成熟，应用领域也不断扩大，可以设想，未来人工智能带来的科技产品，将会是人类智慧的“容器”。人工智能可以对人的意识、思维的信息过程的模拟。人工智能不是人的智能，但能像人那样思考、也可能超过人的智能。

人工智能是包括十分广泛的科学，它由不同的领域组成，如机器学习，计算机视觉等等，总的说来，人工智能研究的一个主要目标是使机器能够胜任一些通常需要人类智能才能完成的复杂工作。

![](img/202cface8244f523c2641baa2e00d7dd_291_0.png)

图1-1 人工智能示意图

```cpp
#include <iostream>
using namespace std;

const int PRICE;
const long YEARS;
const double YIELD;
int main()
{
    int bondtype;
    double interest, coupon;
    .
    .
    .
    return 0;
}
double roi(int mat1, int mat2)
{
    int count;
    double effectiveRate;
    .
    .
    .
    return effectiveRate;
}
int step(double first, double last)
{
    int numofyrs;
    double fracpart;
    .
    .
    .
    return(10*numofyrs);
}
```

- b. Draw a box around the appropriate section of the preceding code to enclose the scope of each variable or constant.
- c. Determine the data type of the arguments that the `roi()` and `step()` functions expect and the data type of the value these functions return.

2. (Practice) a. For the following section of code, determine the data type and scope of all declared variables on a separate sheet of paper, using the column headings shown in the following chart. (The entries for the first variable have been filled in.)

| Variable Name | Data Type | Scope |
|---|---|---|
| key | char | global to `main()`, `func1()`, and `func2()` |

4. (Practice) Define the scope of the parameter p2 and the variables a, b, c, d, e, f, m, n, p, q, and z in the following program structure:

```cpp
#include <iostream>
using namespace std;

int a, b;
double One(float);
void Two(void);

int main()
{
    int c, d;
    double e, f;
    .
    .
    return 0;
}

double One(double p2)
{
    char m, n;
    .
    .
}

void Two(void)
{
    int p, d;
    double q, z;
    .
    .
}
```

5. (Desk check) Determine the values displayed by each cout statement in the following program:

```cpp
#include <iostream>
using namespace std;

int firstnum = 10;  // declare and initialize a global variable
void display();     // function prototype

int main()
{
    int firstnum = 20;  // declare and initialize a local variable

    cout << "\nThe value of firstnum is " << firstnum << endl;
    display();

    return 0;
}

void display(void)
{
    cout << "The value of firstnum is now " << firstnum << endl;

    return;
}
```

## 6.5 Variable Storage Category

The scope of a variable defines the location in a program where that variable can be used. If you draw a box around the section of program code where each variable is valid, the space inside the box represents the variable’s scope. From this viewpoint, a variable’s scope can be thought of as the space in the program where the variable is valid.

In addition to the space dimension represented by scope, variables have a time dimension that refers to the length of time storage locations are reserved for a variable. This time dimension is referred to as the variable’s “lifetime.” For example, all variable storage locations are released back to the operating system when a program is finished running. However, while a program is still running, interim variable storage locations are reserved and subsequently released back to the operating system. Where and how long a variable’s storage locations are kept before they’re released can be determined by the variable’s storage category.

The four available storage categories are auto, static, extern, and register. If one of these categories is used, it must be placed before the variable’s data type in a declaration statement. The following are examples of declaration statements that include a storage category designation:

```cpp
auto int num;      // auto storage category and int data type
static int miles;  // static storage category and int data type
register int dist; // register storage category and int data type
extern int volts;  // extern storage category and int data type
auto float coupon; // auto storage category and float data type
static double yrs; // static storage category and double data type
extern float yd;   // extern storage category and float data type
auto char inKey;   // auto storage category and char variable
```

To understand what a variable’s storage category means, next you examine local variables (created inside a function) and global variables (created outside a function).

## Local Variable Storage Categories

Local variables can be members only of the auto, static, or register storage categories. If no category description is included in the declaration statement, the variable is assigned to the auto category automatically, so auto is the default category C++ uses. All the local variables you have used have been auto variables because the storage category designation was omitted.

The term auto is short for "automatic." Storage for auto local variables is reserved or created automatically each time a function declaring auto variables is called. As long as the function hasn't returned control to its calling function, all auto variables local to the function are "alive"—meaning storage for the variables is available. When the function returns control to its calling function, its local auto variables "die"—meaning storage for the variables is released back to the operating system. This process repeats each time a function is called. For example, in Program 6.13, the testauto() function is called three times from main().

### Program 6.13

```cpp
#include <iostream>
using namespace std;

void testauto(); // function prototype

int main()
{
    int count;      // count is a local auto variable

    for(count = 1; count <= 3; count++)
        testauto();

    return 0;
}

void testauto()
{
    int num = 0;    // num is a local auto variable
                    // initialized to zero
    cout << "The value of the automatic variable num is "
         << num << endl;
    num++;

    return;
}
```

## Modularity Using Functions

This is the output produced by Program 6.13:

```
The value of the automatic variable num is 0
The value of the automatic variable num is 0
The value of the automatic variable num is 0
```

Each time `testauto()` is called, the auto variable `num` is created and initialized to 0. When the function returns control to `main()`, the variable `num` is destroyed along with any value stored in `num`. Therefore, the effect of incrementing `num` in `testauto()`, before the function’s return statement, is lost when control is returned to `main()`.

For most applications, the use of auto variables works just fine and is the reason it’s the default storage category. In some cases, however, you want a function to remember values between function calls, which is the purpose of the static storage category. A local variable declared as static causes the program to keep the variable and its latest value even when the function that declared it has finished executing. The following are examples of static variable declarations:

```cpp
static int rate;
static double amount;
static char inKey;
```

A local static variable isn’t created and destroyed each time the function declaring it is called. After they’re created, local static variables remain in existence for the program’s lifetime. This means the last value stored in the variable when the function finishes executing is available to the function the next time it’s called.

Because local static variables retain their values, they aren’t initialized in a declaration statement in the same way as auto variables. To understand why, consider the auto declaration `int num = 0;`, which causes the auto variable `num` to be created and set to 0 each time the declaration is encountered. This procedure is called a **runtime initialization** because initialization occurs each time the declaration statement is encountered. This type of initialization would be disastrous for a static variable because resetting the variable’s value to 0 each time the function is called destroys the very value you’re trying to save.

Initialization of static variables (both local and global) is done only once, when the program is first compiled. At compile time, the variable is created and any initialization value is placed in it.¹⁶ Thereafter, the value in the variable is kept without further initialization. To see how this process works, examine Program 6.14.
