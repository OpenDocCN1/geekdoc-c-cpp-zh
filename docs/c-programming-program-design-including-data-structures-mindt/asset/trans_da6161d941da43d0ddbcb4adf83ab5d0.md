
因此，没有必要显式重载赋值运算符来将 C 字符串存储到 newString 类型的对象中。

接下来，我们编写一个 C++ 程序，测试 newString 类的一些操作。

```cpp
//***********************************************************
// Author: D.S. Malik
//
// This program shows how to use the class newString.
//***********************************************************

#include <iostream>                                      //Line 1
#include "myString.h"                                    //Line 2

using namespace std;                                     //Line 3

int main()                                               //Line 4
{                                                        //Line 5
    newString str1 = "Sunny";//initialize str1 using
                             // the assignment operator. Line 6
    const newString str2("Warm");//initialize str2
                                 //using the conversion constructor. Line 7
    newString str3; //initialize str3 to the
                    //empty string.                  Line 8
    newString str4; //initialize str4 to the
                    //empty string.                  Line 9

    cout << "Line 10: " << str1 << "    " << str2
         << " ***" << str3 << "###." << endl;        //Line 10

    if (str1 <= str2)        //compare str1 and str2; Line 11
        cout << "Line 12: " << str1 << " is less "
             << "than or equal to " << str2 << endl;//Line 12
    else
        cout << "Line 14: " << str2 << " is less "   //Line 13
             << "than " << str1 << endl;              //Line 14

    cout << "Line 15: Enter a string with a length "
         << "of at least 7: ";                        //Line 15
    cin >> str1;             //input str1;            //Line 16
    cout << endl;                                     //Line 17

    cout << "Line 18: The new value of "
         << "str1 = " << str1 << endl;                //Line 18

    str4 = str3 = "Birth Day";                        //Line 19

    cout << "Line 20: str3 = " << str3
         << ", str4 = " << str4 << endl;              //Line 20
}
```

## 函数重载

上一节讨论了运算符重载。运算符重载为程序员提供了针对用户自定义数据类型的简洁表示法，与运算符用于内置类型时相同。与运算符一起使用的参数类型决定要执行的操作。与运算符重载类似，C++ 允许程序员重载函数名。第 6 章介绍了函数重载。为便于在后续讨论中参考，让我们回顾这一概念。

回想一下，一个类可以有多个构造函数，但一个类的所有构造函数都具有相同的名称，即该类的名称。这是函数重载的一个例子。进一步回想，函数重载指的是具有多个同名但参数列表不同的函数。参数列表决定将执行哪个函数。

要使函数重载生效，我们必须给出每个函数的定义。下一节将教你如何用单个代码段重载函数，并把为各个函数生成代码的工作留给编译器。

## 模板

模板是 C++ 的一项非常强大的特性。它们允许你为一组相关函数编写单个代码段，称为**函数模板**，并为一组相关类编写单个代码段，称为**类模板**。我们用于模板的语法是

```cpp
template <class Type>
declaration;
```

其中 Type 是数据类型的名称，可以是内置类型或用户自定义类型，而 **声明** 是函数声明或类声明。在 C++ 中，`template` 是保留字。标题中的 `class` 一词指任何用户自定义类型或内置类型。**Type** 被称为模板的形式参数。（注意，在第一行 `template <class Type>` 中，关键字 `class` 可以替换为关键字 `typename`。）

与变量作为函数参数类似，类型（即数据类型）是模板的参数。

### 函数模板

在第 6 章中，当我们介绍函数重载时，函数 **larger** 被重载以找出两个整数、字符、浮点数或字符串中较大的一个。要实现函数 **larger**，我们需要为该数据类型编写四个函数定义：一个用于 `int`，一个用于 `char`，一个用于 `double`，一个用于 `string`。然而，每个函数的主体都相似。在这种情况下，C++ 通过提供函数模板简化了函数重载的过程。

函数模板的语法是

```cpp
template <class Type>
function definition;
```

其中 Type 被称为模板的形式参数。它用于指定函数的参数类型和函数的返回类型，并在函数内声明变量。

以下语句：

```cpp
template <class Type>
Type larger(Type x, Type y)
{
        if (x >= y)
                return x;
        else
                return y;
}
```

定义了一个函数模板 larger，它返回两个项中较大的一个。在函数头中，形式参数 x 和 y 的类型是 Type，当调用函数时，该类型将由实际参数的类型指定。语句

`cout << larger(5, 6) << endl;`

是对函数模板 larger 的调用。由于 5 和 6 是 int 类型，因此数据类型 int 被替换为 Type，编译器生成相应的代码。

注意，函数模板 larger 仅适用于已定义运算符 >= 的那些数据类型。

如果在函数模板定义中省略函数体，那么该函数模板照常是原型。

下面的示例说明了函数模板的用法。

**示例 13-9**

下面的程序使用函数模板 larger 确定两个项中较大的一个。

```cpp
//Template larger

#include <iostream>                              //Line 1
#include "myString.h"                           //Line 2

using namespace std;                              //Line 3

template <class Type>                             //Line 4
Type larger(Type x, Type y);                      //Line 5

int main()
{
    cout << "Line 8: Larger of 5 and 6 = "        //Line 6
        << larger(5, 6) << endl;                 //Line 7
    cout << "Line 9: Larger of A and B = "        //Line 8
        << larger('A', 'B') << endl;              //Line 9
    cout << "Line 10: Larger of 5.6 and 3.2 = "   //Line 10
        << larger(5.6, 3.2) << endl;

    newString str1 = "Hello";                    //Line 11
    newString str2 = "Happy";                    //Line 12

    cout << "Line 13: Larger of " << str1 << " and "
        << str2 << " = " << larger(str1, str2)
        << endl;                                  //Line 13

    return 0;                                     //Line 14
}                                                 //Line 15
```

```cpp
template <class Type>
Type larger(Type x, Type y)
{
    if (x >= y)
        return x;
    else
        return y;
}
```

**示例运行：**

```text
Line 8: Larger of 5 and 6 = 6
Line 9: Larger of A and B = B
Line 10: Larger of 5.6 and 3.2 = 5.6
Line 13: Larger of Hello and Happy = Hello
```

### 类模板

与函数模板类似，类模板用于为一组相关类编写单个代码段。例如，在第 10 章中，我们将列表定义为 ADT；我们的列表元素类型是 `int`。如果列表元素类型从 `int` 变为例如 `char`、`double` 或 `string`，我们需要为每种元素类型编写单独的类。在大多数情况下，对列表的操作以及实现这些操作的算法保持不变。使用类模板，我们可以创建泛型类 `listType`，编译器可以为特定实现生成相应的源代码。

我们用于类模板的语法是：

```cpp
template <class Type>
class declaration
```

类模板被称为**参数化类型**，因为根据参数类型会生成特定的类。
