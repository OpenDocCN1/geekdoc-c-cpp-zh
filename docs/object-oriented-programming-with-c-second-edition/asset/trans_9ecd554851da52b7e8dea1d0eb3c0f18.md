

## 11.2 C 风格的错误生成代码处理

让我们学习一个函数 `hmean()`，它接受两个浮点型数字作为参数，并计算它们的调和平均数。请参见列表 11.1。

列表 11.1 计算调和平均数的函数

```cpp
float hmean(const float a, const float b)
{
    return 2.0*a*b/(a+b);
}
```

显然，“a” 和 “b”不应该互为相反，否则会导致除以零。应该尽力防止在 “a” 和 “b” 互为相反时对返回表达式进行评估以及随之而来的运行时错误。针对这个问题有三种传统的 C 风格解决方案：

- 终止程序
- 在函数调用前检查参数
- 返回一个表示错误的错误值

这些方法将在下文中讨论。

## 11.2.1 终止程序

让我们来看这种解决方案（列表 11.2）。

列表 11.2 当满足错误条件时终止程序

```cpp
/*Beginning of hmean.h*/
float hmean(const float a, const float b);
/*End of hmean.h*/

/*Beginning of hmean.cpp*/
#include<stdlib.h> // for abort()
float hmean(const float a, const float b)
{
    if(a==b)
        abort();
        return 2.0*a*b/(a+b);
}
/*End of hmean.cpp*/

/*Beginning of hmeanmain.cpp*/
#include<iostream.h>
#include"hmean.h"
void main()
{
    float x,y,z;
    cout<<"Enter a number: ";
    cin>>x;
    cout<<"Enter another number: ";
    cin>>y;
    z=hmean(x,y);
```

```cpp
cout<<"Harmonic mean = "<<z<<endl;\n}
/*End of hmean.cpp*/
```

# 输出

Enter a number: 10
Enter another number: -10
Abnormal program termination

这种终止程序的解决方案（如列表 11.2 所示）过于极端和剧烈。库函数在检测到无效输入时简单地终止程序。即使我们不提供 `abort()` 函数，操作系统也会抛出类似或相同的错误（取决于实现方式）并终止程序。这种解决方案没有产生任何实质性的结果。库用户没有机会采取其选择的纠正措施。库完全可以并且做得更好。

## 11.2.2 在函数调用前检查参数

列表 11.3 给出一个用于验证函数参数的程序。

- 列表 11.3 验证函数参数以避免错误条件

```cpp
/*Beginning of hmean.h*/
float hmean(const float, const float);
/*End of hmean.h*/
/*Beginning of hmean.cpp*/
#include "hmean.h"
float hmean(const float a, const float b)
{
    return 2.0*a*b/(a+b);
}
/*End of hmean.cpp*/
/*Beginning of hmeanmain.cpp*/
#include <iostream>
#include "hmean.h"
void main()
{
    float x,y,z;
    while(1)
    {
        cout<<"Enter a number: ";
        cin>>x;
        cout<<"Enter another number: ";
        cin>>y;
        if(x!=-y)
        {
            break;
        }
        cout<<"Invalid entry - enter again\n";
    }
    z=hmean(x,y);
    cout<<"Harmonic mean = "<<z<<endl;
}
```

# 输出

Enter a number: 3
Enter another number: -3
Invalid entry - enter again
Enter a number: 2
Enter another number: 6
Harmonic mean = 3

这种方法依赖于应用程序程序员在将数据作为参数传递给函数调用之前对其进行预验证。然而，依赖应用程序程序员有足够的了解（或足够关心）来执行此类检查是不够安全的。一个设计良好的库函数不需要、也不应该让用户负担起检查所有无效条件下的参数的任务。

## 11.2.3 返回一个表示错误的值

另一种方法是使用函数的返回值来指示问题。让我们使用指针参数或引用参数将一个值返回给调用程序，并使用函数的返回值来指示成功或失败。通过通知调用函数成功或失败，我们为程序员提供了采取其选择的适当行动的选择。列表 11.4 显示了这种方法的示例。它重新定义了 `hmean()` 函数为一个 `int` 函数，其返回值指示成功或失败。它添加了第三个参数来获取答案。

- 列表 11.4 从库函数返回错误条件

```cpp
/*Beginning of hmean.h*/
int hmean(const float, const float, float const *);
/*End of hmean.h*/

/*Beginning of hmean.cpp*/
#include"hmean.h"
int hmean(const double a, const double b,double const * c)
{
  if(a==-b){
    *c = 0;
    return 0; // failure
  }
  else{
    *c=2.0*a*b/(a+b);
    return 1; // success
  }
}
/*End of hmean.cpp*/
/*Beginning of hmeanmain.cpp*/
#include<iostream.h>
#include"hmean.h"
void main()
{
    float x,y,z;
    while(1)
    {
        cout<<"Enter a number: ";
        cin>>x;
        cout<<"Enter another number: ";
        cin>>y;
        if(hmean(x,y,&z)==1)
            break;
        cout<<"Invalid entry - enter again\n";
    }
    cout<<"Harmonic mean = "<<z<<endl;
}
```

# 输出

Enter a number: 3
Enter another number: -3
Invalid entry - enter again
Enter a number: 2
Enter another number: 6
Harmonic mean = 3

