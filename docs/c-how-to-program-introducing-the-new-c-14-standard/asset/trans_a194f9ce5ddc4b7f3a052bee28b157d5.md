

图 17.1 `DivideByZeroException` 类的定义。

## 17.2.2 演示异常处理

**图 17.2** 使用异常处理来封装可能抛出 `DivideByZeroException` 的代码，并在异常发生时处理该异常。

用户输入两个整数，这两个整数作为参数传递给函数 `quotient`（第 10～18 行）。该函数用第一个参数（`numerator`）除以第二个参数（`denominator`）。假设用户没有将除数指定为 `0`，函数 `quotient` 将返回除法结果。如果用户为除数输入 `0`，`quotient` 将抛出异常。在示例输出中，前两行显示了一次成功的计算，接下来的两行显示了由于尝试除以零而导致的失败。发生异常时，程序会告知用户错误，并提示用户输入两个新的整数。在讨论代码之后，我们将考察产生*这些输出*的用户输入和程序控制流。

```cpp
// Fig. 17.2: fig17_02.cpp
// Example that throws exceptions on
// attempts to divide by zero.
#include <iostream>
#include "DivideByZeroException.h" // DivideByZeroException class
using namespace std;

// perform division and throw DivideByZeroException object if
// divide-by-zero exception occurs
double quotient(int numerator, int denominator) {
   // throw DivideByZeroException if trying to divide by zero
   if (denominator == 0) {
      throw DivideByZeroException{}; // terminate function
   }

   // return division result
   return static_cast<double>(numerator) / denominator;
}

int main() {
   int number1; // user-specified numerator
   int number2; // user-specified denominator

   cout << "Enter two integers (end-of-file to end): ";

   // enable user to enter two integers to divide
   while (cin >> number1 >> number2) {
      // try block contains code that might throw exception
      // and code that will not execute if an exception occurs
      try {
         double result{quotient(number1, number2)};
         cout << "The quotient is: " << result << endl;
      }
      catch (const DivideByZeroException& divideByZeroException) {
         cout << "Exception occurred: "
              << divideByZeroException.what() << endl;
      }

      cout << "\nEnter two integers (end-of-file to end): ";
   }

   cout << endl;
}
```

```text
Enter two integers (end-of-file to end): 100 7
The quotient is: 14.2857

Enter two integers (end-of-file to end): 100 0
Exception occurred: attempted to divide by zero

Enter two integers (end-of-file to end): ^Z
```

图 17.2 尝试除以零时抛出异常的示例。

## 17.2.3 将代码封装在 `try` 块中

程序首先提示用户输入两个整数。整数在 `while` 循环的条件中输入（第 27 行）。第 31 行将这些值传递给函数 `quotient`（第 10～18 行）；该函数要么对整数执行除法并返回结果，要么在尝试除以零时**抛出异常**（即指示发生了错误）。异常处理适用于这样的情况：检测到错误的函数无法处理该错误。

正如你在**第 7.10 节**中所学，`try` 块支持异常处理，它将可能引发异常的语句，以及发生异常时应该跳过的语句封装起来。第 30～33 行中的 `try` 块封装了对函数 `quotient` 的调用以及显示除法结果的语句。在本例中，由于对函数 `quotient` 的调用（第 31 行）可能*抛出*异常，因此我们将该函数调用封装在 `try` 块中。将输出语句（第 32 行）放在 `try` 块中，可以确保仅当函数 `quotient` 返回结果时才会输出结果。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2162_0.png)

**软件工程观察 17.3**

*异常可能通过 `try` 块中明确列出的代码、对其他函数（包括库函数）的调用、由 `try` 块中的代码发起的深层嵌套函数调用，以及 `new` 等运算符而出现（[第 17.8 节](#)）。*

## 17.2.4 定义用于处理 `DivideByZeroException` 的 `catch` 处理程序

你在**第 7.10 节**中已经了解到，异常由 `catch` 处理程序处理。每个 `try` 块后面*必须立即*跟随至少一个 `catch` 处理程序（第 34～37 行）。异常参数应该*始终*声明为异常类型的*引用*，该类型是 `catch` 处理程序能够处理的异常类型（本例中为 `DivideByZeroException`）。这样可以避免捕获异常时复制异常对象，并允许 `catch` 处理程序正确捕获派生类异常。

当 `try` 块中发生异常时，实际执行的是第一个类型与所发生异常类型*匹配*的 `catch` 处理程序（即，`catch` 块中的类型与抛出的异常类型完全相同，或者是该异常类型的*直接*或*间接基类*）。如果异常参数包含一个*可选的*参数名，则 `catch` 处理程序可以在其主体中使用该参数名与捕获的异常进行交互；`catch` 处理程序的主体由花括号（`{` 和 `}`）界定。

`catch` 处理程序通常会向用户报告错误、将错误记录到文件中、优雅地终止程序，或尝试使用替代策略来完成失败的任务。在本例中，`catch` 处理程序只是报告用户尝试除以零。然后，程序提示用户输入两个新的整数值。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2164_0.png)

**常见编程错误 17.1**

*在 `try` 块与其对应的 `catch` 处理程序之间，或在各个 `catch` 处理程序之间放置代码，是语法错误。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2164_1.png)

**常见编程错误 17.2**

*每个 `catch` 处理程序只能有一个参数——指定以逗号分隔的异常参数列表是语法错误。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2165_0.png)

**常见编程错误 17.3**

*在同一个 `try` 块后面的多个 `catch` 处理程序中捕获相同类型，是编译错误。*

## 17.2.5 异常处理的终止模型

如果 `try` 块中的某条语句导致异常发生，则 `try` 块失效（即*立即终止*）。接下来，程序会搜索能够处理所发生异常类型的第一个 `catch` 处理程序。程序将抛出异常的类型与每个 `catch` 的异常参数类型进行比较，直到找到匹配项。若两种类型*相同*，或者抛出异常的类型是异常参数类型的*派生类*，则认为匹配成功。

匹配成功后，匹配的 `catch` 处理程序中的代码将执行。当 `catch` 处理程序执行到其右花括号（`}`）并完成处理时，该异常被视为已处理，并且 `catch` 处理程序中定义的局部变量（包括 `catch` 参数）将离开作用域。程序控制**不会**返回到异常发生的位置（称为**抛出点**），因为 `try` 块已经*失效*。相反，控制将从 `try` 块之后、最后一个 `catch` 处理程序之后的第一条语句（图 17.2 中的第 39 行）继续执行。这称为异常处理的**终止模型**。有些语言使用异常处理的**恢复模型**，在该模型中，异常处理完成后，控制会从抛出点之后继续执行。与其他代码块一样，*当 `try` 块终止时，在该块中定义的局部变量将离开作用域*。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2166_0.png)

**常见编程错误 17.4**

如果假设异常处理完成后，控制会返回到抛出点之后的第一条语句，就可能发生逻辑错误。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2166_1.png)

**错误预防提示 17.2**

借助 C++ 异常处理，程序在处理问题后可以继续执行，而不是终止。这有助于确保应用程序具备足够的健壮性，从而支持所谓的任务关键型计算或业务关键型计算。

