

尝试使用它。你可以在同一语句中声明并初始化一个变量，如下例所示：

```
int myInt = 99;
```

或者，你也可以这样做，前提是 myOtherInt 是一个已初始化的整数变量：

```
int myInt = myOtherInt * 99;
```

现在，请记住，你赋给变量的值必须与变量的类型相同。例如，你只能将 int 值赋给 int 变量。C# 编译器可以快速推断出用于初始化变量的表达式的类型，并指出它是否与变量的类型不匹配。你也可以要求 C# 编译器从表达式推断变量的类型，并在声明变量时使用 var 关键字代替类型，如下所示：

```
var myVariable = 99;
var myOtherVariable = "Hello";
```

变量 myVariable 和 myOtherVariable 被称为隐式类型变量。var 关键字会使编译器根据用于初始化它们的表达式的类型推断变量的类型。在这些示例中，myVariable 是 int，而 myOtherVariable 是 string。然而，你必须明白，这只是声明变量的便利方式，一旦变量被声明，你只能为其赋予推断类型的<|message|>值——例如，你不能在程序的后面将 float、double 或 string 值赋给 myVariable。你还应明白，你只能在提供表达式来初始化变量时使用 var 关键字。以下声明是非法的，会导致编译错误：

```
var yetAnotherVariable; // Error - compiler cannot infer type
```

## Important

如果你过去曾使用 Visual Basic 编程，你可能熟悉 *Variant* 类型，你可以用它在变量中存储任何类型的值。我在此强调，你应该忘记你在用 Visual Basic 编程时关于 *Variant* 变量所学的一切。虽然关键字看起来相似，但 *var* 和 *Variant* 含义完全不同。当你使用 *var* 关键字在 C# 中声明变量时，你可以赋给该变量的值的类型 *不能改变*，它必须与用于初始化变量的类型相同。

如果你是一个纯粹主义者，你现在可能正咬牙切齿，想知道为什么像 C# 这样精致的语言的设计者会允许 *var* 这样的特性出现。毕竟，这听起来像是程序员极度懒惰的借口，会使理解程序正在做什么或追踪错误变得更加困难（甚至可能很容易在你的代码中引入新的错误）。然而，请相信我，*var* 在 C# 中有非常合理的用途，当你阅读接下来的许多章节时你会看到这一点。不过，就目前而言，我们将坚持使用显式类型变量，除非隐式类型变得必要。

## Summary

在本章中，你学习了如何创建和使用变量，并了解了 C# 中变量可用的一些常见数据类型。你还学习了标识符。此外，你使用了一些运算符来构建表达式，并学习了运算符的优先级和结合性如何决定表达式的求值方式。

- 如果你想继续下一章，请保持 Visual Studio 2015 运行并转到第 3 章。
- 如果你现在想退出 Visual Studio 2015，请在 File 菜单上单击 Exit。如果出现 Save 对话框，请单击 Yes 并保存项目。

## Quick Reference

| To | Do this |
|---|---|
| Declare a variable | Write the name of the data type, followed by the name of the variable, followed by a semicolon. For example: `int outcome;` |
| Declare a variable and give it an initial value | Write the name of the data type, followed by the name of the variable, followed by the assignment operator and the initial value. Finish with a semicolon. For example: `int outcome = 99;` |
| Change the value of a variable | Write the name of the variable on the left, followed by the assignment operator, followed by the expression calculating the new value, followed by a semicolon. For example: `outcome = 42;` |
| Generate a string representation of the value in a variable | Call the ToString method of the variable. For example: `int intVar = 42;` `string stringVar = intVar.ToString();` |
| Convert a string to an int | Call the System.Int32.Parse method. For example: `string stringVar = "42";` `int intVar = System.Int32.Parse(stringVar);` |
| Override the precedence of an operator | Use parentheses in the expression to force the order of evaluation. For example: `(3 + 4) * 5` |
| Assign the same value to several variables | Use an assignment statement that lists all the variables. For example: `myInt4 = myInt3 = myInt2 = myInt = 10;` |
| Increment or decrement a variable | Use the ++ or -- operator. For example: `count++;` |

## Chapter 3. Writing methods and applying scope

完成本章后，你将能够：

- Declare and call methods.
- Pass information to a method.
- Return information from a method.
- Define local and class scope.
- Use the integrated debugger to step into and out of methods as they run.

在第 2 章“Working with variables, operators, and expressions”中，你学习了如何声明变量，如何使用运算符创建表达式，以及优先级和结合性如何控制包含多个运算符的表达式的求值方式。在本章中，你将学习方法。你将看到如何声明和调用方法，如何使用参数和形参将信息传递给方法，以及如何使用 return 语句从方法返回信息。你还将看到如何使用 Microsoft Visual Studio 2015 集成调试器在方法运行时进入和退出方法。当你需要跟踪方法执行过程而它们没有按预期工作时，此信息很有用。最后，你将学习如何声明接受可选参数的方法以及如何使用命名参数调用方法。

## Creating methods

方法是一段命名的语句序列。如果你以前使用 C、C++ 或 Microsoft Visual Basic 等语言编程过，你会发现方法类似于函数或子程序。方法有一个名称和一个主体。方法名称应是有意义的标识符，表示方法的主要用途（例如 calculateIncomeTax）。方法主体包含在调用方法时实际运行的语句。此外，方法可以接收一些数据进行处理并返回信息，通常是处理的結果。方法是一种基本而强大的机制。

## Declaring a method

声明 C# 方法的语法如下：

```
returnType methodName ( parameterList )
{
    // method body statements go here
}
```

以下是构成声明的元素的描述：

- *returnType* 是类型的名称，指定方法作为其处理结果返回的信息种类。这可以是任何类型，例如 *int* 或 *string*。如果你编写的方法不返回值，则必须使用关键字 *void* 代替返回类型。
- *methodName* 是用于调用方法的名称。方法名遵循与变量名相同的标识符规则。例如，*addValues* 是有效的方法名，而 *add$Values* 则不是。目前，你应遵循方法名的 camelCase 惯例；例如，*displayCustomer*。
- *parameterList* 是可选的，描述可以传递给方法以供其处理的信息的类型和名称。你在打开和关闭括号 ( ) 之间编写参数，就像声明变量一样，类型名称后跟参数名称。如果要编写的方法有两个或多个参数，则必须用逗号分隔它们。
- 方法主体语句是在调用方法时运行的代码行。它们被包含在大括号 { } 之间。

## Important

如果你使用 C、C++ 和 Visual Basic 编程，你应该注意 C# 不支持全局方法。你必须将所有方法写在类内部；否则，你的代码将无法编译。

下面是名为 *addValues* 的方法的定义，它返回 *int* 结果并有两个 *int* 参数，*leftHandSide* 和 *rightHandSide*：

```
int addValues(int leftHandSide, int rightHandSide)
{
    // ...
    // method body statements go here
    // ...
}
```

## Note

你必须显式指定任何参数的类型和方法返回类型。你不能使用 *var* 关键字。

下面是名为 *showResult* 的方法的定义，它不返回值

