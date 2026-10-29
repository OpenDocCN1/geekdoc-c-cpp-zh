
# TIP: (continued)

This allows you to omit names that are in the namespace but that are not used. That in turn avoids potential name conflicts. Moreover, it nicely documents which names you use, and it is not as messy as always qualifying a name with notation of the form `theSpace::f`.

If your files are structured so that different namespaces are used in different locations, it may sometimes be preferable to place your using directives and using declarations inside blocks, such as the bodies of function definitions, rather than at the start of the file.

To invoke `sample` outside the namespace `S1`, you use

```
S1::S2::sample();
```

To invoke `sample` outside the namespace `S2` but within namespace `S1`, you use

```
S2::sample();
```

Alternatively, you could use a suitable using directive.

# Self-Test Exercises

+   10. Would the program in Display 11.10 behave any differently if you replaced the four `using` declarations
+   
+   ```cpp
+   using std::cout;
+   using std::cin;
+   using std::endl;
+   using DTimeSavitch::DigitalTime;
+   ```
+   
+   with the following two using directives?
+   
+   ```cpp
+   using namespace std;
+   using namespace DTimeSavitch;
+   ```

+   11. What is the output produced by the following program?
+   
+   ```cpp
+   #include <iostream>
+   using namespace std;
+   namespace Sally
+   {
+       void message();
+   }
+   
+   namespace
+   {
+       void message();
+   }
+   ```

# Self-Test Exercises (continued)

```
int main()
{
    {
        message();
        using Sally::message;
        message();
    }
    message();
    return 0;
}

namespace Sally
{
    void message()
    {
        cout << "Hello from Sally.\n";
    }
}

namespace
{
    void message()
    {
        cout << "Hello from unnamed.\n";
    }
}
```

12. What is the output produced by the following program?

```
#include <iostream>
using namespace std;

namespace Outer
{
    void message();
    namespace Inner
    {
        void message();
    }
}
int main()
{
    Outer::message();
    Outer::Inner::message();
    using namespace Outer;
    Inner::message();
```

## 1. 项目概况

本项目旨在开发一套基于人工智能的智能文档处理系统，通过光学字符识别（OCR）、自然语言处理（NLP）及深度学习技术，实现各类纸质及电子文档的自动化识别、结构化提取与智能归档。系统将支持多格式文档输入（PDF、图片、Word等），并输出高精度的结构化数据，以提升企业文档管理效率，降低人工成本。

## 2. 技术方案

系统采用模块化架构，核心组件包括：

+   - 文档解析引擎：负责PDF、图片等文件的解析与预处理
+   - OCR识别模块：基于深度学习的中英文文字识别
+   - 信息抽取模块：利用NLP技术提取关键字段与实体
+   - 数据存储层：支持结构化数据入库及全文检索
+   - 管理后台：提供任务调度、监控及可视化报表

## 3. 实施计划

| 阶段 | 时间 | 主要任务 |
|------|------|----------|
| 需求分析 | 第1-2周 | 调研用户需求，明确功能边界 |
| 系统设计 | 第3-4周 | 架构设计、数据库设计、接口定义 |
| 核心开发 | 第5-10周 | 各模块编码与单元测试 |
| 集成测试 | 第11-12周 | 系统联调、性能优化 |
| 试运行 | 第13-14周 | 用户培训、部署上线 |

## 4. 预期成果

+   - 完成一套可用的智能文档处理系统
+   - 文档识别准确率不低于95%
+   - 单页处理时间小于2秒
+   - 提供完整的操作手册及技术文档

+   2. The name of the interface file ends in `.h`.

+   3. Only the implementation file needs to be compiled. The interface file does not need to be compiled.

+   4. Only the implementation file needs to be recompiled. You do, however, need to relink the files.

+   5. You need to delete the private member variables hour and minute from the interface file shown in Display 11.1 and replace them with the member variable minutes (with an s). You do not need to make any other changes in the interface file. In the implementation file, you need to change the definitions of all the constructors and other member functions, as well as the definitions of the overloaded operators, so that they work for this new way of recording time. (In this case, you do not need to change any of the helping functions readHour, readMinute, or digitToInt, but that might not be true for some other class or even some other reimplementation of this class.) For example, the definition of the overloaded operator, >>, could be changed to the following.

```
istream& operator >> (istream& ins,
                    DigitalTime& theObject)
{
    int inputHour, inputMinute;
    DigitalTime::readHour(inputHour);
    DigitalTime::readMinute(inputMinute);
    theObject.minutes = inputMinute + 60*inputHour;
    return ins;
}
```

You need not change any application files for programs that use the class. However, since the interface file is changed (as well as the implementation file), you will need to recompile any application files, and of course you will need to recompile the implementation file.

+   6. No. If you replace bitGreeting with greeting, you will have a definition for the name greeting in the global namespace. There are parts of the program where all the name definitions in the namespace Space1 and all the name definitions in the global namespace are simultaneously available. In those parts of the program, there would be two distinct definitions for

```cpp
void greeting();
```

+   7. Yes. The additional definition would cause no problems because overloading is always allowed. When, for example, the namespace Space1 and the global namespace are available, the function name greeting would be overloaded. The problem in Self-Test Exercise 6 was that there would sometimes be two definitions of the function name greeting with the same parameter lists.

+   8.

```text
Hello
Good-Bye
Good-Bye
```

```
9. void wow(speedway::speed s1, indy500::speed s2);
```

10. The program would behave exactly the same. However, most authorities favor using the using declaration, as we have done in Display 11.10. Note that with either, there are still two different functions named readHour. The one in Display 11.10 is different from the one defined in the unnamed namespace in Display 11.9.

```
11. Hello from unnamed.
Hello from Sally.
Hello from unnamed.
```

```
12. Outer.
Inner.
Inner.
```

# Programming Projects

+   1. This exercise is intended to illustrate namespaces and separate compilation in your development environment. You should use the development environment you regularly use in this course for this exercise. In a file f.h, place a declaration of void f() in namespace A. In a file g.h, place a declaration of void g() in namespace A. In files f.cpp and g.cpp, place the definitions of void f() and void g(), respectively. Place the definitions of void f() and void g() in namespace A. The functions can do anything you want, but to keep track of execution include something like cout << "Function_Name called" << endl; where Function_Name is the name of the particular function. In another file, main.cpp, put your main function, #include the minimum collection of files to provide access to the names from namespace A. In your main function call the functions f then g. Compile, link, and execute using your development environment. To provide access to names in namespaces, you may use local using declarations such as using std::cout; or use local using directives such as using namespace std; inside a block, or qualify names using the names of namespaces, such as std::cout. You may not use global namespace directives such as the following which are not in a block and apply to the entire file: using namespace std; Of course you must handle namespace A and function names f and g, in addition to possibly std and cout. After doing this, write a one page description of how to create and use namespaces and separate compilation in your environment.

+   2. Obtain the source code for the PFArrayD class and the demonstration program from Displays 11.10, 10.11, and 10.12. Modify this program to use namespaces and separate compilation. Put the class definition and other function declarations

in one file. Place the implementations in a separate file. Distribute the namespace definition across the two files. Place the demonstration program in a third file. To provide access to names in namespaces, you may use local using declarations such as

```
using std::cout;
```

or use local using directives such as

```
using namespace std;
```

inside a block, or qualify names using the names of namespaces, such as std::cout. You may not use global namespace directives such as the following which are not in a block and apply to the entire file:

```
using namespace std;
```

# 3. Extend Programming Project 7.1 from Chapter 7 in which you implemented a RainbowColor class by placing the class definition and implementation in a namespace, then providing access to the names in the namespace. Test your code. To provide access to names in namespaces, you may use local using declarations, such as

```
using std::cout;
```

or use local using directives such as

```
using namespace std;
```

inside a block, or qualify names using the names of namespaces, such as std::cout. You may not use global namespace directives such as the following which are not in a block and apply to the entire file:

```
using namespace std;
```

# 4. You would like to verify the credentials of a user for your system. Listed next is a class named Security, which authenticates a user and password. (Note that this example is really not very secure. Typically passwords would be encrypted or stored in a database.)

```
class Security
{
public:
    static int validate(string username, string password);
};
```

```
// This subroutine hard-codes valid users and is not
// considered a secure practice.
// It returns 0 if the credentials are invalid,
// 1 if valid user, and
// 2 if valid administrator
```

```
int Security::validate(string username, string password)
{
    if ((username=="abbott") && (password=="monday")) return 1;
    if ((username=="costello") && (password=="tuesday")) return 2;
    return 0;
}
```
