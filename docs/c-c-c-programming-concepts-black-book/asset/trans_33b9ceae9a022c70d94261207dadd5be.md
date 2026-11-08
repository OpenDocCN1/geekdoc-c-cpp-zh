
## 第15章

```cpp
#include <iostream>
#include <string>
using namespace std;
class DivideByZero {
public:
    DivideByZero(int a, int b) : numerator(a), denominator(b), errorMessage("divide by zero Exception has occured") {}
    ~DivideByZero() {}
    int getNumerator()
    {
        return numerator;
    }
    int getDenominator()
    {
        return denominator;
    }
    string getMessage()
    {
        return errorMessage;
    }
private:
    int numerator;
    int denominator;
    string errorMessage;
};
int main()
{
    int a = 6;
    int b = 0;
    int result;
    try {
        if (b == 0) {
            throw DivideByZero(a, b);
        }
        result = a/b;
    }
    catch (DivideByZero e)
    {
        cout << "An exception has occurred..." << endl;
        cout << e.getMessage() << endl;
        cout << "Numerator is: " << e.getNumerator() << endl;
        cout << "Denominator is: " << e.getDenominator() << endl;
    }
    cout << "Exiting the program." << endl;
    return 0;
}
```

## 注意

try 子句后面的复合语句是受保护的代码区域。throw 表达式抛出一个异常。catch 子句后面的复合语句是特定的异常处理程序，并接收从 throw 表达式抛出的异常。catch 子句后面的异常声明语句指示该子句处理的异常种类。此类型可以是有效的数据类型，包括 C++ 类。

注意，C++ 默认不会捕获除零异常。当发生除零情况时，代码会崩溃。因此，唯一的选择是编写一个类或方法来处理除零情况。以下示例展示了如何处理除零情况以及如何构造异常：

```cpp
#include<iostream>
using namespace std;
class Division
{
    public:
        double quotient(int numerator, int denominator);
    private:
};

double Division::quotient(int numerator, int denominator)
{
    if(!denominator)
    {
        exception e("divide by 0 exception");
        throw(e);
    }
    return (static_cast< double >( numerator ))/denominator;
}
int main()
{
    Division d;
    try
    {
        cout<<"1. (500/10) = "<<d.quotient(500, 10)<<endl;
        cout<<"2. (15/6) = "<<d.quotient(15, 6)<<endl;
        cout<<"3. (10/0) = "<<d.quotient(10, 0)<<endl;
        cout<<"4. (30/9) = "<<d.quotient(30, 9)<<endl;
    }
    catch(exception& e)
    {
        cout<<"Exception caught with cause :"<<e.what()<<endl;
    }
    return 0;
}
```

上述程序的输出如下：

```text
1. (500/10) = 50
2. (15/6) = 2.5
Exception caught with cause: Divide by 0 exception
```

现在我们来讨论异常处理的机制。

## 异常处理——机制

每当抛出异常时，它会被相应的 catch 声明捕获，并由该声明处理异常。一个 try 可以有多个 catch 语句；可以使用哪个 catch 语句将由异常的种类决定。也就是说，如果 catch 中指定的数据类型与异常的数据类型匹配，那么所有其他 catch 语句都会被绕过。当捕获到异常时，catch 子句中指定的参数将包含该异常。任何类型的数据最终都可能被捕获，包括已创建的类。如果完全没有抛出异常，则不会执行任何 catch 语句。如果找到匹配项，则执行 catch 处理程序的代码，控制流从 catch 处理程序之后的位置继续。

如果控制流通过正常的顺序执行到达 try 语句，那么就完成了 try 块的受保护部分。如果受保护部分中没有要抛出的异常，那么 try 块后面的 catch 子句当然不会执行。执行将继续从 try 块之后最后一个 catch 子句后面的语句开始。如果受保护部分执行中或任何例程中抛出异常，而该受保护部分直接或间接调用了该例程。异常对象由 throw 操作数所创建的对象生成。这意味着可能涉及拷贝构造函数。此时，编译器会在更高层的异常上下文中查找 catch 子句，该子句可以处理所抛出类型的异常，或查找可处理任何类型异常的新 catch 处理程序。catch 处理程序按照它们在 try 块之后出现的顺序进行检查。如果找不到合适的处理程序，就检查下一个动态关联的 try 块。此过程持续进行，直到检查最外层的封闭 try。如果未找到匹配的处理程序，或者在栈展开期间、处理程序获得控制之前发生异常，则调用预定义的运行时函数 terminate()。

throw 语句通常接受一个参数，并将其作为参数传递给异常处理程序。throw 语句的一般格式如下：

```cpp
throw ex;
```

throw 生成由 ex 指定的异常。如果要捕获该异常，那么 throw 必须在 try 块内执行，或者从 try 块内调用的任何函数中执行。

在下一节中，我们将演示如何在栈类中处理异常。

## 异常——栈

数据被压入栈中并从中弹出。栈可以具有以下约束：

- 栈的大小将是固定的
- 如果试图将数据压入已满的栈，栈将抛出栈溢出异常
- 如果试图从空栈中弹出数据，栈将抛出栈空异常

考虑以下用于实现栈类的程序：

```cpp
#include <iostream>
#include <string>
using namespace std;
class DivideByZero {
public:
    DivideByZero(int N, int D) : numerator(N), denominator(D), errorMessage("Divide by zero exception because of occur!!!") {}
    ~DivideByZero() {}
    void getMessage()
    {
        cout << "An exception has occurred in the program. " << endl;
        cout << errorMessage << endl;
        cout << "The Numerator is: " << numerator << endl;
        cout << "The Denominator is: " << denominator << endl;
    }

    // private declarations
private:
    int numerator;
    int denominator;
    string errorMessage;
};

// defining Stack overflow exception
class StackOverflowException {
public:
    StackOverflowException() {}
    ~StackOverflowException() {}
    void getMessage()
    {
        cout<< "An exception has occurred. "<< endl;
        cout<< "Exception: Stack is Full." << endl;
    }
};

// Defining empty stack exception
class StackEmptyException {
public:
    StackEmptyException() {}
    ~StackEmptyException() {}
    void getMessage()
    {
        cout<< "An exception has occurred..." << endl;
        cout<< "Exception: Stack is Empty." << endl;
    }
};

// Implementing a very crude stack class that is intended only to illustrate
// exceptions.

class CrudeStack {
public:
    CrudeStack() : index(-1) {}
    ~CrudeStack() {}
    void push(int value)
    {
        index++;
        if (index >= 25)
        {
            throw StackOverflowException();
        }
        data[index] = value;
    }

    int pop()
    {
        if (index < 0)
        {
            throw StackEmptyException();
        }
        int value = data[index];
        index--;
        return value;
    }

//Private declarations
private:
    int data[20];
    int index;
};

int divide(int numer, int denom)
{
    if (denom == 0)
    {
        throw DivideByZero(numer,denom);
    }
    return numer/denom;
}
int main()
{
    CrudeStack stack;
    int numer;
    int denom;
    int value;
    cout<< "Starting implementation of crude stack..." << endl;
    cout<< "Enter the numerator: ";
    cin>> numer;
    cout<< "Enter the denominator: ";
    cin>> denom;
    try {
        stack.push(numer);
        stack.push(denom);
        divide(numer, denom);
        value = stack.pop();
        cout<< "An starting popping of values..." << endl;
        cout<< "The following is popped " << value<< endl;
        value = stack.pop();
        cout<< "The following is popped " << value<< endl;
        value = stack.pop();
        cout<< "The following is popped " << value<< endl;
    }
    catch (StackOverflowException e) {
        e.getMessage();
    }
    catch (StackEmptyException e) {
        e.getMessage();
    }
    catch (DivideByZero e) {
        e.getMessage();
    }
    catch (...) {
        cout<< "An exception has occurred..." << endl;
        cout<< "An exception of unknown type occurred" << endl;
    }
    cout<< "Exiting the program..." << endl;
    return 0;
}
```

在上述程序中，每当发生除零错误时，都会通过异常妥善处理。同样，当栈溢出或为空时，也会抛出异常。

## 栈展开

每当控制流进入函数时，所有静态分配的局部变量都会在栈上创建。同样，当控制流退出函数时，这些变量会从栈中弹出。现在，假设 main() 函数调用 F1() 函数，而 F1() 又调用 F2()。F2() 函数可能抛出两种条件：E1 和 E2，如下所示：
