

```
}
int area::calculate_area()
{
    return x*y;
}
```

输出
矩形的面积是 15

在这里，在语句 class area rectangle; 中，rectangle 是对象。要访问类中定义的函数，我们使用作用域解析运算符 (::)。在类内部声明的函数的定义语法是：

```
return_type class_name::function_name(arg1,arg2,arg3,...)
```

```
{
    //statements
}
```

以下是一个类、多个对象的示例：

```
#include<iostream>
using namespace std;
class area {
int x, y;
public:
void assign_values (int,int);
int calculate_area (void);
};
int main()
{
    class area rectangle,parallelogram;
    rectangle.assign_values(3,5);
    parallelogram.assign_values(4,2);
    cout<<"Area of rectangle is "<<rectangle.calculate_area()<<endl;
    cout<<"Area of parallelogram is "<<parallelogram.calculate_area();
    return 0;
}
```

```
void area::assign_values(int a,int b)
{
x=a;
y=b;
}
```

```
int area::calculate_area()
{
return x*y;
}
```

输出
矩形的面积是 15
平行四边形的面积是 8

类中还引入了一个功能，使上述程序更简单。这称为构造函数。

## 构造函数

关于构造函数一个令人惊叹的地方是，它与类同名。它是一个函数，一旦声明对象就会自动调用。它没有返回类型，甚至不是 void。

```
#include<iostream>
using namespace std;
class area {
int x, y;
public:
area (int,int);
int calculate_area (void);
};

int main()
{
    class area rectangle(3,5),parallelogram(4,2);
    cout<<"Area of rectangle is "<<rectangle.calculate_area()<<endl;
    cout<<"Area of parallelogram is "<<parallelogram.calculate_area();
    return 0;
}
```

```
area::area(int a,int b)
{
    x=a;
    y=b;
}

int area::calculate_area()
{
    return x*y;
}
```

输出
矩形的面积是 15
平行四边形的面积是 8

在这里，我们没有设计任何单独的函数来赋值，而是将其合并在构造函数中。仔细看，我们在声明对象时带有参数，例如 class area rectangle(3,5); 这里 3 和 5 是参数。这里，area(int,int); 是一个构造函数。

## 构造函数重载

构造函数可以像函数一样重载，我们可以定义多个构造函数，但在声明构造函数时应注意，我们只能创建参数数量与构造函数中完全相同的对象。

```
#include<iostream>
using namespace std;
class area {
int x, y;
public:
area();
area (int,int);
int calculate_area (void);
};
int main()
{
    class area rectangle;
    class area parallelogram(4,2);

    cout<<"Area of rectangle is "<<rectangle.calculate_area()<<endl;
    cout<<"Area of parallelogram is "<<parallelogram.calculate_area()<<endl;
    return 0;
}
area::area()
{
    x=y=1;
}
area::area(int a,int b)
{
    x=a;
    y=b;
}
int area::calculate_area()
{
    return x*y;
}
```

输出
矩形的面积是 1
平行四边形的面积是 8

## 默认构造函数

如果程序员没有创建任何构造函数，则会自动创建一个名为默认构造函数且无参数的构造函数。因此，我们可以创建任何无参数的对象，例如 class area rectangle，但如果我们尝试声明带有三个参数的对象，例如 class area cuboid(3,4,5)，由于相应的构造函数不存在，编译器将报错说“no matching function to call for area::area(int,int,int)”。如果我们声明了任何构造函数，编译器就不提供默认构造函数。因此，如果我们只声明了带有两个参数的构造函数，则无法创建无参数或只有一个参数的对象。要创建无参数的对象，我们还必须声明和定义相应的构造函数。

## 拷贝构造函数

当我们想要以自己的方式复制对象时，拷贝构造函数特别有用。与默认构造函数一样，拷贝构造函数很重要，重要到 C++ 认为没有哪个类应该没有拷贝构造函数。如果你不提供自己的拷贝构造函数，C++ 会为你生成一个。（这与 C++ 提供的默认构造函数不同，除非你的类为其定义了构造函数。）C++ 提供的拷贝构造函数对每个数据成员执行逐成员复制。早期版本的 C++ 提供的拷贝构造函数执行的是逐位复制。区别在于，逐成员复制会调用类成员可能存在的所有拷贝构造函数，而逐位复制则不会。
我们也可以定义自己的拷贝构造函数。
请考虑以下程序：

```
#include<iostream>
using namespace std;
class area
{
    int x, y;
public:
    area();
    area(area&);
    int calculate_area (void);
};
int main()
{
    class area rectangle;
    class area parallelogram(rectangle);
    cout<<"\nArea of rectangle is "<<rectangle.calculate_area()<<endl;
    cout<<"Area of parallelogram is "<<parallelogram.calculate_area();
    return 0;
}
area::area()
{
    x=y=1;
}
area::area(area& s)
{
    x=5;
    y=s.y;
    cout<<"Calling copy constructor";
}
int area::calculate_area()
{
    return x*y;
}
```

输出
Calling copy constructor
矩形的面积是 1
平行四边形的面积是 5

## 析构函数

就像我们调用构造函数来创建对象一样，同样可以使用析构函数来销毁对象。它也与类同名。那么，如何将其与构造函数区分开？为了将其与构造函数区分开，我们在其前面使用波浪号 (~)。与构造函数一样，它也不返回任何内容。当对象在其生命周期内分配动态内存，并在销毁时我们希望释放对象分配的内存时，析构函数的使用尤其合适。它也像构造函数一样自动调用。

请考虑以下程序：
#include<iostream>
using namespace std;

```
class area
{
int *x, *y;
public:
area (int,int);
~area();
int calculate_area (void);
};
int main()
{
    class area parallelogram(4,2);
    cout<<"Area of parallelogram is "<<parallelogram.calculate_area();
    return 0;
}
area::area(int a,int b)
{
x=new int;
y=new int;
*x=a;
*y=b;
}
area::~area()
{
delete x;
delete y;
cout<<"\nPointers deleted";
}
int area::calculate_area()
{
return *x**y;
}
```

输出
平行四边形的面积是 8
指针已删除

## 在类内部定义方法

方法也可以在类内部定义。当方法太小时，这非常有用。在类内部定义方法所使用的代码片段如下：

```
class class_name
{
    //statements
    return_type func_name(arg1,arg2,...)
{
   //statements of functions
}
};
```

因此，我们可以将之前的代码写成如下形式：

```
#include<iostream>
using namespace std;
class area
{
    int *x, *y;
    public:
    area (int a,int b)
    {
        x=new int;
        y=new int;
        *x=a;
        *y=b;
    }
    ~area()
    {
        delete x;
        delete y;
        cout<<"\nPointers deleted";
    }
    int calculate_area (void)
    {
    return *x**y;
    }
};
int main()
{
    class area parallelogram(4,2);
    cout<<"Area of parallelogram is "<<parallelogram.calculate_area();
    return 0;
}
```

输出
平行四边形的面积是 8
指针已删除

## 将类传递给函数

类可以传递给函数。将类传递给函数的定义语法如下：

```
return_type func_name(class_name object_name)
{
//Statements
}
```

请考虑以下程序：

```
#include<iostream>
using namespace std;
class student
{
    public:
    char name[50];
    char section;
    int roll;
    void read_data();
};
void display_data(student);
void student::read_data()
{
    cout<<"Enter the name\n";
    cin.getline(name,50);
    cout<<"Enter the section\n";
    cin>>section;
    cout<<"Enter the roll number\n";
    cin>>roll;
}
int main()
{
    class student s1;
    s1.read_data();
    display_data(s1);
}
void display_data(student x)
{
    cout<<"Name of the student is: ";
    cout<<x.name;
    cout<<"\nThe section of the student is: ";
    cout<<x.section;
    cout<<"\nThe roll number of the student is: ";
    cout<<x.roll;
}
```

输出
Enter the name
Aman Kumar Jha
Enter the section
D
Enter the roll number

