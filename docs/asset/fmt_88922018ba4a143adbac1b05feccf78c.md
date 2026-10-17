
```cpp
#include <iostream>
using namespace std;
void Division(const double a, const double b);
int main()
{
    double op1=0, op2=10;
    try
    {
        Division(op1, op2);
    }
    catch (const char* Str)
    {
        cout << "\nBad Operator: " << Str;
    }
    return 0;
}
void Division(const double a, const double b)
{
    double res;
    if (b == 0)
        throw "Division by zero not allowed";
    res = a / b;
    cout << res;
}
```

- a. `0`

- b. 错误运算符

- c. `10`

- d. `15`

### 36. 以下 C++ 代码的输出是什么？

```cpp
#include <stdexcept>
#include <limits>
#include <iostream>
using namespace std;
void MyFunc(char c)
{
    if (c < numeric_limits<char>::max())
        return invalid_argument;
}
int main()
{
    try
    {
        MyFunc(256);
    }
    catch(invalid_argument& e)
    {
        cerr << e.what() << endl;
        return -1;
    }
    return 0;
}
```

- a. `256`

- b. 无效参数

- c. 错误

- d. `246`

```cpp
cout << "Standard exception: " << e.what() << endl;
}
return 0;
}
```

- a. 已分配

- b. 标准异常：

- c. `bad_alloc`

- d. 取决于内存

### 39. 以下 C++ 代码的输出是什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
    char* ptr;
    unsigned long int a = (size_t(0) / 3);
    cout << a << endl;
    try
    {
        ptr = new char[size_t(0) / 3];
        delete[] ptr;
    }
    catch(bad_alloc &thebadallocation)
    {
        cout << thebadallocation.what() << endl;
    };
    return 0;
}
```

- a. `0`

- b. `2`

- c. `bad_alloc`

- d. 取决于编译器

### 40. 以下 C++ 代码的输出是什么？

```cpp
#include <typeinfo>
#include <iostream>
using namespace std;
class shape
{
public:
    virtual void myvirtualfunc() const {}
};
class mytriangle: public shape
{
    public:
    virtual void myvirtualfunc() const
    {
    };
};
int main()
{
    shape shape_instance;
    shape &ref_shape = shape_instance;
    try
    {
        mytriangle &ref_mytriangle = dynamic_cast<mytriangle&>(ref_shape);
    }
    catch (bad_cast)
    {
        cout << "Caught: bad_cast exception\n";
    }
    return 0;
}
```

- a. 捕获到标准异常

- b. 没有产生异常

- c. 捕获到：`bad_cast` 异常

- d. 捕获到：`cast`

### 41. 以下 C++ 代码的输出是什么？

```cpp
#include <typeinfo>
#include <iostream>
using namespace std;
class Test
{
    public:
    Test();
    virtual ~Test();
};
int main()
{
    Test *ptrvar = NULL;
    try
    {
        cout << typeid(*ptrvar).name() << endl;
    }
    catch (bad_typeid)
    {
        cout << "The object is null" << endl;
    }
    return 0;
}
```

- a. 没有产生异常

- b. 对象为空

- c. 错误

- d. 对象为

### 42. 给定代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;

        if (B == 0)
            throw 2;

        C = A / B;
    }
    catch (int num) {
        cout << "Error code: " << num << endl;
    }
    return 0;
}
```

- a. 错误代码：`2`

- b. 语法错误

- c. 没有输出

- d. 垃圾值

### 43. 给定代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;
        C = A / B;
    }
    catch (exception e) {
        cout << "Exception generated" << endl;
    }
    return 0;
}
```

- a. 生成了异常

- b. 语法错误

- c. 没有输出

- d. 程序在运行时崩溃

### 44. 给定代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;

        if (B == 0)
            throw "divide by zero";
        C = A / B;
    }
    catch (char* e) {
        cout << "Exception Received: " << e << endl;
    }
    return 0;
}
```

- a. 收到异常：除以零

- b. 语法错误

- c. 没有输出

- d. 程序在运行时崩溃

### 45. 给定代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;

int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;

        if (B == 0)
            throw "divide by zero";
        C = A / B;
    }
    catch (const char* e) {
        cout << "Exception Received: " << e << endl;
    }
    return 0;
}
```

- a. 收到异常：除以零

- b. 语法错误

- c. 没有输出

- d. 程序在运行时崩溃

### 46. 给定代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;

        if (B == 0)
            throw "Divide by zero";
        C = A / B;
    }
    catch (int num) {
        cout << "Error Code: " << num << endl;
    }
    catch (...) {
        cout << "Exception received" << endl;
    }
    return 0;
}
```

- a. 收到异常

- b. 除以零

- c. 语法错误

- d. 没有输出

### 47. 给定代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;

int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;

        if (B == 0) {
            Exception E;
            throw E;
        }
        C = A / B;
    }
    catch (exception E) {
        cout << "Exception Received" << endl;
    }

    return 0;
}
```

- a. 收到异常

- b. 除零错误

- c. 语法错误

- d. 无输出

### 48. 以下代码片段的正确输出是什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;

        if (B == 0) {
            exception E;
            throw E;
        }
        C = A / B;
    }
    catch (exception E) {
        cout << "Exception Received" << endl;
    }
    return 0;
}
```

- a. 收到异常

- b. 除零错误

- c. 语法错误

- d. 无输出

### 49. 以下代码片段的正确输出是什么？

```cpp
#include <iostream>
using namespace std;

int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;
        if (B == 0) {
            bad_exception E;
            throw E;
        }
        C = A / B;
    }
    catch (bad_exception E) {
        cout << "@@@Exception Received" << endl;
    }
    catch (exception E) {
        cout << "###Exception Received" << endl;
    }
    return 0;
}
```

- a. ###收到异常

- b. @@@收到异常

- c. 语法错误

- d. 无输出

## 多项选择题

| 1. (a) | 2. (b) | 3. (a) | 4. (a) | 5. (b) | 6. (a) | 7. (d) | 8. (a) | 9. (b) | 10. (c) |

| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

| 11. (d) | 12. (c) | 13. (d) | 14. (c) | 15. (c) | 16. (c) | 17. (b) | 18. (b) | 19. (c) | 20. (d) |

| 21. (d) | 22. (b) | 23. (c) | 24. (c) | 25. (c) | 26. (d) | 27. (a) | 28. (a) | 29. (b) | 30. (a) |

| 31. (b) | 32. (a) | 33. (b) | 34. (a) | 35. (a) | 36. (c) | 37. (b) | 38. (d) | 39. (a) | 40. (a) |

| 41. (b) | 42. (a) | 43. (d) | 44. (d) | 45. (a) | 46. (a) | 47. (c) | 48. (a) | 49. (a) | 50. (a) |

| 51. (b) |  |  |  |  |  |  |  |  |  |

## 参考资料

### 图书

- B. Stroustrup, *C++程序设计语言*（第4版）（Addison-Wesley Professional，2013年）。

- K. R. Venugopal, *精通C++*（第2版）（McGraw Hill Education，2017年7月）。

- Y. Kanetkar, *让我们学C++*（BPB Publications，2020年9月）。

- Y. Kanetkar, *测试你的C++技能*（BPB Publications，2003年3月）。

### 网站

- Learn CPP，2022年8月访问，`https://www.learncpp.com`

- Codes Cracker，2022年8月访问，`https://codescracker.com`

- Roll Bar，2022年8月访问，`https://rollbar.com`

- Geeks For Geeks，2022年8月访问，`https://www.geeksforgeeks.org`

- Udacity，2022年8月访问，`https://www.udacity.com`

- Scaler，2022年8月访问，`https://www.scaler.com`

- C Plus Plus，2022年8月访问，`https://cplusplus.com`

- Silly Codes，2022年8月访问，`https://sillycodes.com`

# 第11章 文件处理

## 11.1 文件与流

整理和维护我们的物品有助于我们在需要时轻松获取它们，桌面文件夹和手机数据也是如此。一切都需要整理和高效处理。在C++中，我们处理和组织文件、文件夹和目录。我们可以编写自己的文件，并在创建的文件中显示内容。C++中的文件究竟是什么？让我们用简单的术语来定义它。

### 文件

在C++中创建的文件有助于将数据存储到硬盘上，并保留在系统中以供以后使用。这与传统程序不同，在传统程序中，我们的数据或保存数据的对象会在程序终止后被删除，以回收分配的临时内存空间。很多时候，我们需要将数据安全地存储在系统中，这样从文件中取出条目所需的时间会更少。

### 流

为了让用户输入和提供详细信息或值，我们使用输入流。流是指一组可以按顺序访问的字节。有两种不同类型的流。*输入流*用于保存来自用户的输入，例如键盘输入。例如，用户可能会按下键盘上的任意键，即使没有被要求这样做。在类似这样的情况下

### 代码：处理文件和流
