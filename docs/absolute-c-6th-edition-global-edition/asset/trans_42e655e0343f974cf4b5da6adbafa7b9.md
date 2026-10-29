

## catch-Block 参数

catch-block 参数是 catch 块标题中的一个标识符，作为可能被抛出的异常（一个值）的占位符。当在前面的 try 块中抛出合适的数值时，该值将被填入 catch-block 参数。 （为了使 catch 块被执行，被抛出的值必须与为其 catch-block 参数给出的类型相同。）你可以使用任何合法的（非保留字）标识符作为 catch-block 参数。

### 示例

```
catch(int e)
{
    cout << e << " donuts, and No Milk!\n"
         << "Go buy some milk.\n";
}
```

e 是 catch-block 参数。

如果在 try 块中没有抛出异常（没有值），则在 try 块完成后，程序执行将继续执行 catch 块之后的<|message|>代码。换句话说，如果没有抛出异常，catch 块将被忽略。大多数情况下程序执行时，throw 语句不会被执行，因此在大多数情况下，try 块中的代码会运行到完成，而 catch 块中的代码将被完全忽略。

## try-throw-catch

抛出和捕获异常的基本机制是 try-throw-catch 序列。throw 语句抛出异常（一个值）。catch 块捕获异常（该值）。当抛出异常时，try 块结束，然后执行 catch 块中的代码。catch 块完成后，将执行 catch 块或块之后的代码（前提是 catch 块没有结束程序或执行其他特殊操作）。

（被抛出的异常的类型必须与为 catch-block 参数列出的类型匹配，否则该 catch 块不会捕获该异常。这一点在“Multiple Throws and Catches”小节中进一步讨论。）

如果在 try 块中没有抛出异常，则在 try 块完成后，程序执行将继续执行 catch 块或块之后的 fificode。 （换句话说，如果没有抛出异常，catch 块或块将被忽略。）

## 语法

```
try
{
    Some_Statements
    <Either some code with a throw statement or
    a function invocation that might throw an exception>
    Some_More_Statements
}
catch (Type e)
{
    <Code to be performed if a value of the
    catch-block parameter type is thrown in the try block>
}
```

### 示例

参见 Display 18.2 的示例。

## 自测练习

- 1. 以下代码会产生什么输出？

```
int waitTime = 46;

try
{
    cout << "Try block entered.\n";
    if (waitTime > 30)
        throw waitTime;
    cout << "Leaving try block.\n";
}

catch(int thrownValue)
{
    cout << "Exception thrown with\n"
         << "waitTime equal to " << thrownValue << endl;
}
cout << "After catch block" << endl;
```

- 2. 如果我们对自测练习 1 中的代码做如下更改，会产生什么输出？将行
  int waitTime = 46;
  改为
  int waitTime = 12;

## 自测练习（续）

- 3. 在自测练习 1 给出的代码中，throw 语句是什么？
- 4. 当执行 throw 语句时会发生什么？（说明一般情况下会发生什么，而不是仅仅说明在自测练习 1 的代码中或某些示例代码中会发生什么。）
- 5. 在自测练习 1 给出的代码中，try 块是什么？
- 6. 在自测练习 1 给出的代码中，catch 块是什么？
- 7. 在自测练习 1 给出的代码中，catch-block 参数是什么？

## 定义你自己的异常类

throw 语句可以抛出任何类型的值。常见的做法是定义一个类，其对象可以携带你希望抛给 catch 块的确切信息。定义专门的异常类的更重要原因是，你可以拥有不同的类型来标识每一种可能的异常情况。

异常类只是一个类。使其成为异常类的是其使用方式。尽管如此，在选择异常类的名称和其他细节时仍需注意。

Display 18.3 包含了一个使用程序员定义的异常类的程序示例。这只是一个玩具程序，用来说明异常处理的一些 C++ 细节。它对如此简单的任务使用了太多[content]

## catch-Block 参数

catch-block 参数是 catch 块标题中的一个标识符，作为可能被抛出的异常（一个值）的占位符。当在前面的 try 块中抛出合适的数值时，该值将被填入 catch-block 参数。 （为了使 catch 块被执行，被抛出的值必须与为其 catch-block 参数给出的类型相同。）你可以使用任何合法的（非保留字）标识符作为 catch-block 参数。

### 示例

```
catch(int e)
{
    cout << e << " donuts, and No Milk!\n"
         << "Go buy some milk.\n";
}
```

e 是 catch-block 参数。

如果在 try 块中没有抛出异常（没有值），则在 try 块完成后，程序执行将继续执行 catch 块之后的 fificode。换句话说，如果没有抛出异常，catch 块将被忽略。大多数情况下程序执行时，throw 语句不会被执行，因此在大多数情况下，try 块中的代码会运行到完成，而 catch 块中的代码将被完全忽略。

## try-throw-catch

抛出和捕获异常的基本机制是 try-throw-catch 序列。throw 语句抛出异常（一个值）。catch 块捕获异常（该值）。当抛出异常时，try 块结束，然后执行 catch 块中的代码。catch 块完成后，将执行 catch 块或块之后的 fificode（前提是 catch 块没有结束程序或执行其他特殊操作）。

（被抛出的异常的类型必须与为 catch-block 参数列出的类型匹配，否则该 catch 块不会捕获该异常。这一点在“Multiple Throws and Catches”小节中进一步讨论。）

如果在 try 块中没有抛出异常，则在 try 块完成后，程序执行将继续执行 catch 块或块之后的 fificode。 （换句话说，如果没有抛出异常，catch 块或块将被忽略。）

## 语法

```
try
{
    Some_Statements
    <Either some code with a throw statement or
    a function invocation that might throw an exception>
    Some_More_Statements
}
catch (Type e)
{
    <Code to be performed if a value of the
    catch-block parameter type is thrown in the try block>
}
```

### 示例

参见 Display 18.2 的示例。

## 自测练习

- 1. 以下代码会产生什么输出？

```
int waitTime = 46;

try
{
    cout << "Try block entered.\n";
    if (waitTime > 30)
        throw waitTime;
    cout << "Leaving try block.\n";
}

catch(int thrownValue)
{
    cout << "Exception thrown with\n"
         << "waitTime equal to " << thrownValue << endl;
}
cout << "After catch block" << endl;
```

- 2. 如果我们对自测练习 1 中的代码做如下更改，会产生什么输出？将行
  int waitTime = 46;
  改为
  int waitTime = 12;

## 自测练习（续）

- 3. 在自测练习 1 给出的代码中，throw 语句是什么？
- 4. 当执行 throw 语句时会发生什么？（说明一般情况下会发生什么，而不是仅仅说明在自测练习 1 的代码中或某些示例代码中会发生什么。）
- 5. 在自测练习 1 给出的代码中，try 块是什么？
- 6. 在自测练习 1 给出的代码中，catch 块是什么？
- 7. 在自测练习 1 给出的代码中，catch-block 参数是什么？

## 定义你自己的异常类

throw 语句可以抛出任何类型的值。常见的做法是定义一个类，其对象可以携带你希望抛给 catch 块的确切信息。定义专门的异常类的更重要原因是，你可以拥有不同的类型来标识每一种可能的异常情况。

异常类只是一个类。使其成为异常类的是其使用方式。尽管如此，在选择异常类的名称和其他细节时仍需注意。

Display 18.3 包含了一个使用程序员定义的异常类的程序示例。这只是一个玩具程序，用来说明异常处理的一些 C++ 细节。它对如此简单的任务使用了太多机器，但它是一个否则不含杂乱的示例，展示了一些 C++ 细节。

注意 throw 语句，重现如下：

```
throw NoMilk(donuts);
```

部分 NoMilk(donuts) 是对类 NoMilk 的构造函数的调用。构造函数接受一个 int 参数（这里是 donuts）并创建一个 NoMilk 类的对象。然后该对象被抛出。

## 多重抛出和捕获

try 块可能抛出任意数量的异常值，这些值可以是不同类型。在 try 块的一次执行中，最多只会抛出一个异常（因为 throw 语句会结束 try 块的执行），但在不同场合执行 try 块时可以抛出不同类型的异常值。每个 catch 块只能捕获一种类型的值，但你可以通过在 try 块后放置多个 catch 块来捕获不同类型的异常值。例如，Display 18.4 中的程序在其 try 块后有两个 catch 块。

## Display 18.3 定义你自己的异常类

```
#include <iostream>
using std::cin;
using std::cout;

class NoMilk
{
public:
    NoMilk( ) {}
    NoMilk(int howMany) : count(howMany) {}
    int getCount( ) const { return count; }
private:
    int count;
};

int main( )
{
    int donuts, milk;
    double dpg;
    try
    {
        cout << "Enter number of donuts:\n";
        cin >> donuts;
        cout << "Enter number of glasses of milk:\n";
        cin >> milk;

        if (milk <= 0)
            throw NoMilk(donuts);

        dpg = donuts / static_cast<double>(milk);
        cout << donuts << " donuts.\n"
             << milk << " glasses of milk.\n"
             << "You have " << dpg
             << " donuts for each glass of milk.\n";
    }
    catch(NoMilk e)
    {
        cout << e.getCount( ) << " donuts, and No Milk!\n"
             << "Go buy some milk.\n";
    }
    cout << "End of program.\n";
    return 0;
}
```

> 这只是一个玩具示例，用于学习 C++ 语法。不要将其作为异常处理良好典型使用的示例。

> 示例对话与 Display 18.2 相同。

## Display 18.4 捕获多个异常（第 1 部分，共 2 部分）

```
#include <iostream>
#include <string>
using std::cin;
using std::cout;
using std::endl;
using std::string;

class NegativeNumber
{
public:
    NegativeNumber() {}
    NegativeNumber(string theMessage): message(theMessage) {}
    string getMessage() const { return message; }
private:
    string message;
};

class DivideByZero
{};

int main()
{
    int pencils, erasers;
    double ppe; //pencils per eraser

    try
    {
        cout << "How many pencils do you have?\n";
        cin >> pencils;
        if (pencils < 0)
            throw NegativeNumber("pencils");
        cout << "How many erasers do you have?\n";
        cin >> erasers;
        if (erasers < 0)
            throw NegativeNumber("erasers");

        if (erasers != 0)
            ppe = pencils / static_cast<double>(erasers);
        else
            throw DivideByZero();
        cout << "Each eraser must last through "
             << ppe << " pencils.\n";
    }
```

> *异常类可以拥有自己的接口和实现文件，并且可以放在命名空间中。这又是另一个玩具示例。*

## Display 18.4 捕获多个异常（第 2 部分，共 2 部分）

```
39 catch(NegativeNumber e)
40 {
41     cout << "Cannot have a negative number of "
42     << e.getMessage() << endl;
43 }
44 catch(DivideByZero)
45 {
46     cout << "Do not make any mistakes.\n";
47 }
48 
49 cout << "End of program.\n";
50 return 0;
51 }
```

如果 catch-block 参数未被使用，你不需要在标题中给出它。

## 示例对话 1

```
How many pencils do you have?
5
How many erasers do you have?
2
Each eraser must last through 2.5 pencils
End of program.
```

## 示例对话 2

```
How many pencils do you have?
-2
Cannot have a negative number of pencils
End of program.
```

## 示例对话 3

```
How many pencils do you have?
5
How many erasers do you have?
0
Do not make any mistakes.
End of program.
```

注意 DivideByZero 的 catch 块中没有参数。如果不需要参数，你只需列出类型而不带参数即可。这在编程提示部分“Exception Classes Can Be Trivial”中稍有讨论。

