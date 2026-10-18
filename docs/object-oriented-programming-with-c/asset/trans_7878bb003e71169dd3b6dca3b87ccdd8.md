

else
    if (x == -1) throw 1.0;  // double
    cout << "End of try-block \\n";
}
catch (char c)    // Catch 1
{
    cout << "Caught a character \\n";
}
catch (int m)    // Catch 2
{
    cout << "Caught an integer \\n";
}
catch (double d)    // Catch
{
    cout << "Caught a double \\n";
}
cout << "End of try-catch system \\n\\n";
int main()
{
    cout << "Testing Multiple Catches \\n";
    cout << "x == 1 \\n";
    test(1);
    cout << "x == 0 \\n";
    test(0);
    cout << "x == -1 \\n";
    test(-1);
    cout << "x == 2 \\n";
    test(2);
    return 0;
}
程序 13.3 的输出将是：

[PAGE 567]

<!-- no content -->

[PAGE 568]

在某些情况下，我们可能无法预见所有可能的异常类型，因此可能无法设计独立的 **catch** 处理程序来捕获它们。在这种情况下，我们可以强制 **catch** 语句捕获所有异常，而不是仅捕获特定类型。这可以通过使用省略号定义 **catch** 语句来实现，如下所示：

```
catch(...)
{
    // Statements for
    processing
    // all exceptions
}
```

```
#include <iostream>
using namespace cout;
void test(int x)
{
    try
    {
    if(x == 0) throw x;    // int
    if(x == -1) throw 'x';   // char
    if(x == 1) throw 1.0;    // float
    }
    catch(...)    // catch all
    {
    cout << "Caught an exception \n";
    }
}
int main()
{
    cout << "Testing Generic Catch \n";
    test(-1);
    test(0);
    test(1);
}
```

[PAGE 569]

return 0;
}

程序 13.4 的输出将是：

Testing Generic Catch

Caught an exception

Caught an exception

Caught an exception

注意：所有抛出的异常都被 catch(...) 语句捕获了。

使用 catch( ) 作为默认语句，与其他 catch 处理程序一起使用，以便捕获所有未被显式处理的异常，这可能是一个好主意。

注意：请记住，catch(...) 应始终放在处理程序列表的最后。将它放在其他 catch 块之前会阻止这些块捕获异常。

将类类型作为异常捕获

针对不同类型的错误创建自定义对象始终是一个好做法。然后，异常处理程序可以适当地处理这些对象，以采取必要的行动。程序 13.5 演示了将类类型作为异常捕获：

程序 13.5 类类型作为异常

#include <iostream>

[PAGE 570]

```
#include <string.h>
#include <conio.h>

using namespace std;
class Error
{
    int err_code;
    char *err_desc;

    public:
    Error(int c,char *d)
    {
    err_code=c;
    err_desc=new char[strlen(d)];
    strcpy(err_desc,d);
    }
    void err_display(void)
    {
    cout<<"\nError
Code: "
    <<"err_code"\n"<<"Error
Description:
"<<"err_desc;
    }
};
int main()
{
    try
    {
    cout<<"Press any key to throw a
test exception.";
    getch();
    throw Error(99,"Test Exception");
    }
    catch(Error e)
    {
    cout<<"\nException
caught
successfully.";
    }
}
```

[PAGE 571]

```
e.err_display();
    }
    getch();
    return 0;
}
```

```
#include <iostream>

using namespace std;

void divide(double x, double y)
{
```

[PAGE 572]

```
cout << "Inside function \n";
try
{ 
if(y == 0.0)
throw y;    // Throwing double
else
cout << "Division = " << x/y << "\n";
}
catch(double)    // Catch a double
{ 
cout << "Caught double inside function \n";
throw;    // Rethrowing double
}
cout << "End of function \n\n";
}

int main()
{ 
cout << "Inside main \n";
try
{ 
divide(10.5,2.0);
divide(20.0,0.0);
}
catch(double)
{ 
cout << "Caught double inside main \n";
}
cout << "End of main \n";
return 0;
}
```

程序 13.6 的输出将是：

```
Inside main
Inside function
Division = 5.25
End of function

Inside function
Caught double inside function
Caught double inside main
End of main
```

当异常被重新抛出时，它不会被同一个 **catch** 语句或该组中的任何其他 **catch** 捕获。相反，它只会被外部的 **try/catch** 序列中的相应 **catch** 捕获。

**catch** 处理程序本身也可能检测并抛出异常。同样，抛出的异常不会被该组中的任何 **catch** 语句捕获。它将被传递给下一个外部的 **try/catch** 序列进行处理。

# 13.7 指定异常

可以限制一个函数只抛出某些指定的异常。这是通过在函数定义中添加一个 **抛出列表** 子句来实现的。使用*异常规范*的一般形式是：

```
type   function(arg-list)   throw
(type-list)
{
            .....
            ..... Function body
            .....
}
```

_type-list_ 指定可能抛出的异常类型。抛出任何其他类型的异常将导致程序异常终止。如果我们希望防止函数抛出任何异常，可以通过使 _type-list_ 为空来实现。也就是说，我们必须使用

```
throw(); // Empty list
```

> 注意：函数只能限制其抛回调用它的 try 块的异常类型。该限制仅适用于将异常抛出函数时（而不是在函数内部）。

# 程序 13.7 测试抛出限制

```
#include <iostream>

using namespace std;

void test(int x) throw(int,double)
{
    if(x == 0) throw 'x';    // char
    else
    if(x == 1) throw x;    // int
    else
    if(x == -1) throw 1.0;    // double
    cout << "End of function block \\n";
}

int main()
{
    try
    {
```

[PAGE 575]

```
cout << "Testing Throw Restrictions 

";
cout << "x == 0 \n";
test(0);
cout << "x == 1 \n";
test(1);
cout << "x == -1 \n";
test(-1);
cout << "x == 2 \n";
test(2);
}

catch(char c)
{
cout << "Caught a character \n";
}
catch(int m)
{
cout << "Caught an integer \n";
}
catch(double d)
{
cout << "Caught a double \n";
}
cout << "End of try-catch system \n
";
return 0;
```

程序 13.7 的输出将是：

+   Testing Throw Restrictions
+   x == 0
+   Caught a character
+   End of try-catch system

[PAGE 576]

# 13.8 构造函数和析构函数中的异常

在执行构造函数例程时抛出异常会发生什么？由于对象尚未完全构造，一旦程序控制离开对象的上下文，其析构函数将不会被调用。而且，如果在引发异常之前构造函数已经保留了一些内存，那么将没有机制来防止此类内存泄漏。因此，必须针对构造函数例程实施适当的异常处理机制，以处理对象构造期间发生的异常。

现在，问题来了：我们应该在哪里捕获异常？在构造函数块内部还是在 main 内部？如果我们允许在 main 内部处理异常，那么我们将无法防止前面讨论的内存泄漏情况。因此，我们必须在构造函数块内捕获异常，这样我们才有机会释放任何保留的内存空间。但是，我们必须同时重新抛出异常，以便在 main 块内得到适当的处理。下面的代码说明了这种情况：

```
class A
{
    public:
        A()
        {
            try
            {
                data-type d1;
                //Constructor code
                throw e;
            }
```

[PAGE 577]

```
catch (e)
{ 
delete d1; //Deleting the allocated memory before re
//throwing the exception
throw e;
}
```

现在来看析构函数抛出异常的情况。在析构函数块执行期间引发的异常也可能导致内存泄漏，因为析构函数可能未能在引发异常之前释放所有保留的内存空间。虽然可以在main块内处理析构函数引发的异常，但有时这可能导致程序中止。当程序控制在其引发的异常得到处理之前已经离开对象的上下文时，就可能发生这种情况。因此，建议在析构函数块内处理析构函数引发的异常，如下所示：

```
class A
{ 
public: 
A() 
{ 
. 
. 
} 
} ~A()
{ 
try
{ 
}
```

