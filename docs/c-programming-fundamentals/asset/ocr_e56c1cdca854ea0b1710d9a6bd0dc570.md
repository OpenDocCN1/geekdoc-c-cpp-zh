# Code Debriefing

+   - In this code, the addition function of our class exists in multiple forms.
+   - This type of polymorphism is implemented using the function overloading of the addition method.
+   - The functions all have the same name, but different signatures. That is, they have different combinations and numbers of parameters.
+   - While calling the display function, keep in mind which signature calls which function.

# 7.2 Dynamic vs. Static Binding

Table 7.1 Dynamic and static binding

| Dynamic Binding | Static Binding |
|---|---|
| Dynamic or late binding tells which procedure will be called at runtime. | Static or early binding tells which procedure will be called at compile time. |
| The code inside our procedure is not known until execution, hence the name late binding. | The code inside our procedure is known before execution, and both join together at execution time, hence the name early binding. |
| It is implemented in C++ using virtual functions. | It is implemented in C++ using normal function calls, function overloading, and operator overloading. |
| The execution of a program is slower. | The execution of a program is faster. |
| Runtime polymorphism is also another name for it. | Compile-time polymorphism is also another name for it. |

# Code: Static binding

```
#include <iostream>
using namespace std;
class person
{
    public:
    int age;
    void display1()
    {
        cout<<"Enter your age"<<endl;
        cin>>age;
    }
```