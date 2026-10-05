

```cpp
char cVar;
float fVar;
cout<<"Enter a whole number: ";
cin>>iVar;
cout<<"Enter a character: ";
cin>>cVar;
cout<<"Enter a real number: ";
cin>>fVar;
cout<<"You entered: "<<iVar<<" "<<cVar<<" "<<fVar<<";
}
/*End of cin.cpp*/
```

# 输出

Enter a whole number: 10<enter>
Enter a character: x<enter>
Enter a real number: 2.3<enter>
You entered: 10 x 2.3

就像插入运算符一样，提取运算符也可以进行级联。列表 1.14 就是一个很好的例子。

# 列表 1.14 级联提取运算符

```cpp
/*Beginning of cinCascade.cpp*/
#include<iostream.h>
void main ()
{
int x,y;
cout<<"Enter two numbers\n";
cin>>x>>y; //级联提取运算符
cout<<"You entered: "<<x<<" "<<y;
}
/*End of cinCascade.cpp*/
```

# 输出

Enter two numbers
10<enter>
20<enter>
You entered: 10 and 20

在本节的开头提到过，cin 是一个与控制关联的对象。因此，如果它是提取运算符的左侧操作数，则右侧将从键盘获取值。你将在流处理的章节中学习到，可以将某些其他与磁盘文件类似关联的类对象作为提取运算符的左侧操作数。在这种情况下，右侧的变量将从关联文件中获取值。

# 1.6 C++ 中的变量

C++ 中的变量可以在函数内部任何地方声明，而不一定在函数的最开始。例如，列表 1.15 所示。

# C++ 面对象编程

# 列表 1.15 在 C++ 中声明变量

```cpp
#include<iostream>
void main()
{
    int x;
    x=10;
    cout<<"Value of x="<<x<<endl;
    int * IPtr; //在函数中间声明变量
    IPtr=x;
    cout<<"Address of x="<<IPtr<<endl;
}
```

输出
Value of x=10
Address of x=0x21873163

# 1.7 C++ 中的引用变量

首先，让我们了解基础。操作系统（OS）如何显示变量的值？这些问题的详细解答超出了本书的范围。但是，为了更好地理解引用变量，这种研究是且必要的。操作系统在运行时为每个变量分配内存。赋值操作如 'x=y' 是是如何执行的？以下是简化的解释。

假设执行以下语句（x 和 y 是整数型变量）：

```cpp
x=y;
```

步骤如下：

- OS 找到 y 的地址。
- OS 跳转到匹配该地址的字节。
- OS 从该字节开始的四字节块中读取值（大多数 C++ 编译器在运行时使用整数型变量占据四个字节，并接受此值）。
- OS 将读取到的值推入临时栈。
- OS 找到 x 的地址。
- OS 跳转到匹配该地址的字节。
- OS 将之前放入栈中的值拷贝到以该字节开始的四字节块中（上 x）。

请注意，赋值左侧和右侧变量的地址都是确定的。然而，右侧操作数的值也是确定的。右侧表达式必须能够求出一个值。这是一个重要的点，必须牢记于心。这将使我们能够理解许多概念。

# C++ 简介

特别是你必须记住赋值运算符左侧的表达式必须是一个有效的左值（lvalue）。左值是指内存位置的表达式，可以对其进行赋值。

现在，让我们学习引用变量。引用变量仅仅是现有变量的别名。这意味着引用变量和原始变量共享内存位置。通过引用变量进行的任何更改也会更改原始变量。声明引用变量的语法如下：

```cpp
type &reference = variable;
```

例如，如果 x 是一个整数型变量，我们想为其创建一个引用：

```cpp
int x = 10;
int &ref = x;
ref = 20;
```

在这种情况下，x 的值将变为 20，因为 ref 只是 x 的另一个名字。引用变量通常用于向函数传递参数，以避免复制大对象的开销。

