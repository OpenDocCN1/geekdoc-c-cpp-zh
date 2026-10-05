

# 异常处理基础

# 陷阱：（续）

按照这种第二种顺序，类型为 `NegativeNumber` 的异常（抛出的值）将如所愿地被 `NegativeNumber` catch 块捕获。然而，如果抛出一个 `DivideByZero` 类型的值，它可能会被以 `catch(...)` 开头的块捕获。因此，`DivideByZero` catch 块将永远无法到达。幸运的是，大多数编译器都会提示你犯了此类错误。

# 提示：异常类可以是平凡的

在接下来，我们复制了显示 18.4 中 `DivideByZero` 异常类的定义：

```cpp
class DivideByZero
{};
```

该异常类没有成员变量，也没有成员函数（默认构造函数除外）。它除了名称外一无所有，但这已经足够了。抛出 `DivideByZero` 类的对象可以激活相应的 catch 块，正如显示 18.4 所示。

在使用平凡异常类时，一旦控制权转移到 catch 块，你通常不需要对异常（抛出的值）做任何事情。异常只是被用来引导你进入 catch 块。因此，你可以省略 catch 块参数。事实上，在任何不需要它的时候，你都可以省略 catch 块参数，无论异常是否为平凡。

# 在函数中抛出异常

有时，延迟处理异常是有意义的。例如，你可能有一个函数，其代码在尝试除以零时会抛出异常，但你可能不想在该函数中捕获该异常。也许某些程序希望函数在抛出异常时直接结束，而其他程序则使用该函数执行其他操作。因此，如果你在函数内部捕获异常，你将不知道如何处理它。在这些情况下，不在函数定义中捕获异常是有意义的，而是让使用该函数的程序（或其他代码）将调用放在 `try` 块中，并在随后的 `catch` 块中捕获异常。

看显示 18.5 中的程序。它有一个 try 块，但 try 块中可见的 `throw` 语句。该程序中执行抛出操作的语句是

```cpp
if (bottom == 0)
    throw DivideByZero( );
```

# 第18 章 异常处理

显示 18.5 在函数内部抛出异常（2 部分中的第 1 部分）

```cpp
#include <iostream>
#include <cstdlib>
using std::cin;
using std::cout;
using std::endl;
```

```cpp
class DivideByZero {
};
```

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero);
```

```cpp
int main() {
    int numerator;
    int denominator;
    double quotient;
    cout << "Enter numerator:\n";
    cin >> numerator;
    cout << "Enter denominator:\n";
    cin >> denominator;
```

```cpp
try {
    quotient = safeDivide(numerator, denominator);
} catch (DivideByZero) {
    cout << "Error: Division by zero!\n";
    cout << "Program aborting.\n";
    exit(0);
}
```

```cpp
cout << numerator << " /" << denominator
    << " = " << quotient << endl;
```

```cpp
cout << "End of program.\n";
    return 0;
}
```

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero) {
    if (bottom == 0) {
        throw DivideByZero();
    }
    return top / static_cast<double>(bottom);
}
```

# 异常处理基础 843

显示 18.5 在函数内部抛出异常（2 部分中的第 2 部分）

示例对话 1

```
Enter numerator:
5
Enter denominator:
10
5/10 = 0.5
End of Program.
```

示例对话 2

```
Enter numerator:
5
Enter denominator:
0
Error: Division by zero:
Program aborting.
```

该语句在 try 块中不可见。但在程序执行方面它是 try 块的一部分，因为它是 `safeDivide` 的定义，并且 try 块中有一个 `safeDivide` 的调用。`throw (DivideByZero)` 的意义将在节讨论。

# 异常规范

如果函数不能捕获异常，它至少应该警告程序员任何调用可能会抛出异常。如果有可能抛出但未被捕获的异常，这些异常应该列在异常规范中，如显示 18.5 所示：

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero);
```

如显示 18.5 所示，异常规范应该出现在函数声明和函数定义中。如果一个函数有多个函数声明，那么所有函数声明必须具有相同的规范。函数的异常规范也称为抛出列表（throw list）。

如果在函数定义中可以抛出多个异常，异常类型之间用逗号分隔，如下所示：

```cpp
void someFunction() throw (DivideByZero, OtherException);
```

# 第18 章 异常处理

规范中列出的所有异常类型都将被正常处理。当我们说异常被正常处理时，我们的意思是它像在本节之前描述的那样被处理。特别是，异常被正常处理，你可以省略 catch 块参数。如果有可能抛出但未被捕获的异常，这些异常应该列在异常规范中，如显示 18.5 中的函数声明所示：

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero);
```

如显示 18.5 所示，异常规范应该出现在函数声明和函数定义中。如果一个函数有多个函数声明，那么所有函数声明必须具有相同的规范。函数的异常规范也称为抛出列表。

如果在函数定义中可以抛出多个异常，异常类型之间用逗号分隔，如下所示：

```cpp
void someFunction() throw (DivideByZero, OtherException);
```

# 异常处理基础 845

```cpp
void someFunction() throw ( );
//空列表，所以所有异常都会调用 unexpected().
```

```cpp
void someFunction();
//
类型的
不
在函数内部。
```

是

空异常异常：

```cpp
someFunction() throw (DivideByZero,
OtherException);
// 类型被正常处理。
```

如显示 18.5 所示，异常规范应该出现在函数声明和函数定义中。如果一个函数有多个函数声明，那么所有函数声明必须具有相同的规范。函数的异常规范也称为抛出列表。

如果在函数定义中可以抛出多个异常，异常类型之间用逗号分隔，如下所示：

```cpp
void someFunction() throw (DivideByZero, OtherException);
```

规范中列出的所有异常类型都将被正常处理。当我们说异常被正常处理时，我们的意思是它像在本节之前描述的那样被处理。特别是，异常被正常处理，你可以省略 catch 块参数。

如果有可能抛出但未被捕获的异常，这些异常应该列在异常规范中，如显示 18.5 中的函数声明所示：

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero);
```

>这在所有语言中都不适用。

异常规范应该出现在函数声明和函数定义中。如果一个函数有多个函数声明，那么所有函数声明必须具有相同的规范。函数的异常规范也称为抛出列表。

如果在函数定义中可以抛出多个异常，异常类型之间用逗号分隔，如下所示：

```cpp
void someFunction() throw (DivideByZero, OtherException);
```

