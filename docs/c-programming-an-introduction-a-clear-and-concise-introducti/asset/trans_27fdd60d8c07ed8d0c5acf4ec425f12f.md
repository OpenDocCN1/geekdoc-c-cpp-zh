
```cpp
void addFive(int &num)
{
    num += 5;
}
```

有些程序员建议将与符号放在数据类型旁边，而不是参数旁边，但编译器两种风格都能接受。

只有当没有其他方法可以完成特定任务时，才应该按引用传递参数。例如，上面的 addFive() 函数完全可以用一个值参数来编写，向调用程序返回参数加 5 的结果，这样，作为参数传入的变量就可以被赋值为函数的返回值。或者用更清晰的代码来表示：

```cpp
int addFive(int num)
{
    return num += 5;
}

// in calling program
int number = 0;
number = addFive(number);
```

然而，有些情况下只有按引用传递参数才行，swap() 函数就是其中之一。我们必须使用引用参数来编写该函数的主要原因在于，一个返回值的函数只能返回一个值，而 swap() 函数要处理的是两个值。

话不多说，让我们重写 swap 函数，使其能正确工作：

```cpp
void swap(string &word1, string &word2)
{
    string temp = word1;
    word1 = word2;
    word2 = temp;
}
```

现在 word1 和 word2 是按引用传递的，因此当函数改变这些变量的值时，它实际上是在调用程序中以及函数内真正地改变它们。下面是完整的程序：

```cpp
// Swap.cpp : main project file.

#include "stdafx.h"

using namespace System;

#include <iostream>
#include <string>
using namespace std;

void swap(string &word1, string &word2)
{
    string temp = word1;
    word1 = word2;
    word2 = temp;
}

int main(array<System::String ^> ^args)
{
    string word1, word2;
    word1 = "banana";
    word2 = "apple";
    cout << word1 << " " << word2 << endl;
    swap(word1, word2);
    cout << word1 << " " << word2 << endl;
    Console::ReadKey();
    return 0;
}
```

输出如下：

```
banana apple
apple banana
```

存储在各个内存地址中的值现在已经被交换，因此 word1 存储的是 "apple" 而 word2 存储的是 "banana"。

## 变量作用域

变量的作用域指的是变量的可访问性。变量在何处以及如何可访问，取决于变量在何处声明。最好通过示例来解释变量作用域的工作方式。请看下面这个简单的程序片段：

```cpp
int main()
{
    int number1;
    number1 = 23;
    int number2 = number1 * 13;
    return 0;
}
```

变量 number1 的作用域是 main() 函数。main() 函数块内的任何代码都可以访问 number1 的值。接下来再看一个更长的代码片段：

```cpp
int changeNumber(int number)
{
    return number *= 3;
}

int main()
{
    int number = 3;
    cout << changeNumber(number);
    cout << number;
    return 0;
}
```

参数 number 被称为 changeNumber() 函数的局部变量。这意味着该变量只能被函数定义内的代码访问，并且一旦函数停止执行，它的值就会从内存中完全移除。

为了演示这一点，让我们重写上面的程序来展示局部作用域是如何工作的。完整程序如下：

```cpp
// ScopeExample.cpp : main project file.

#include "stdafx.h"

using namespace System;
#include <iostream>
using namespace std;

int changeNumber(int number)
{
    number *= 3;
    cout << "The value of number in the changeNumber()"
         << " function is: " << number << endl;
```

## 作用域级别

上面的示例说明了 C++ 程序中可用的作用域级别之一。这些作用域级别包括：

- *全局*
- *局部*
- *块*

在函数（无论是 main 函数还是用户自定义函数）内声明的变量具有局部作用域。该变量及其值可被定义该函数的块内的任何代码访问。其他函数中的代码无法访问该变量。

## 全局作用域

如果变量定义在 C++ 程序的全局区域中，则该变量具有全局作用域。这个区域是定义函数的区域，包括 main() 函数上方和下方的区域。在此区域中定义的变量称为*全局变量*，可以被程序中的任何代码访问。

让我们看一个关于全局变量如何工作的简单示例：

```cpp
// GlobalScope.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int number = 1; // global variable

int changeNumber()
{
    number += 5;
    return number;
}

int main(array<System::String ^> ^args)
{
    cout << "The value of number is: " << number
         << endl;
    number = changeNumber();
    cout << "Now the value of number is: "
         << number << endl;
    Console::ReadKey();
    return 0;
}
```

变量 number 是一个全局变量。即使该变量没有作为参数传递给 changeNumber() 函数，该函数也可以访问 number 的值。同样，尽管 number 没有在 main() 函数中声明，main() 函数也可以访问 number 的值。

如上所述，全局变量可以被程序中定义的任何代码访问。因此你可能会认为，应该将所有变量都声明为全局变量，以便于使用。然而，这是错误的想法。在程序中使用全局变量会带来很多问题。这些问题包括：

- 意外修改 —— 你可能会在某一个函数中意外地修改一个全局变量，却以为它在另一个函数中未发生变化。
- 无法复用代码 —— 大量使用全局变量会让代码变得更加僵化，使代码无法在其他程序中使用。
- 难以管理模块化 —— 大量使用全局变量的代码不如使用更多局部变量的代码具有模块性。

最好的建议是：一开始将变量声明为局部变量，只有在绝对必要时才将它们改为全局变量。在本书后面，我们将讨论使用全局变量更有优势的情况。

## 局部作用域

我们已经讨论过如何创建具有*局部作用域*的变量，这里只回顾一下这个概念。在函数体内（包括 main() 函数）声明的变量被视为具有局部作用域。局部作用域变量的生命周期与函数的生命周期一致，并且该函数体内定义的任何代码都可以访问该变量。

## 块作用域

具有*块作用域*的变量只能被该变量所在块内的代码访问。这似乎有些令人困惑，因为局部变量通常定义在一个块中，但很多时候会在另一个代码块内部存在一个代码块。

请看下面这个简单的 for 循环：

```cpp
// BlockScope.cpp : main project file.
#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    for(int i = 1; i <= 10; ++i)
    {
        cout << "The value of i in the loop is: "
             << i << endl;
    }
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

```
The value of i in the loop is: 1
The value of i in the loop is: 2
The value of i in the loop is: 3
The value of i in the loop is: 4
The value of i in the loop is: 5
The value of i in the loop is: 6
The value of i in the loop is: 7
The value of i in the loop is: 8
The value of i in the loop is: 9
The value of i in the loop is: 10
```

现在，让我们通过在循环的右花括号之后添加下面这一行，来检查循环外 i 的值：

```cpp
cout << "The value of i outside the loop is: " << i
     << endl;
```

现在编译这个程序。你会发现编译无法通过，因为有一个错误。错误信息指出 i 是未声明的标识符。这是因为 i 是在 for 循环的块内声明的，具有块作用域。换句话说，i 及其值只能在 for 循环的块内被访问，一旦 for 循环结束，变量 i 就会从内存中移除。

你可以将块级作用域用于任何类型的块。虽然我们还没有讨论这一点，但你可以在程序的任何位置放置一个代码块。请看下面的程序：

```cpp
// BlockScope.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number = 1;
    cout << "The value of number is: " << number
         << endl;
    {
        int number = 100;
        cout << "The value of number in this block"
             << " is: " << number << endl;
    }
    number += 4;
    cout << "The value of number is: " << number << endl;
    Console::ReadKey();
    return 0;
}
```

