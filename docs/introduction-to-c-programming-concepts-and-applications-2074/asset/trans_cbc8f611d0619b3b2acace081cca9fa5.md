

# // 构建一个库

如果你要有一个库，你会想要一个命名空间——名称和双冒号，你必须在某些命令中放入——帮助你将库中的函数与其它函数区分开来。

在主函数中，你可以通过编写 english::greeting() (14) 来调用问候函数。这意味着你可以调用 english 命名空间内的名为 greeting 的函数。当它被调用时，会打印出 Hello!。

头文件将包含命名空间、要在该库或命名空间中定义的任何变量，以及函数声明——它们只是头文件的一部分，不包括大括号。

你应该熟悉你在每个程序开头都写上的 using namespace std，这使你能够在所有内容前面使用标准命名空间 std:: 中的命令。

就像 iostream 等库提供有用的函数一样，你也可以以类似的方式创建自己的库。当你创建自己的库时，你会希望将所有新函数放在单独的命名空间中，以防止不同函数的命名重叠。

声明是一种说“将会有具有此签名的函数”的方式，而不是实际说明函数是如何实现的。实际实现是定义。

命名空间是一种帮助区分一个库的函数与另一个库的方法。这样，如果你有一个名为 get_data 的函数，那么另一个库也可以有一个名为 get_data 的函数。它们可以位于不同的命名空间中，并且这两个函数保持独立。

当你分离库并且想要编写非常大的程序时——这些程序是由团队人员构建的或一个人长期工作——你可以开始使用一个称为单独编译的功能。

到目前为止，你一直将定义与声明放在一起，这在单个文件中很常见。但类似头文件的和类似体的定义可以拆分。如果你想尝试这样做，你可能需要使用 Visual Studio 或 Xcode 等 IDE，而不是基于浏览器的在线编译器。参见第 172 页，了解如何在你的环境中分离源文件和头文件的说明。

你也可以创建自己的命名空间。为此，你使用关键字 namespace 然后是你想要为命名空间使用的名称；然后，在大括号中，你包含将成为该命名空间一部分的所有声明。

假设你想要创建一个函数库。C 和 C++ 中的常见做法是将这些代码拆分为两个文件：头文件和源文件。头文件具有 .h 或有时是 .hpp 文件扩展名，而源文件具有一个

```
// Program 15_3
// Namespace example
#include <iostream>
using namespace std;
namespace english {
void greeting() {
    cout << "Hello!" << endl;
}
}
int main() {
    english::greeting();
}
```

例如，在 Program 15_3 中，你有一个名为 english 的命名空间 (1)。在大括号内，你定义了一个名为 greeting (m) 的函数类型。此函数是作为命名空间的一部分定义的。

Lecture 15 | Functions in Top-Down and Bottom-Up

在设计你的程序时，使用伪代码来查看你的函数，查看所有函数并搜索你想要重用代码的地方。或者一个文件可能在同一位置包含太多想法。这两者都是考虑将函数拆分为单独文件的良好时机。

- 将函数跨文件划分有助于确保没有单个文件过大，并且文件中的所有内容密切相关。
- 通过单独编译文件，只有被重新编译的文件。在大型项目中，这可以大大提高生产力。

单独编译之所以有用，尤其对于较大任务，有很多原因。

- 它使在其他程序中重用文件变得更容易；你只需编写一次代码，然后在其他程序中 #include 它。

事实上，你可以单独编译你编写的每个函数。但对于初学者来说，这会使代码更难处理，并且你将无法从基于浏览器的开发环境中执行代码。经验法则是当你可能重用代码或简化文件时考虑分离。🔸

## 如何在你的 IDE 中创建单独的源文件和头文件

在 Visual Studio 中，你创建的单独文件不会自动放入你的项目中，因此在准备编译它们时，你必须将文件添加到项目中。要将单独的文件添加到项目中：

- 保存文件。
- 转到项目窗口并选择“add” 和 “existing item”。
- 将所有 3 个文件添加到项目中：
- 包含 main 的源文件
- 包含函数头的头文件
- 包含函数定义的源文件
- 然后，你可以构建项目：运行它。

## READINGS

- Stroustrup, Programming Principles and Practice Using C++, 8.7 for (namespaces).
- Lippman, Lajo, and Moo, C++ Primer, section 18.2 (for namespaces).
- Csterhouse, A Philosophy of Software Design, chap. 4 (describing design) and chap. 5 (describing information hiding).
- See references from lecture 11: Problem Solving and Program Design in C (8th ed.) by Jeri R. Hanly and Elliott B. Koffman and Problem Solving, Abstract, and Design Using C++ (6th ed.) by Frank Lied and Elliott B. Koffman.

Xcode 会自动将文件放入项目中。

- 从 main.cpp 文件开始，main 会自动重复。
- 转到 File 菜单并创建一个 Header File。
- 将其保存为 .h。
- 将其保存为 C++ 文件，.cpp。
- 如果你先创建 .cpp 源文件，Xcode 会给你自动创建头文件的选项。
- 构建并运行程序。

# // QUIZ

1 Match the idea to its name:

2 Imagine you have the following program and want to break it into several files, which will be compiled separately. Specifically, you would like to have: a library header file, a library implementation file, and a main file. Which of the code would end up in each of these files?

- a top-down
b bottom-up
c separate compilation
d stub
namespace
affold

1 a way of building a program by combining existing, simpler parts

2 a way of writing a minimal function that it can be called when testing some other code

```
#include <iostream>
using namespace std;
bool update_balance(float& balance, float payment, float interest) {
    balance -= payment;
    if (balance <= 0) {
        return true;
    }
    balance *= (1.0+interest/100.0);
    return false;
}
int main() {
    float account_balance=1000.0;
    float payment = 50.0;
    float interest_rate = 3.5;
    int numpments = 1;
    while (update_balance(account_balance,payment,interest_rate)) {
        numpments++;
        payment += 10.0;
    }
    cout << "It takes " << numpments << " increasing payments to pay the balance in the account." << endl;
}
```

3 a way of setting up code so that a particular function can be tested

4 a way of grouping functions and variables with a common purpose

5 a way of dividing a program into multiple files

6 a way of dividing a problem into simpler subproblems

# // QUIZ ANSWERS

- 1 Separate compilation means that functions can be placed in separate files that are compiled separately. In this case, that means that there will be the following:

- b 1

>> a header file, containing the function header:

```
bool update_balance(float& balance, float payment, float interest)
```

>> an implementation file, containing the function definition:

```
bool update_balance(float& balance, float payment, float interest) {
balance -= payment;
if (balance <= 0) {
    return true;
}
balance *= (1.0+interest/100.0);
return false;
}
```

>> a main file that would include the main program (it must also #include the library header file):

```
int main() {
    float account_balance=1000.0;
    float payment = 50.0;
    float interest_rate = 3.5;
    int numpayment = 1;
    while(update_balance(account_balance,payment,interest_rate)) {
        numpayment++;
        payment += 10.0;
    }
    cout << "It takes " << numpayment << " increasing payments to pay the balance in the account." << endl;
}
```

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_179_0.png)

