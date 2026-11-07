
## 示例 13-10

下面的程序测试基于数组的列表上的各种操作。

```cpp
#include <iostream>
#include <string>
#include "unorderedArrayListType.h"

using namespace std;

int main()
{
    unorderedArrayListType<string> stringList(25);  //Line 1

    string str;                                      //Line 2

    cout << "List 3: Enter 5 strings: ";             //Line 3

    for (int count = 0; count < 5; count++)          //Line 4
    {
        cin >> str;                                  //Line 5
        stringList.insertEnd(str);                   //Line 6
    }

    cout << endl;                                    //Line 7
    cout << "Line 8: stringList: ";                 //Line 8
    stringList.print();                              //Line 9
    cout << endl;                                    //Line 10

    cout << "Line 11: Enter the string to be "
         << "deleted: ";                            //Line 11
    cin >> str;                                      //Line 12
    cout << endl;                                    //Line 13

    stringList.remove(str);                          //Line 14
    cout << "Line 15: After removing " << str
         << " stringList: ";                         //Line 15
    stringList.print();                              //Line 16
    cout << endl;                                    //Line 17

    cout << "Line 18: Enter the search item: ";      //Line 18

    cin >> str;                                      //Line 19
    cout << endl;                                    //Line 20

    if (stringList.seqSearch(str) != -1)             //Line 21
        cout << "Line 22: " << str
             << " found in stringList." << endl;     //Line 22
    else                                             //Line 23
        cout << "Line 24: " << str
             << " is not in stringList." << endl;    //Line 24

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
List 3: Enter 5 strings: `hello sunny warm winter summer`
Line 8: stringList: hello sunny warm winter summer
Line 11: Enter the string to be deleted: `hello`
Line 15: After removing hello stringList: sunny warm winter summer
Line 18: Enter the search item: `winter`
Line 22: winter found in stringList.
```

上述程序的工作过程如下。第 1 行的语句将 stringList 声明为 unorderedArrayListType 类型的对象。stringList 的成员变量 list 是一个包含 25 个分量的数组，分量类型为 string。第 2 行的语句声明字符串变量 str。第 3 行的语句提示用户输入 5 个字符串。第 5 行的语句从输入流中获取下一个字符串。第 6 行的语句使用 stringList 的成员函数 insertEnd 将该字符串存入 stringList。第 9 行的语句使用 stringList 的成员函数 print 输出 stringList 的元素。第 11 行的语句提示用户输入要从 stringList 中删除的字符串，第 12 行的语句从输入流中获取要删除的字符串。第 14 行的语句使用 stringList 的成员函数 remove 从 stringList 中删除该字符串。第 16 行的语句输出修改后的 stringList。

第 18 行到第 24 行的语句测试函数 seqSearch。

**注意：** 本书配套网站包含其他程序，说明如何使用 `class template unorderedArrayListType` 创建由 `double` 元素和 `clockType` 对象组成的列表。

正如我们可以从抽象类模板 `arrayListType` 派生出 `class template unorderedArrayListType` 来操作无序列表一样，我们也可以派生出 `class template orderedArrayListType` 来操作有序列表。（参见本章末尾的编程练习 21。）

## 快速回顾

- 1. 对不同的数据类型具有不同含义的运算符称为被重载的运算符。
- 2. 在 C++ 中，`>>` 既用作流提取运算符，也用作右移运算符。同样，`<<` 既用作流插入运算符，也用作左移运算符。两者都是运算符重载的例子。
- 3. 任何重载运算符的函数都称为运算符函数。
- 4. 运算符函数头部的语法是：`returnType operator operatorSymbol(parameters)`
- 5. 在 C++ 中，`operator` 是保留字。
- 6. 运算符函数是有返回值的函数。
- 7. 除赋值运算符和成员选择运算符外，要在类对象上使用运算符，必须重载该运算符。赋值运算符执行默认的逐成员复制。
- 8. 对于含有指针成员变量的类，必须显式重载赋值运算符。
- 9. 运算符重载为用户定义的数据类型提供了与内置数据类型相同的简洁表示法。
- 10. 重载运算符时，不能改变其优先级，不能改变其结合性，不能使用默认参数，不能改变该运算符接受的参数个数，并且运算符与内置数据类型配合工作的方式保持不变。
- 11. 不能创建新的运算符。只能重载已有的运算符。
- 12. 大多数 C++ 运算符都可以重载。
- 13. 不能重载的运算符是 `.`、`.*`、`::`、`?:` 和 `sizeof`。
- 14. 指针 `this` 指代整个对象。
- 15. 为类重载运算符 `()`、`[]`、`->` 或 `=` 的运算符函数必须是该类的成员。
- 16. `friend` 函数是类的非成员。
- 17. `friend` 函数的原型头部前面有单词 `friend`。
- 18. 在 C++ 中，`friend` 是保留字。
- 19. 如果运算符函数是类的成员，则该运算符最左边的操作数必须是该运算符所属类的类对象（或类对象的引用）。
- 20. 作为类成员的二元运算符函数只有一个参数；作为类的非成员时，它有两个参数。
- 21. 为类重载流插入运算符 `<<` 和流提取运算符 `>>` 的运算符函数必须是该类的 `friend` 函数。
- 22. 如果运算符函数是类的成员，要为类重载前置自增（`++`）运算符，它必须没有参数。同样，如果运算符函数是类的成员，要为类重载前置自减（`--`）运算符，它必须没有参数。
- 23. 如果运算符函数是类的成员，要为类重载后置自增（`++`）运算符，它必须有一个 `int` 类型的参数。用户不为该参数指定任何值。函数头部中的哑参数有助于编译器生成正确的代码。后置自减运算符也有类似的约定。
- 24. 转换构造函数是单参数函数。
- 25. 转换构造函数将其实参转换为该构造函数所属类的对象。编译器会隐式调用此类构造函数。
- 26. 含有指针成员变量的类必须重载赋值运算符，并同时包含复制构造函数和析构函数。
- 27. 在 C++ 中，函数名可以重载。
- 28. 在 C++ 中，template 是保留字。
- 29. 使用模板，可以为一系列相关函数编写单个代码段——称为函数模板。
- 30. 使用模板，可以为一系列相关类编写单个代码段——称为类模板。
- 31. 模板的语法为：

    ```cpp
    template <class Type>
    declaration;
    ```

    其中 Type 是用户定义的标识符，用于将类型（即数据类型）作为参数传递，而 declaration 要么是函数，要么是类。头部中的单词 class 指任何用户定义的数据类型或内置数据类型。

- 32. 类模板称为参数化类型。
- 33. 在类模板中，参数 Type 指定如何定制泛型类模板以形成特定的模板类。
- 34. 参数 Type 出现在每个类头部和成员函数定义中。
- 35. 假设 cType 是类模板，func 是 cType 的成员函数。func 的函数定义头部是：

    ```cpp
    template <class Type>
    funcType cType<Type>::func(parameters)
    ```

    其中 funcType 是函数的类型，例如 void。

- 36. 假设 cType 是类模板，它可以接受 int 作为参数。语句：

    ```cpp
    cType<int> x;
    ```

    将 x 声明为 cType 类型的对象，并且传递给类 cType 的类型是 int。
