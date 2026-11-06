

## 创建更易读且简洁的 C++ 代码

使用 C++ 的优势之一是你可以创建简洁且易于阅读的代码。由于你可以一眼看到更多代码，C++ 通常也更容易理解，因为你无需滚动编辑器页面即可查看某个问题的完整解决方案。然而，在早期版本的 C++ 中，某些类型的问题确实需要相当冗长的解决方案。从 C++ 11 开始，开发者掌握了一种新技术，可以以让 C++ 代码回归简洁本源的方式解决这些问题。

你可以使用 lambda 表达式解决许多 C++ 开发问题，但典型的问题是如何让代码更简洁、更易读。清单 7-1 中展示的 Problem 示例完全没有任何问题——按原样运行良好。

### 清单 7-1：定义由 lambda 表达式解决的问题

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

class MyFunctor
{
public:
    void operator()(int x)
    {
        cout << x << endl;
    }
};

void ProcessVector(vector<int>& vect)
{
    MyFunctor Func;
    for_each(vect.begin(), vect.end(), Func);
}

int main()
{
    vector<int> MyVector;
    MyVector.push_back(1);
    MyVector.push_back(2);
    MyVector.push_back(3);
    MyVector.push_back(4);

    ProcessVector(MyVector);
}
```

在本例中，示例创建了一个 vector（MyVector）并用数据填充它，然后调用 ProcessVector() 来使用 vector 中的数据执行任务。

对 ProcessVector() 的调用创建了一个名为 Func 的函数对象（functor）——一种行为类似于函数的特殊类。这是一种极其有用的类，你将在第 VI 卷第 1 章的“函数对象”一节中进一步探讨。目前，你只需要知道它是一种行为类似于函数的特殊类。

for_each() 算法（在第 VI 卷第 5 章的“使用 Foreach 创建改进的循环”一节中完整演示）是标准库的一部分。它使用 Func 处理 vect（即传递给 ProcessVector() 的 vector）中的每个元素，从第一个元素（由 vect.begin() 定义）开始，到最后一个元素（由 vect.end() 定义）结束。

查看 MyFunctor 时，你会看到一个 operator 的定义，它要求一个 int 输入 x。代码所做的只是将 x 输出到控制台。因此，你会看到此示例的以下输出。

```
1
2
3
4
```

## 定义基本的 lambda 表达式

lambda 表达式的目的是让代码更短、更易读。它创造了一种呈现代码的新方法。然而，它并没有真正创造新的 C++ 能力。你实际上是使用同样的技术，但方式与之前不同。以下各节将帮助你创建第一个 lambda 表达式，让你更清楚地了解它们的具体工作方式。

### 定义 lambda 表达式的组成部分

上一节中的示例完全可以使用。然而，函数对象在示例中只使用了一次。这种情况相对常见，并且会给需要阅读最终代码的开发者造成困惑。lambda 表达式可以将函数对象合并到 for_each() 算法中，如清单 7-2 中的解决方案示例所示。

第 IV 卷
第 7 章
使用
Lambda 表达式

### 清单 7-2：定义 lambda 表达式解决方案

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

void ProcessVector(vector<int>& vect)
{
    for_each(vect.begin(), vect.end(), [](int x){cout << x << endl;});
}

int main()
{
    vector<int> MyVector;
    MyVector.push_back(1);
    MyVector.push_back(2);
    MyVector.push_back(3);
    MyVector.push_back(4);

    ProcessVector(MyVector);
}
```

如你所见，使用 lambda 版本的示例更短且更容易理解，因为不再需要单独的类来处理 `for_each()` 算法中的数据。lambda 表达式始终如下所示：

```cpp
[](int x){cout << x << endl;}
```

![](img/6ba99460b0feb3585671a4612ff5fabb_619_0.png)

那对方括号（`[]`），后面跟着括号中的任何输入参数，必须始终位于 lambda 表达式的开头；你要执行的代码——放在一对花括号（`{}`）中——总是位于末尾。与任何函数一样，lambda 表达式可以接受多个输入变量并提供返回值。开头的方括号称为*捕获子句*，你将在本章后面看到它的使用。lambda 表达式可以包含其他功能——包括本章“使用 lambda 表达式开发”一节中演示的功能——但每个 lambda 表达式都包含以下三个要素：

- 方括号中的捕获子句
- 括号中的参数列表
- 花括号中的可执行代码

### 依赖编译器推断返回类型

lambda 表达式可以直接处理信息并呈现，或作为返回类型的一部分提供信息。简单的 lambda 表达式可以在不告知编译器太多信息的情况下返回信息，因为编译器可以自动推断返回类型。清单 7-3 中的 `ReturnType01` 示例演示了如何实现一个返回由编译器自动检测的数据的 lambda 表达式。

### 清单 7-3：使用编译器自动推断返回类型

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

void ProcessVector(vector<int>& vect)
{
    vector<bool> Result;
    Result.resize(vect.size());

    transform(vect.begin(), vect.end(), Result.begin(),
              [](int x) { return x > 3; });

    cout.setf(ios::boolalpha);
    for_each(Result.begin(), Result.end(),
             [](bool x) { cout << x << endl; });
}

int main()
{
    vector<int> MyVector;
    MyVector.push_back(1);
    MyVector.push_back(2);
    MyVector.push_back(3);
    MyVector.push_back(4);

    ProcessVector(MyVector);
}
```

与前面的示例一样，本例（以及后面的大多数示例）创建了一个名为 `MyVector` 的 `vector<int>`，向其中填充信息，并将其传递给 `ProcessVector()`。`ProcessVector()` 将数据作为 `vect` 接收，并一次处理一个元素。

`ProcessVector()` 首先创建一个名为 `Result` 的 `vector<bool>`，用于接收数据处理的结果。在本例中，处理发生在 `transform()` 函数中，该函数接收 `vect` 的开始和结束位置，以及 `Result` 的开始位置和一个 lambda 表达式。为了使 `transform()` 正常工作，lambda 表达式必须返回一个值，该值精确定义转换过程的工作方式。在本例中，该过程是将输入值 `x` 与数字 3 进行简单比较。

当 transform() 完成时，Result 包含一个 bool 值列表，指示 vect 中的各个数字是否大于 3。要以 true 或 false 文本输出的形式查看这些值，而不是数字，你需要调用 cout.setf(ios::boolalpha)。然后，代码使用 for_each() 循环来显示 Result 中的各个值。运行此示例时，你会看到以下输出。

```
false
false
false
true
```

鉴于 vect 中的输入值为 1、2、3 和 4，vect 的最后一个元素 4 确实大于数字 3。如图所示，将 transform() 与 lambda 表达式结合使用，是减少执行各种批量比较（以及其他特定的转换任务）所需代码的绝佳方式。

### 使用特定的返回类型

有时，lambda 表达式足够复杂，编译器无法确定要使用的返回类型。发生这种情况时，你通常会在编译过程中看到错误消息。幸运的是，只需告诉编译器需要哪种返回类型，就可以轻松解决此问题。清单 7-4 中显示的 `ReturnType02` 示例演示了如何执行此任务。

### 清单 7-4：使用特定的返回类型

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

void ProcessVector(vector<int>& vect)
{
    vector<bool> Result;
    Result.resize(vect.size());

    transform(vect.begin(), vect.end(), Result.begin(),
              [](int x)->bool{return x > 3;});

    cout.setf(ios::boolalpha);
    for_each(Result.begin(), Result.end(),
             [](bool x){cout << x << endl;});
}
```

