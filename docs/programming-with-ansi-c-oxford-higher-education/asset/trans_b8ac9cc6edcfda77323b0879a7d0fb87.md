

```cpp
class MyException
{
private:
    int ExNumber;
    string ExMessage;
public:
    MyException(int ErrNo, string Description)
    {
        ExNumber = ErrNo;
        ExMessage = Description;
    }

    void ShowEx()
    {
        cout << "Error number is" << ExNumber << "\n";
        cout << ExMessage << "\n";
    }
};

void ExGen()
{
    cout << "Inside the function \n";
    try
    {
        cout << "Inside try block\n";
        MyException Error1(20, "Error testing");
        cout << "Press 1 for int, 2 for char, 3 for MyException, and 4 for string \n";
        int reply;
        cin >> reply;
        cout << "Assuming error and throwing exception now \n";
        switch(reply)
        {
            case 1:
                throw 10;
            case 2:
                throw 'a';
            case 3:
                throw Error1;
            case 4:
                throw "There is nobody to catch this \n";
        }
        cout << "This statement will not be executed \n";
    }
    catch (int IntEx)
    {
        cout << "Integer exception" << IntEx << "is caught in the function \n";
        throw;  // Rethrowing
    }
}
```

## 8.12 terminate() AND unexpected() FUNCTIONS

如前所述，terminate() 是在与异常相关的运行时错误发生时调用 abort() 以退出程序的函数。通过 terminate() 函数进行间接调用的原因是用户可以定义自己的 terminate() 函数，而不是仅调用 abort() 且不做其他操作的内置 terminate()。这样用户就可以在退出程序前关闭所有打开的文件并释放资源。让我们通过以下程序来看看这是如何实现的。

```cpp
//SetTerminate.cpp
#include <exception>
#include <iostream>
#include <string>
using namespace std;
class MyException
{
private:
    int ExNumber;
    string ExMessage;
public:
    MyException(int ErrNo, string Description)
    {
        ExNumber = ErrNo;
        ExMessage = Description;
    }
    void ShowEx()
    {
        cout << "Error number is" << ExNumber << "\n";
        cout << ExMessage << "\n";
    }
};
void ExGen()
{
    cout << "Inside the function \n";
    cout << "Inside try block \n";
    cout << "Assuming error and throwing exception now \n";
    MyException Error1(20, "Error testing");
    throw Error1;
    cout << "This statement will not be executed";
}
void MyTerminate()
{
    cout << "This is my terminate function";
    /* The cleanup code comes here; it closes all open files,
    closes open connections, and runs destructors if need be */
    exit(-1);
}
void main()
{
    void MyTerminate();
    set_terminate(MyTerminate);
    /* Instead of system's terminate, MyTerminate is called */
    cout << "Inside main\n";
    ExGen();
    // This would generate an exception for which no catch is available
    cout << "This will not be executed";
}
```

我们现在在这个例子中拥有自己的 terminate() 函数，而不是默认的 terminate()。我们可以在这里完成所有的清理工作。我们可以关闭文件，释放动态内存，如果在客户端-服务器环境中工作，还可以关闭连接，以便连接方意识到我们的离开，等等。

**注意：** 我们可以拥有自己的 terminate() 函数，而不是仅调用 abort() 的默认 terminate()。set_terminate() 函数告诉系统存在用户指定的新的 terminate() 函数。

类似地，对于具有异常规范的函数，如果函数抛出不允许的异常，则会调用 unexpected() 函数，该函数进而调用 abort()。与 terminate() 类似，可以使用 set_unexpected() 来提供我们自己的函数。考虑以下程序。set_unexpected() 函数用于告诉系统存在用户指定的新的 unexpected() 函数。

```cpp
//SetUnexpected.cpp
#include <exception>
#include <iostream>
#include <string>
using namespace std;
class MyException
{
private:
    int ExNumber;
    string ExMessage;
public:
    MyException(int ErrNo, string Description)
    {
        ExNumber = ErrNo;
        ExMessage = Description;
    }
    void ShowEx()
    {
        cout << "Error number is" << ExNumber << "\n";
        cout << ExMessage << "\n";
    }
};

void ExGen() throw()
{
    cout << "Inside the function \n";
    cout << "Inside try block \n";
    cout << "Assuming error and throwing exception now \n";
    MyException Error1(20, "Error testing");
    throw Error1;
    cout << "This statement will not be executed";
}

void MyUnExpected()
{
    cout << "This is my unexpected function \n";
    /* The cleanup code comes here; it closes all open files, closes open connections, and runs destructors if needed */
    exit(-1);
}

int main()
{
    try
    {
        void MyUnExpected();
        set_unexpected(MyUnExpected);
        cout << "Inside main\n";
        ExGen();
        // This would generate an exception for which no catch is available
        cout << "This will not be executed \n";
    }
    catch(...)
    {
        cout << "Caught it!";
    }
    return 0;
}
```

```text
Inside main
Inside the function
Inside try block
Assuming error and throwing exception now
This is my unexpected function
```

函数 ExGen() 的异常规范为 throw()。如果 ExGen() 抛出某个异常，则会调用 unexpected() 函数，此函数的输出为 "This is my unexpected function"。在给出的示例中，我们为意外情况编写了自己的函数。我们已使用语句 `set_unexpected(MyUnExpected);` 指定使用该函数而不是内置的 unexpected()。因此，用户定义的 MyUnExpected() 函数被调用。

## 8.13 uncaught_exception() FUNCTION

当抛出异常时，它会自动调用栈展开过程。在此过程中，从 throw 语句之前到 try 块开始的所有对象都按创建的逆序销毁。可能其中一些正在被销毁的对象具有析构函数，而析构函数本身也可能抛出异常。

如果至少有一个对象包含这样的析构函数，我们就会遇到一种情况：第一个异常尚未完全处理，而第二个异常正在被抛出。C++ 中不可能同时处理两个异常。这种情况的正常结果是调用 abort()，从而终止程序。在这种情况下，来自内置异常类的 uncaught_exception() 函数非常有用。它在抛出异常时返回 true。如果析构函数检查发现析构函数被调用时已抛出异常，它将不会抛出新的异常。该函数的算法如下：

```text
if(uncaught_exception())
{
    Do not call the function that might throw an exception
}
else
{
    Follow the natural sequence of the destructor algorithm
}
```

`uncaught_exception()` 是查找未处理的异常的一种便捷方法。

程序 8.5 演示了 uncaught_exception() 函数的使用。当抛出异常时，try 块中定义的所有对象的析构函数会一个接一个地被调用。然后，异常被处理，现在它被称为已捕获。如果我们现在检查未捕获的异常，会发现它已被捕获。

### PROGRAM 8.5 Using uncaught_exception to find out unhandled exceptions

```cpp
//UncaughtException.cpp
#include <exception>
#include <iostream>
using namespace std;

class TestClass
{
    char *ptrMessage;
public:
    TestClass(char Message[], int LengthOfMessage)
    {
        ptrMessage = new char [LengthOfMessage + 1];
        for(int i = 0; i < LengthOfMessage; i++)
        {
            ptrMessage[i] = Message[i];
        }
        ptrMessage[LengthOfMessage] = 0; // Null

    }

    friend ostream & operator <<(ostream & TempOut, TestClass & TempData);

    // To destroy the objects defined in the try block
    ~TestClass()
    {
        if(uncaught_exception() == true)
        {
            cout << "There is an uncaught exception in process when";
            cout << *this;
            delete [] ptrMessage;
        }
        else
        {
            cout << "There is no uncaught exception in process when";
            cout << *this;
        }
    };
};
ostream & operator <<(ostream & TempOut, TestClass & TempData)
{
    TempOut << TempData.ptrMessage;
    return TempOut;
}

void ExGen()
{
    char FirstMessage[] = "message is not a part of the try block \n";
    char SecondMessage[] = "message is within the try block \n";
    TestClass TestObject1(FirstMessage, strlen(FirstMessage));
    /* This object is created outside the try block */
    try
    {
        /* The following object is created within the try block*/
        TestClass TestObject2(SecondMessage, strlen(SecondMessage));
        cout << "Inside the function \n";
        cout << "Inside try block\n";
        int dummy = 10;

        /* When the following exception is thrown, the destructor for
        TestObject would be called, which finds that the exception is not yet caught */
        throw dummy;
    }
    catch (int)
    {
        cout << "Caught dummy\n";
    }
}

/* Now the destructor for TestObject1 would be called, which finds that the exception has already been caught */
int main()
{
    ExGen();
    return 0;
}
```

