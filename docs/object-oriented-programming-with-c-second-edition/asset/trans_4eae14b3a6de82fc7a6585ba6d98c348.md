

## 运算符重载、类型转换、新风格强制转换、RTTI 235

在大多数情况下，这种默认赋值运算符已经足够。然而，在某些情况下，这种默认行为会导致问题。让我们回顾第 4 章中关于拷贝构造函数的章节。我们讨论过对于动态获取类，默认拷贝构造函数的负面影响。由于默认赋值运算符的影响，会出现完全相同的问题。代码产生的问题：

```cpp
String s1, s2;
s1.setString("abcd");
s2 = s1;
```

如果未定义赋值运算符，其产生的问题与以下代码的问题相同：

```cpp
String s1("abcd");
s2 = s1;
```

前提是未定义拷贝构造函数。由于上述赋值操作，'s1' 和 's2' 的指针最终将指向同一个内存块（见图 8.1）。通过对拷贝构造函数的研究，我们已经熟悉了此类情况下造成的破坏性。结论是，对于一个定义了拷贝构造函数的类，必须也定义赋值运算符。给出的该类赋值运算符的合适定义在列表 8.30 中。

### 列表 8.30 运算符运算符重载的示例

```cpp
/*Beginning of String.h*/
class String {
    char * cStr;
    unsigned int len;
public:
    String(const String&);
    String& operator = (const String&);
    // rest of the class String
};
/*End of String.h*/
```

```cpp
/*Beginning of String.cpp*/
#include "String.h"
#include<string.h>
String& String :: operator = (const String& ss)
{
    if(this != &ss)
    {
        delete[] cStr;
        cStr = NULL;
        len = 0;
    }
    if(ss.cStr != NULL)
    {
```

```cpp
        len = ss.len;
        cStr = new char[len + 1];
        strncpy(cStr,ss.cStr);

        return *this;
    }
/* definitions of the rest of the functions of class String
*//End of String.cpp*/
```

理解为什么最外层的 'if'（`if (this != &ss)`）被插入在函数顶部，以及为什么函数通过引用返回调用对象，我们必须意识到列表 8.30 中赋值运算符的定义，它按如下方式处理了所有可能的情况：

- LHS.cStr = NULL AND RHS.cStr = NULL
  如果 LHS.cStr = NULL，则第一个内部的 'if'（`if cStr != NULL`）失败，对应的 'if' 块不执行。如果 RHS.cStr = NULL，则第二个内部的 'if'（`if (ss.cStr != 0)`）失败，对应的 'if' 块不执行。整个函数不做任何操作，保持原样并通过引用返回调用对象。正如预期的那样，左侧操作数的值保持不变（因为 `cStr = NULL` 且 `len = 0`），因为右侧对象中的对应值为 NULL 和 0。
- LHS.cStr = NULL AND RHS.cStr != NULL
  如果 LHS.cStr = NULL，则第一个内部的 'if'（`if cStr != NULL`）失败，对应的 'if' 块不执行。如果 RHS.cStr != NULL，则第二个内部的 'if'（`if (ss.cStr != 0)`）成功，对应的 'if' 块执行：
    - 正确将类的 'len' 成员值设置为等于将存储右侧对象中 'cStr' 成员所指向的字符串拷贝的长度；
    - 分配足够的内存来存储 `cStr` 成员对象所指向的字符串拷贝，并使左侧的 'cStr' 成员指向它，并且
    - 将右侧 'cStr' 成员指向的字符串拷贝到左侧对象的内存块中。
- LHS.cStr != NULL AND RHS.cStr = NULL
  如果 LHS.cStr != NULL，则第一个内部的 'if'（`if cStr != NULL`）成功，对应的 'if' 块执行。它释放了左侧 'cStr' 成员所指向的内存块，将其值设置为 NULL，并将左侧 'len' 成员的值置为 0。如果 RHS.cStr = NULL，则第二个内部的 'if'（`if (ss.cStr != 0)`）失败，'if' 块不执行。正如预期的那样，如果尚未如此，左侧操作数的值将置空（`cStr = NULL` 且 `len = 0`），因为右侧为 NULL。
- LHS.cStr != NULL AND RHS.cStr != NULL
  如果 LHS.cStr != NULL，则第一个内部的 'if'（`if cStr != NULL`）成功，对应的 'if' 块执行。它释放了左侧 'cStr' 成员所指向的内存块，将其值设置为 NULL，并将左侧 'len' 成员的值置为 0。如果 rhs.cStr != NULL，则第二个内部的 'if'（`if (ss.cStr != 0)`）成功，对应的 'if' 块执行：
    - 正确将类的 'len' 成员值设置为将存储右侧对象中 'cStr' 成员所指向的字符串拷贝的长度；
    - 分配足够的内存来存储 `cStr` 成员对象所指向的字符串拷贝，并使左侧的 'cStr' 成员指向它，并且
    - 将右侧 'cStr' 成员指向的字符串拷贝到左侧对象的内存块中。

