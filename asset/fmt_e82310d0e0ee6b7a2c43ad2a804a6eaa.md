
```cpp
//11_8.cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
int main() {
    struct {
        double salary;
        char name[23];
    } employee1, employee2;
    employee1.salary=8000;
    strcpy(employee1.name,"L Zheng");
    ofstream outfile("payroll",ios_base::binary);
    outfile.write((char *) &employee1,sizeof(employee1));
    outfile.close();
    ifstream is("payroll",ios_base::binary);
    if (is) {
        is.read((char *) &employee2,sizeof(employee2));
        cout << employee2.name << ' ' << employee2.salary << endl;
    }
    else
    {
        cout << "ERROR: Cannot open file 'payroll'." << endl;
    }
    is.close();
}
```

数据记录使用定义的结构体进行格式化，且没有输入终止符或换行符。

程序的运行如下：

![](img/5618306d085ac1bac8275d6c4c5bbf2a_479_0.png)

## 6. seekg 和 tell 函数

输入文件流维持一个内部指针，指向下一个要读取的数据的位置。`seekg` 函数用于设置此指针。

### 示例 11.9: 使用 `seekg` 函数设置位置指针。

```cpp
//19.cpp
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
    char ch;
    ifstream tfile("payroll",ios_base::binary);
    if(tfile)
    {
        tfile.seekg(8);
        while (tfile.good())
        //结束读取操作直到文件结束或读取操作失败
        tfile.get(ch);
        if (!ch) break; // 如果没有读取则退出循环
        cout << ch;
    }
    else
    {
        cout << "ERROR: Cannot open file 'payroll'." << endl;
    }
    tfile.close();
}
```

`seekg` 函数可用于实现对象管理系统。文件最后一个字节的位置可以通过固定长度记录的大小乘以记录总数来确定。根据此数值，可以使用 `get` 读取记录。

成员函数 `tellg` 返回当前读取指针的位置；其值类型为 `streampos`。

### 示例 11.10: 读取文件并显示内部空白的位置。

```cpp
//11_10.cpp
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
    char ch;
    ifstream tfile("payroll",ios_base::binary);
    if (tfile)
    {
        while (tfile.good())
        {
            streampos pos = tfile.tellg();
            tfile.get(ch);
            if (!ch) break;
            if (ch == ' ')
                cout << "blank at " << pos << endl;
        }
    }
    else
    {
        cout << "ERROR: Cannot open file 'payroll'." << endl;
    }
    tfile.close();
}
```

## 11.4 输入/输出流

`iostream` 类是所有输入输出流的基类。它同时继承自 `istream` 和 `ostream`，这意味着它同时支持输入和输出操作。`iostream` 最常用的成员函数是 `>>` 和 `<<` 运算符，它们用于格式化输入和输出。

# 466 11 I/O 流库与输入/输出

```cpp
ifstream infile("employee.txt", ios_base::in);
//建立一个输入文件对象

for(i=0;i<4;i++)
{
    infile.getline(line, 100);
    cout<<line<<endl;
}
infile.close();
}
```

程序的运行结果如下：

| 请输入下一个员工姓名：Zhang |

| 请输入下一个员工姓名：Wang |

| 请输入下一个员工姓名：Li |

| 请输入下一个员工姓名：Zhao |

| 请输入兼职技员 Wang 本月的工作时长：40 |

| 月薪：40000 |

| 请输入销售员 Zhao 本月的销售额：40000 |

| 员工信息已存储 |

从文件中读取信息并显示：

Zhang 编号 1000 级别:4，本月工资：8000

Wang 编号 1001 级别：3，本月工资：4000

Li 编号 1002 级别：3，本月工资：7000

Zhao 编号 1003 级别：1，本月工资：1600

程序将存储在 vector 中的员工信息写入文件，并显示这些信息。

# 11.6 总结

在本章中，我们首先引入了流的概念，然后介绍了流类库的结构和用法。C++ 语言中没有输入/输出语句，但在 C++ 编译系统中有一个面向对象的 I/O 软件包，即 I/O 流类库。流是 I/O 流类库的核心概念。它负责连接数据的生产者和消费者，并管理数据流。程序将流对象视为文件对象的一种形式。

输出流对象是信息流的目标。三个最重要的输出流是 `ostream`、`ofstream` 和 `stringstream`。

输入流对象是数据流的源头。三个重要的流是 `istream`、`ifstream` 和 `stringstream`。

`iostream` 对象是数据的源头或目的地。两个重要的 I/O 类 `fstream` 和 `stringstream` 派生自 `iostream`。

我们只介绍了流类库的概念和简单应用。读者应该参考类库参考手册或在线帮助来获取更多细节。

# 习题

11.1 什么是流？什么是流的提取和插入？C++ 中 I/O 流的作用是什么？

11.2 `cerr` 和 `clog` 之间有什么区别？

11.3 使用 I/O 流模式创建一个名为 `test.txt` 的文件，写入字符 `"Write files successfully!"`，并用其他文本处理程序（如 Windows 中的记事本）打开它，检查写入是否正确。

11.4 使用 I/O 流文本模式打开上述创建的 `test.txt` 文件，读取内容，并在如果正确的情况下显示。

11.5 使用 I/O 流文本模式打开上述创建的 `test.txt` 文件，在文件后添加字符 `"Add characters successfully!"`，读取整个文件并在如果正确的情况下显示内容。

11.6 定义一个类 `dog`，包括两个成员变量 `weight`、`height` 以及它们对应的成员函数。

11.7 使用 I/O 流模式创建一个名为 `test.txt` 的文件，写入字符 `"Write files successfully!"`，并用其他文本处理程序（如 Windows 中的记事本）打开它，检查写入是否正确。

```cpp
{
  cout<<"except of dividing zero.\n";
  cout<<"that is ok.\n"
}
int Div(int x,int y)
{
  if(y==0)
    throw y;
  return x/y;
}
```

程序的运行结果如下：

| 5/2=2 \ except of dividing zero. that is ok. |

我们可以从结果中看到，当执行以下语句时，`Div` 函数中发生了除以零的异常。

```cpp
cout<<"8/0="<<Div(8,0)<<endl;
```

异常抛出后，它将在 `main()` 函数中被捕获。在 `try` 块中，异常处理器输出一些相关信息，然后程序跳转到 `main` 函数的最后一条语句并输出 "that is ok"。然而，`Div` 函数中的以下语句将不会执行。

```cpp
cout<<"7/1="<<Div(7,1)<<endl;
```

`catch` 句器的顺序非常重要，因为在 `try` 块中，异常处理器是按照出现顺序进行检查的。如果在 `catch` 子句中找到匹配的异常类型，则后续的 `catch` 子句将被忽略。例如，下面的异常处理块中，`catch (...)` 优先出现，它可以捕获任何异常。因此，`catch (...)` 应该始终放在最后。

```cpp
//...
try
{
  //...
}
catch( ... )
{
  //在此处处理所有异常
}
```

## 12.3 异常处理中的析构与构造 — 473

```cpp
//error: two exception handlers behind will not be checked
catch(const char * str)
{
    cout << "Caught exception: " << str << endl;
}
catch( int)
{
    //处理异常
}
```

在 VC++ 6.0 环境中，我们必须设置以下内容才能使用异常处理：

1. 打开“Project Settings”（项目设置）对话框；
2. 选择“C/C++”
3. 选择“Language”框；
4. 选择“Enable Handling”。

### 12.2.2 异常接口

为了使程序具有可读性，并让用户知道函数可能抛出的所有异常，我们可以在函数声明中列出所有可能的异常类型。例如，

```cpp
void func() throw(A, B, C, D);
```

表示 `func()` 可以调用且只能抛出类型为 A、B、D 及其子类的异常异常。如果函数声明中没有异常声明，则可以抛出任何类型的异常。例如，

```cpp
void func();
```

一个不抛出任何类型异常的函数可以声明如下：

```cpp
void func() throw();
```

### 12.3 析构与构造

C++ 异常处理的真正能力不仅在于它处理各种类型异常的能力，还在于它能够为抛出异常之前已构造的所有对象调用析构函数。在程序中，当找到匹配的 `catch` 处理器后，如果 `catch` 子句的异常声明是值参数，则其初始化模式是拷贝抛出的对象；如果 `catch` 子句的异常声明是引用，则其初始化模式是使该引用指向异常对象。

异常类型声明初始化后，将开始展开过程（unfolding）。这包含了从 `try` 块开始到抛出异常的地方所构造（且未析构）的所有自动对象的析构。析构顺序与构造顺序相反。程序将在最后一个 `catch` 处理器后恢复执行。

### 示例 12.2：使用 C++ 异常处理处理带析构函数的类

```cpp
//12_2.cpp
#include <iostream>
using namespace std;
void MyFunc();
class Expt {
public:
    Expt();
    ~Expt();
    const char *ShowReason() const
    {
        return "Expt is exceptional.";
    }
};
class Demo {
public:
    Demo();
    ~Demo();
};
Demo::Demo() {
    cout << "construct Demo." << endl;
}
Demo::~Demo() {
    cout << "destruct Demo." << endl;
}
void MyFunc() {
    Demo D;
    cout << "throw exception." << endl;
    throw Expt();
}

int main() {
  cout << "start\n";
  try {
    cout << "call MyFunc()" << endl;
    MyFunc();
  } catch (Expt& e) {
    cout << "caught exception: " << e.ShowReason() << endl;
  } catch (const char* str) {
    cout << "caught exception: " << str << endl;
  } catch (...) {
    cout << "caught unknown exception" << endl;
  }
  cout << "end\n" << endl;
  return 0;
}
```

输出结果：

```
start
call MyFunc()
throw exception.
destruct Demo.
caught exception: Expt is exceptional.
end
```

*注：由于提供的原文文本在部分似乎不完整，以上翻译基于所提供的文本片段进行。*

---

**重新审视提供的文本翻译：**

```cpp
{
  cout<<"except of dividing zero.\n";
  cout<<"that is ok.\n"
}
int Div(int x,int y)
{
  if(y==0)
    throw y;
  return x/y;
}
```

程序的运行结果如下：

| 5/2=2 \ except of dividing zero. that is ok. |

我们可以从结果中看到，当执行以下语句时，`Div` 函数中发生了除以零的异常。

```cpp
cout<<"8/0="<<Div(8,0)<<endl;
```

异常抛出后，它将在 `main()` 函数中被捕获。在 `try` 块中，异常处理器输出一些相关信息，然后程序跳转到 `main` 函数的最后一条语句并输出 "that is ok"。然而，`Div` 函数中的以下语句将不会执行。

```cpp
cout<<"7/1="<<Div(7,1)<<endl;
```

`catch` 句器的顺序非常重要，因为在 `try` 块中，异常处理器是按照出现顺序进行检查的。如果在 `catch` 子句中找到匹配的异常类型，则后续的 `catch` 子句将被忽略。例如，下面的异常处理块中，`catch (...)` 优先出现，它可以捕获任何异常。其他 `catch` 子句将永远不会被检查。因此，`catch (...)` 应该始终放在最后。

```cpp
//...
try
{
  //...
}
catch( ... )
{
  //在此处处理所有异常
}
```

## 12.3 异常处理中的析构与构造 — 473

```cpp
//error: two exception handlers behind will not be checked
catch(const char * str)
{
    cout << "Caught exception: " << str << endl;
}
catch( int)
{
    //处理异常
}
```

在 VC++ 6.0 环境中，我们必须设置以下内容才能使用异常处理：

1. 打开“Project Settings”（项目设置）对话框；
2. 选择“C/C++”
3. 选择“Language”框；
4. 选择“Enable Handling”。

### 12.2.2 异常接口

为了使程序具有可读性，并让用户知道函数可能抛出的所有异常，我们可以在函数声明中列出所有可能的异常类型。例如，

```cpp
void func() throw(A, B, C, D);
```

表示 `func()` 可以调用且只能抛出类型为 A、B、D 及其子类的异常。如果函数声明中没有异常声明，则可以抛出任何类型的异常。例如，

```cpp
void func();
```

一个不抛出任何类型异常的函数可以声明如下：

```cpp
void func() throw();
```

### 12.3 析构与构造

C++ 异常处理的真正能力不仅在于它处理各种类型异常的能力，还在于它能够为抛出异常之前已构造的所有对象调用析构函数。在程序中，当找到匹配的 `catch` 处理器后，如果 `catch` 子句的异常声明是值参数，则其初始化模式是拷贝抛出的对象；如果 `catch` 子句的异常声明是引用，则其初始化模式是使该引用指向异常对象。

异常类型声明初始化后，将开始展开过程。这包含了从 `try` 块开始到抛出异常的地方所构造（且未析构）的所有自动对象的析构。析构顺序与构造顺序相反。程序将在最后一个 `catch` 处理器后恢复执行。

### 示例 12.2：使用 C++ 异常处理处理带析构函数的类的

*注：由于后续文本存在乱码或重复，翻译已根据给定有效内容完成*
