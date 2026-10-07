

# 列表 15.8 error2.cpp

```
//error2.cpp -- returning an error code
#include <iostream>
#include <cfloat> // (or float.h) for DBL_MAX

bool hmean(double a, double b, double * ans);

int main() {
    double x, y, z;

    std::cout << "Enter two numbers: ";
    while (std::cin >> x >> y) {
        if (hmean(x,y,z)) {
            std::cout << "Harmonic mean of " << x << " and " << y << " is " << z << std::endl;
        } else {
            std::cout << "One value should not be the negative "
                << "of the other - try again.\n";
            std::cout << "Enter next set of numbers <q to quit>: ";
        }
    }
    std::cout << "Bye!\n";
    return 0;
}

bool hmean(double a, double b, double * ans) {
    if (a == -b) {
        *ans = DBL_MAX;
        return false;
    } else {
        *ans = 2.0 * a * b / (a + b);
        return true;
    }
}
```

这里是列表 15.8 中程序的示例运行结果：

```
Enter two numbers: 3 6
Harmonic mean of 3 and 6 is 4
Enter next set of numbers <q to quit>: 10 -10
One value should not be the negative of the other - try again.
Enter next set of numbers <q to quit>: 1 19
Harmonic mean of 1 and 19 is 1.9
Enter next set of numbers <q to quit>: q
Bye!
```

## 第 15 章 朋友、异常及更多

在列表 15.8 中，程序设计允许用户继续操作，从而绕过错误输入的影响。当然，这种设计依赖于用户去检查函数的返回值，而程序员并不总是这样做。例如，为了保持示例程序的简短，书中的列表没有检查 `cout` 是否成功处理了输出。

你可以对第三个参数使用指针或引用。许多程序员更倾向于对内置类型使用指针，因为这样可以明显看出哪个参数被用于存储结果。

另一种将返回条件存储在某处的变体是使用全局变量，当出现问题时赋予一个特定值，调用程序可以检查该变量。这是传统 C 库使用的方法，它使用全局变量 `errno` 来实现此目的。当然，你必须确保没有其他函数尝试为了其他目的使用同名的全局变量。

## 异常机制

现在让我们看看如何通过使用异常机制来处理问题。C++ 异常是对程序运行时出现的特殊情况的响应，例如尝试除以零。异常提供了一种从程序一个部分转移控制到另一个部分的方法。处理异常包含三个组成部分：

- *抛出异常 (Throwing)*
- 使用处理器捕获异常 (Catching)
- 使用 try 块 (try block)

当出现问题时，程序会抛出异常。例如，你可以修改列表 15.7 中的 `hmean()`，使其抛出异常而不是调用 `abort()` 函数。本质上，`throw` 语句是一个跳转；也就是说它告诉程序跳转到另一个位置的语句。`throw` 关键字表示抛出异常。其后跟着一个值（如字符串或对象），表示异常的性质。

程序在想要处理异常的地点通过异常处理器捕获异常。`catch` 关键字表示捕获异常。处理器以 `catch` 关键字开头，后面跟着一个括号内的类型声明，表示它响应的异常类型。随后是一个大括号括围的代码块，表示要采取的行动。`catch` 关键字结合异常类型充当标签，标识当抛出异常时执行跳转的点。异常处理器也称为 catch 块。

try 块标识了一个可能会激活特定异常的代码块。它后面跟着一个或多个 catch 块。try 块由 `try` 关键字指示，后跟着一个大括号块，表示用于检测异常的代码。

观察这三个元素如何组合的最简单方法是看一个短示例，例如列表 15.9 中的示例。

### 列表 15.9 error3.cpp

```
// error3.cpp -- using an exception
#include <iostream>
double hmean(double a, double b);

int main() {
    double x, y, z;

    std::cout << "Enter two numbers: ";
    while (std::cin >> x >> y) {
        try { // start of try block
            z = hmean(x,y); // end of try block
        } catch (const char * s) { // start of exception handler
            std::cout << s << std::endl;
            std::cout << "Enter a new pair of numbers: ";
            continue; // end of handler
        }
        std::cout << "Harmonic mean of " << x << " and " << y << " is " << z << std::endl;
        std::cout << "Enter next set of numbers <q to quit>: ";
    }
    std::cout << "Bye!\n";
    return 0;
}

bool hmean(double a, double b) {
    if (a == -b) {
        throw "One value should not be the negative of the other";
    }
    return 2.0 * a * b / (a + b);
}
```

