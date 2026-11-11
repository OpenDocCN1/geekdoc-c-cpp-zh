
```cpp
}
void get_data()
{
    cout<<"enter the meters:";
    cin>>m;
    cout<<"enter the centimeters";
    cin>>cm;
}
void convers1()
{
    cm=m*100+cm;
    m=cm/100;
}
friend float add(dm,db);
};

class db
{
 private:
  float feet;
  float inches;
 public:
  db():feet(0.0),inches(0.0)
  {}

  void get_data1()
  {
   cout<<"enter the feet";
   cin>>feet;
   cout<<"enter the inches";
   cin>>inches;
  }

  void convers2()
  {
   inches=feet*12+inches;
   feet=inches/12;
  }
  friend float add(dm,db);
};

float add(dm m1,db feet1)
{
 return(m1.m*3.3+feet1.feet);
}

int main()
{
 dm d1;
 db d2;
 d1.get_data();
 d2.get_data1();
 d1.convers1();
 d2.convers2();
 cout<<add(d1,d2);
 return 0;
}
```

### 输出：

```text
enter the meters:10
enter the centimeters30
enter the feet50
enter the inches12
84.989998
```

![](img/8a6886c00caa6a1651a6c0e62bff341f_376_0.png)

借助一个合适的程序，以复制构造函数为例说明带动态操作的构造函数。

下面探讨如何在类中声明和使用析构函数。

## 声明和使用析构函数

在 C++ 中，如果不再需要某个对象，可以使用析构函数销毁它。析构函数是类的另一种特殊成员函数。它被调用来销毁类的一个对象。析构函数的名称与类名相同，但前面带有一个波浪号（~）符号。波浪号符号将其与同一类的构造函数区分开来。清单 19 展示了如何在类中声明析构函数（可在随书光盘的 code\\chapter6 文件夹中的 SimpleDestructor.cpp 文件中找到此示例）：

### 清单 19：声明析构函数

```cpp
#include<iostream.h>

class NumberInitialization
{
  int x,y;
  public:
  NumberInitialization();  //constructor prototype
  ~NumberInitialization(); //destructor prototype
};
NumberInitialization::NumberInitialization()
{
  cout<<"Default constructor calling"<<endl;
  x=1;
  y=2;
  cout<<"x="<<x<<endl;
  cout<<"y="<<y<<endl;
}
NumberInitialization::~NumberInitialization()
{
    cout<<"Destructor calling"<<endl;
    x=0;
    y=0;
    cout<<"x="<<x<<endl;
    cout<<"y="<<y<<endl;
}
int main()
{
    NumberInitialization n1;
    cout<<"Program Over\n";
    return 0;
}
```

### 输出：

```text
Default constructor calling
x=1
y=2
Program Over
Destructor calling
x=0
y=0
```

如果对象是局部非静态变量，那么当定义该对象的函数即将结束时，就会调用析构函数。但是，如果对象是静态变量或全局变量，则析构函数会在程序终止之前调用。此外，当程序通过调用 `exit()` 函数中断时，此时退出的所有对象的析构函数都会被调用。

![](img/8a6886c00caa6a1651a6c0e62bff341f_377_0.png)

> *析构函数可以显式调用，如下面的代码片段所示：*
>
> ```cpp
> n1.~NumberInitialization();       // Explicit destructor invocation
> ```

不过，析构函数不必显式调用，因为当对象超出作用域时系统会自动调用它。

析构函数具有以下特征：

- 析构函数的名称必须与其类名相同
- 析构函数在类声明中应具有公有访问权限
- 析构函数没有返回类型，因此不能返回值
- 析构函数可以是 `virtual`
- 每个类中只能有一个析构函数。这是因为销毁对象只有一种方式。
- 析构函数不接受参数，因此不能被重载。

可以使用类的构造函数通过 new 运算符分配内存，并使用类的析构函数通过 delete 运算符释放内存。清单 20 展示了构造函数和析构函数分别使用 new 和 delete 运算符（可在随书光盘的 code\chapter6 文件夹中的 Cons_Deleting.cpp 文件中找到此示例）：

### 清单 20：在类的构造函数和析构函数中使用 new 和 delete 运算符

```cpp
#include<iostream.h>
#include<string.h>

class String
{
char *str;
int strlength;
public:
String();
String(char*);
~String();
};
String::String()
{
strlength=0;str=new char[strlength + 1];
str[0]='\0';
cout<<"Default constructor calling : "<<str<<endl;
}
String::String(char *s)
{
strlength=strlen(s) ;
str=new char[strlength+1];
strcpy(str,s);
cout<<"Parameterized constructor calling : "<<str<<endl;
}
String::~String()
{
delete str;
cout<<"Destructor calling : "<<"Object deleted"<<endl;
}
void main()
{
String s1("Object 1"),s2("Object 2"),s3;
}
```

### 输出：

```text
Parameterized constructor calling : Object 1
Parameterized constructor calling : Object 2
Default constructor calling :
Destructor calling : Object deleted
Destructor calling : Object deleted
Destructor calling : Object deleted
```

在清单 20 中，String 是一个类，它有一个 str 变量，该变量是指针类型的字符变量。在 String 类中，我们声明以下内容：

- `String()`：表示默认构造函数，使用 new 运算符为 str 变量分配内存
- `String(char *s)`：表示带参数的构造函数，使用 new 运算符为 str 变量分配内存
- `~String()`：表示析构函数，使用 delete 运算符释放 str 变量的内存

在 main() 函数中，创建了 String 类的三个对象：object1、object2 和 object3。object1 和 object2 对象调用 String(char *s) 构造函数，并显示相应消息。但是，object3 调用 String() 构造函数，并且不显示 str 变量中存储的任何字符串。String() 析构函数被调用三次，分别对应 String 类的每个对象。

现在说明如何全局调用类的构造函数和析构函数。

## 调用全局构造函数和析构函数

类的对象可以在程序中借助全局变量定义为全局对象。全局对象在进入 main() 函数之前创建，并在 main() 函数退出之后销毁。全局对象的这种创建和销毁是通过调用全局构造函数和全局析构函数完成的。清单 21 展示了如何调用全局构造函数和全局析构函数（可在随书光盘的 code\chapter6 文件夹中的 GlobalConsDest.cpp 文件中找到此示例）：

### 清单 21：全局调用类的构造函数和析构函数

```cpp
#include<iostream.h>
class ConsDesCall
{
public:
  ConsDesCall()
  {
    cout<<"Constructor called"<<endl;
  }
  ~ConsDesCall()
  {
    cout<<"Destructor called"<<endl;
  }
};
ConsDesCall o1;
int main()
{
    cout<<"Main begins"<<endl;
    ConsDesCall o2;
    {
        cout<<"Inner block begins"<<endl;
        ConsDesCall o3;
        cout<<"Inner block ends"<<endl;
    }
    cout<<"Main ends"<<endl;
    return 0;
}
```

### 输出：

```text
Constructor called
Main begins
Constructor called
Inner block begins
Constructor called
Inner block ends
Destructor called
Main ends
Destructor called
Destructor called
```

在清单 21 中，随着 ConsDesCall 类的各个实例的创建而调用的构造函数和析构函数的顺序解释如下：

对象 o1 具有全局作用域，其构造函数在 main() 函数开始执行之前执行。对象 o2 具有函数作用域或局部作用域，其构造函数在 main() 函数开始执行之后执行。对象 o3 具有块作用域，其构造函数在内层块开始执行之后执行。当内层块执行结束时，调用 o3 对象的析构函数。当 main() 函数执行结束时，调用 o2 对象的析构函数。当程序结束时，调用 o1 对象的析构函数，因为该对象被声明为全局变量。

下面探讨 C++ 中的局部类和嵌套类。

## 6.7 探讨局部类和嵌套类

在 C++ 中，可以将一个类包含在另一个类中。将一个类包含在另一个类中的任务可以通过以下两种方式完成：

