

## 处理错误

可以通过包含 C++ 标准 `<typeinfo>` 库来提供异常类型信息。其 `typeid()` 函数接受一个异常参数，以便其 `name()` 函数可以返回类型名称：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_93_0.png)

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀来启动一个新程序

```cpp
#include <stdexcept> // 支持标准异常。
#include <typeinfo> // 支持类型信息。
#include <fstream>
#include <string>
#include <iostream>
using namespace std ;
```

- 2. 添加一个主函数，其中包含一个最终的返回语句、两个已初始化的变量声明，以及一个输出文本消息的语句

```cpp
int main()
{
   string lang = "C++" ;
   int num = 1000000000 ; // 十亿。
   // try-catch 块放在这里。
   cout << "Program continues..." << endl ;
   return 0 ;
}
```

- 3. 在主函数中，插入一个 try 块，其中包含一条尝试替换字符串值部分的语句

```cpp
try { lang.replace( 100, 1 , "C" ) ; }
```

- 4. 在 try 块之后，添加一个 catch 块来处理范围异常，然后保存、编译并运行程序

```cpp
catch( out_of_range &e )
{
   cerr << "Range Exception: " << e.what() << endl ;
   cerr << "Exception Type: " << typeid(e).name() ;
   cerr << endl << "Program terminated." << endl ;
   return -1 ;
}
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_93_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_93_2.png)

出现 `out_of_range` 错误是因为 `replace()` 函数试图从第 100 个字符处开始删除，但该 `string` 变量只有三个字符。

- 5. 将 try 块中的语句替换为一条尝试调整字符串变量大小的语句

```cpp
lang.resize( 3 * num ) ;
```

- 6. 在 catch 块之后，添加第二个 catch 块来处理一般异常

```cpp
catch ( exception &e )
{
    cerr << "Exception: " << e.what() << endl ;
    cerr << "Exception Type: " << typeid( e ).name() << endl ;
}
```

- 7. 再次保存、编译并运行程序，以查看由第二个 **catch** 块处理的异常

![](img/bf8dbdfb89042fadbaa73b4160c74bac_94_0.png)

- 8. 将 **try** 块中的语句替换为一条尝试打开不存在文件的语句

```cpp
ifstream reader("nonsuch.txt");
if( ! reader ) throw logic_error("File not found");
```

- 9. 再次保存、编译并运行程序，以查看再次由第二个 catch 块处理的异常，以及指定的自定义错误消息

![](img/bf8dbdfb89042fadbaa73b4160c74bac_94_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_94_2.png)

**catch** 块的顺序可能很重要——将 **exception** 错误处理器放在 **out_of_range** 错误处理器之前，会使 **out_of_range** 错误被（更高级的）**exception** 处理器处理。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_94_3.png)

异常对象通常被命名为“e”——正如这里所见。

## 6 指向数据

*本章演示如何利用指针和引用编写高效的 C++ 程序。*

- 理解数据存储
- 使用指针获取值
- 执行指针运算
- 将指针传递给函数
- 创建指针数组
- 引用数据
- 将引用传递给函数
- 比较指针与引用
- 总结

### 理解数据存储

为了理解 C++ 指针，了解数据在计算机中的存储方式会很有帮助。可以把计算机的内存想象成一行极长、按顺序编号的插槽，每个插槽可以容纳一个字节的数据。当程序中声明一个变量时，机器会预留一些插槽来存储分配给该变量的数据。预留的插槽数量取决于变量的数据类型。当程序使用变量名来检索存储的数据时，它实际上是在寻址该变量第一个预留插槽的编号。

可以将其比作一排按顺序编号的房子，每栋房子可以容纳不同的家庭。任何家庭都可以通过其房子编号被明确引用。

计算机内存中的插槽（房子）编号以十六进制格式表示，可以通过 & 引用运算符来显示。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_97_0.png)

address.cpp

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀来启动一个新程序。

```cpp
#include <string>
#include <iostream>
using namespace std;
```

- 2. 添加一个主函数，其中包含一个最终的 **return** 语句，并声明三个已初始化的变量。

```cpp
int main()
{
    int num = 100;
    double sum = 0.0123456789;
    string text = "C++ Fun";
    // 在这里添加更多语句。
    return 0;
}
```

- 3. 在主函数中，插入语句以输出每个变量的第一个槽的内存地址。

```cpp
cout << "Integer variable starts at: " << &num << endl;
cout << "Double variable starts at: " << &sum << endl;
cout << "String variable starts at: " << &text << endl;
```

- 4. 保存、编译并运行程序以查看这三个内存地址。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_97_1.png)

一旦变量声明预留了内存空间，就可以使用 **=** 赋值运算符将适当数据类型的一个值存储到该空间中。例如，**num = 100** 取其右侧的值（**100**）并将其放入左侧命名变量（**num**）所引用的内存中。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_98_0.png)

这些位置地址是动态分配的——因此会与截图中的地址有所不同。

**=** 赋值运算符左侧的操作数称为其“L-value”（左值），右侧的操作数称为其“R-value”（右值）。可以把 L-value 中的“L”理解为“Location”（位置），把 R-value 中的“R”理解为“Read”（读取）。

C++ 编程中一条重要的规则强调：R-value 不能出现在 **=** 赋值运算符的左侧，但 L-value 可以出现在任一侧。将 R-value 放在 **=** 赋值运算符左侧的代码将无法编译：

- 5. 在 `return` 语句之前，插入将 R-value 错误地放在赋值运算符左侧的语句

```cpp
200 = num ;
5.5 = sum ;
"Bad assignments" = text ;
```

- 6. 保存并尝试重新编译程序，以查看因错误放置 R-value 而导致的错误

![](img/bf8dbdfb89042fadbaa73b4160c74bac_98_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_98_2.png)

L-value 是容器，而 R-value 是数据。

### 使用指针获取值

指针是高效 C++ 编程中有用的部分——它们就是存储其他变量内存地址的变量。

指针变量的声明方式与其他变量相同，但数据类型后缀有一个“*”字符。在声明中，这表示该变量将是一个指针。始终记住：指针的数据类型必须与其指向的变量的数据类型匹配。

指针变量通过使用 & 引用运算符为其赋予另一个变量的内存地址来初始化。赋值可以在声明语句中完成，也可以在声明后的单独语句中完成。仅通过指针变量名来引用它，将会直接显示它所包含的内存地址。

指针变量初始化后（无论是在声明中还是在后续赋值中），它就“指向”其包含地址处的变量。有用的是，这意味着可以通过在指针名称前加上 * 解引用运算符来引用它所指向的变量的值。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_99_0.png)

deref.cpp

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀来启动一个新程序

```cpp
#include <iostream>
using namespace std;
```

- 2. 添加一个主函数，其中包含一个最终的 **return** 语句，并声明两个常规的已初始化整型变量

```cpp
int main()
{
    int a = 8, b = 16;
    // 在这里添加更多语句。
    return 0;
}
```

- 3. 在主函数中，插入一条语句来声明一个指针，并用第一个整型变量的内存地址初始化它

```cpp
int* aPtr = &a;      // aPtr 被赋值为 a 的地址。
```

- 4. 插入一条语句来声明第二个指针，然后用第二个整型变量的地址初始化它

```cpp
int* bPtr;           // 声明 bPtr。
bPtr = &b;           // bPtr 被赋值为 b 的地址。
```

- 5. 接下来，插入语句以输出每个指针的实际内存地址

```cpp
cout << "Addresses of pointers..." << endl;
cout << "aPtr: " << &aPtr << endl;
cout << "bPtr: " << &bPtr << endl;
```

- 6. 现在，插入语句以输出存储在每个指针内部的内存地址

```cpp
cout << "Values in pointers..." << endl;
cout << "aPtr: " << aPtr << endl;
cout << "bPtr: " << bPtr << endl << endl;
```

- 7. 最后，插入语句以输出存储在每个指针所指向的内存地址处的值——即指针所指向变量的值

```cpp
cout << "Values in addresses pointed to..." << endl;
cout << "a: " << *aPtr << endl;
cout << "b: " << *bPtr << endl;
```

