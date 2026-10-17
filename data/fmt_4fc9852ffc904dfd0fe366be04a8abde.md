
`cout << e << " donuts, and No Milk!\n"`

`cout << "Go buy some milk.\n";`

```
```

当一个值被抛出时，抛出的值必须是 `int` 类型，以便此特定块生效。在显示 16.2 中，抛出的值由变量 `donuts` 提供，由于 `donuts` 是 `int` 类型，因此此 `catch` 块可以捕获抛出的值。

假设 `milk` 的值为 12，对应显示 16.2 中的第二个示例对话。由于 `milk` 的值不是正数，`if` 语句中的 `throw` 语句被执行。在这种情况下，抛出了 `donuts` 的值。当显示 16.2 中的 `catch` 块捕获 `donuts` 的值时，`donuts` 的值会被填充到 catch 块参数 `e` 中，并执行 `catch` 块中的代码，产生以下输出：

12 donuts, and No Milk!
Go buy some milk.

如果 `donuts` 的值为正数，则 `throw` 语句不会执行。在这种情况下，`catch` 块不会执行。

目前，我们假设每个 `try` 块后面都跟着一个合适的 `catch` 块。稍后我们将讨论如果没有 `catch` 块会发生什么。

### catch 块参数

`catch` 块参数是 `catch` 块头部中的一个标识符，作为可能被抛出的异常（值）的占位符。当之前的 `try` 块中抛出一个（合适的）值时，该值将填充到 catch 块参数中。你可以使用任何合法的（非保留字）标识符作为 catch 块参数。

示例

```
catch(int e)

{

    cout << e << " donuts, and No Milk!\n"

    << "Go buy some milk.\n";

}
```
`e` 就是 catch 块参数。

...当 `catch` 块执行时。

接下来，我们总结一下在没有抛出异常时发生的情况。如果 `try` 块中没有抛出异常（值），那么在 `catch` 块完成后，程序执行将继续执行 `catch` 块之后的代码。换句话说，如果没有抛出异常，`catch` 块就会被忽略。在程序执行的大多数，`throw` 语句不会被执行，在大多数情况下，`try` 块中的代码将运行完毕，`catch` 块中的代码将被完全忽略。

### try-throw-catch

这是抛出和捕获异常的基础机制。`throw` 语句抛出异常（一个值）。`catch` 块捕获异常（该值）。当抛出异常时，`try` 块结束并执行 `catch` 块中的代码。在 `catch` 块完成后，执行 `catch` 块之后的代码（前提是 `catch` 块没有结束程序或执行了其他操作）。

如果 `try` 块中没有抛出异常，那么在 `try` 块完成后，程序执行将继续执行 `catch` 块之后的代码。（换句话说，如果没有抛出异常，则 `catch` 块就会被忽略。）

# 语法

```cpp
try {
  Some_Statements
  < 或者是带有 throw 语句的代码，或者是
    可能抛出异常的函数调用>
  Some_More_Statements
}
catch(Type_Name e) {
  < 如果在 try 
    块中抛出了与 catch-块 
    参数类型相同的值，则执行此代码>
}
```

# 示例

请参见显示 16.2。

# 自测练习题

- 1. 下面代码的输出输出什么？
```cpp
int waitTime = 46;
try {
  cout << "Try block entered.\n";
  if (waitTime > 30)
    throw waitTime;
  cout << "Leaving try block.\n";
} catch(int thrownValue) {
  cout << "Exception thrown with " << thrownValue << endl;
}
cout << "After catch block." << endl;
```

- 2. 如果我们进行以下更改，自测练习 1 中代码的输出将会是什么？将行
`int waitTime = 46;`
更改为
`int waitTime = 12;`

# 第 16 章 / 异常处理

- 3. 在自测练习 1 给出的代码中，哪个是 *throw* 语句？

- 4. 当执行 *throw* 语句时会发生什么？这是一个通用性问题。请说明通常会发生什么，而不仅仅是自测问题 1 代码或其他代码中发生了什么。

- 5. 在自测练习 1 给出的代码中，哪个是 *try* 块？

- 6. 在自测练习 1 给出的代码中，哪个是 *catch* 块？

- 7. 在自测练习 1 给出的代码中，哪个是 *catch-block* 参数？

# 定义你自己的异常类

*throw* 语句可以抛出任何类型的值。一种常见的做法是定义一个类，其对象携带你想要抛出给 *catch* 块的精确类型信息。定义专门异常类的另一个更重要的理由是，你可以使用不同的类型来识别每种可能的异常情况。

异常仅仅是一个类。异常异常类的特殊之处取决于它的使用方式。在选择异常的名称和其他细节时做出一些选择是有价值的。显示 16.3 包含一个带有程序员定义异常类的程序示例。这只是一个用来说明 C++ 异常处理的一些细节的演示程序。它对于如此简单的任务来说使用了太多的机制，但它是某些 C++ 细节的一个未说明的示例。

注意下面重现的 throw 语句：

```cpp
throw NoMilk(donuts);
```

`NoMilk(donuts)` 部分是对该类构造函数的调用。构造函数接受一个参数（在本例中为 donuts）并创建一个 `NoMilk` 类的对象。然后该对象就被“抛出”了。

# 多次抛出和捕获

*try* 块可能会抛出任意数量的异常值，这些值可以是不同的类型。在 *try* 块的任何执行中，都只会抛出一个异常（因为抛出异常会结束 *try* 块的执行），但在执行 *try* 块的不同时机，可能会抛出不同类型的异常值。每个 *catch* 块只能捕获一种类型的值，但你可以通过在 *try* 块之后放置多个 *catch* 块来捕获不同类型的异常值。例如，显示 16.4 中的程序在它的 *try* 块之后有两个 *catch* 块。

注意，`DivideByZero` 的 *catch* 块没有参数。如果你不需要参数，可以简单列出类型而不带任何参数。

# 显示 16.3 定义你自己的异常类

```cpp
#include <iostream>
using namespace std;
class NoMilk {
public:
    NoMilk();
    NoMilk(int howMany);
    int getDonuts();
private:
    int count;
};
int main() {
    int donuts, milk;
    double dpg;
    try {
        cout << "Enter number of donuts:\n";
        cin >> donuts;
        cout << "Enter number of glasses of milk:\n";
        cin >> milk;
        if (milk <= 0)
            throw NoMilk(donuts);
        dpg = donuts/static_cast<double>(milk);
        cout << milk << " glasses of milk.\n";
        cout << "You have " << dpg << " donuts for each glass of milk.\n";
    } catch (NoMilk e) {
        cout << e.getDonuts() << " donuts, and NoMilk!\n";
        cout << "Go buy some milk.\n";
    }
    return 0;
}
NoMilk::NoMilk() {}
NoMilk::NoMilk(int howMany) : count(howMany) {}
int NoMilk::getDonuts() {
    return count;
};
```

> 这仅仅是一个学习 C++ 语法的演示示例。请不要将其作为异常处理典型用法的示例。

# 显示 16.4 捕获多个异常（2 部分中的第 1 部分）

虽然在这里没有完成，但异常类有自己的接口和实现文件，并且可以放在命名空间中。这是另一个演示示例。

```cpp
#include <iostream>
#include <string>
using namespace std;
class NegativeNumber {
public:
    NegativeNumber();
    NegativeNumber(string takeMeToYourCatchBlock);
    string getMessage();
private:
    string message;
};
class DivideByZero {
};
int main() {
    int jemHadar, klingons;
    double portion;
    cout << "Enter number of JemHadar warriors:\n";
    cin >> jemHadar;
    if (jemHadar < 0)
        throw NegativeNumber("JemHadar");
    cout << "How many Klingon warriors do you have?\n";
    cin >> klingons;
    if (klingons < 0)
        throw NegativeNumber("Klingons");
    if (klingons != 0)
        portion = jemHadar/static_cast<double>(klingons);
    else
        throw DivideByZero();
    cout << "Each Klingon must fight "
        << portion << " JemHadar.\n";
}
catch(NegativeNumber e) {
    cout << "Cannot have a negative number of \n"
        << e.getMessage() << endl;
}
```

（续）

# 显示 16.4 捕获多个异常（2 部分中的第 2 部分）

```cpp
catch (DivideByZero) {
    cout << "Send for help.\n";
}
catch(...) {
    cout << "Unexplained exception.\n";
}
```

# 16.1 异常处理基础

```cpp
{ cout << "Send for help.\n"; }
```

## 显示 16.5 在函数内部抛出异常（2 部分中的 1 部分）

```cpp
#include <iostream>
#include <cctype>
using namespace std;
class DivideByZero {
};
double safeDivide(int top, int bottom) throw (DivideByZero);
int main() {
    int numerator;
    int denominator;
    double quotient;
    cout << "Enter numerator:\n";
    cin >> numerator;
    cout << "Enter denominator:\n";
    cin >> denominator;
    try {
        quotient = safeDivide(numerator, denominator);
    } catch (DivideByZero) {
        cout << "Error: Division by zero!\n";
        cout << "Program aborting.\n";
        exit(0);
    }
    cout << " = / " << quotient << endl;
    cout << "End of program.\n";
    return 0;
}
double safeDivide(int top, int bottom) throw (DivideByZero) {
    if (bottom == 0) {
        throw DivideByZero();
    }
    return top/static_cast<double>(bottom);
}
```

（续）

## 16.5 在函数内部抛出异常（2 部分中的 2 部分）

### 示例对话 1

```
Enter numerator:
5
Enter denominator:
10
5/10 = 0.5
End of Program.
```

### 示例对话 2

```
Enter numerator:
5
Enter denominator:
0
Error: Division by zero!
Program aborting.
```

该语句在 try 块中不可见。然而，从程序执行的角度来看，它在 try 块中，因为位于函数 `safeDivide` 的定义中，并且 try 块中有对 `safeDivide` 的调用。

### 异常规范

如果一个函数没有捕获异常，那么当该函数的任何调用可能抛出异常时，它至少应该警告程序员。如果函数定义中有可能抛出但未被捕获的异常，那么这些异常类型应该列在异常规范中，下例显示 16.5 中的函数声明所示：

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero);
```

如显示 16.5 所示，异常规范应该同时出现在函数声明和函数定义中。如果一个函数有多个函数声明，那么所有声明必须具有相同的异常规范。函数的异常规范有时也被抛出列表（throw list）。

如果函数定义中可以抛出多个一个异常，则异常类型之间用逗号分隔，如下所示：

```cpp
void someFunction() throw (DivideByZero, OtherException);
```
