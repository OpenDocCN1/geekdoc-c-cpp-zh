Note that C++ does not catch a divide by zero exception by default. The code will crash when a divide by zero situation occurs. As a result, the only option is to write a class or method to handle divide by zero case. The following example shows how to handle the divide by zero situation and how to construct an exception:

```
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
        cout<<"1. (500/10) = "<<d.quotient(100, 10)<<endl;
        cout<<"2. (15/6) = "<<d.quotient(10, 4)<<endl;
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
```

The output of the preceding program is as follows:

```
```text
1. (500/10) = 50
2. (15/6) = 2.5
Exception caught with cause: Divide by 0 exception
```
```

Let’s now discuss the mechanics of exception handling.

# Exception Handling – Mechanics

Whenever an exception is thrown, it is caught by the corresponding catch declaration, which processes the exception. There can be several catch statements for a try; which catch statement can be used will be determined by the kind of exception. That is, if the data type specified within a catch matches with that of the exception, then all the other catch statements are bypassed. When an exception is captured, the argument specified within the catch clause will have the exception. Any kind of data may end up being caught, including the classes that are created. If absolutely no exception is thrown, then no catch statement is executed. If a match is found, the catch handler’s code is executed and control resumes at the point after the catch handlers.