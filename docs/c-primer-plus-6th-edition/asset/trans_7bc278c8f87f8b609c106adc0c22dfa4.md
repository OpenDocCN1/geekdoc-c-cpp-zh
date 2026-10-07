

# 第12章章节习题答案

7. 这里有一个可能的原型和定义：

```
//原型和内联定义
operator double () {return mag;}
```
但是，定义 `val()` 方法比定义这种转换函数更有意义。

- 1. a. 语法是正确的，但这个构造函数没有初始化 `str` 指针。构造函数应该将指针设置为 `NULL` 或使用 `new []` 来初始化指针。
  b. 这个构造函数没有创建一个新的字符串；它仅仅拷贝了地址。
  c. 它拷贝了字符串，但没有分配存储它的空间。它应该使用 `new char[len + 1]` 来分配适当的内存。

- 2. 当该类型的对象存在时，对象指向的数据仍然留在内存中，但指针丢失了，因此无法访问。通过在类构造函数中使用 `new` 分配内存可以修复这个问题。其次，在析构函数删除对象后，它可能会尝试两次 `delete`，如果将一个对象赋值给另一个对象，会产生两个指向相同数据的指针。解决方案是重载赋值运算符，使其拷贝数据而不是地址。

- 3. C++ 自动提供了以下成员函数：
  * 如果没有定义构造函数，提供默认构造函数
  * 如果没有定义，提供拷贝构造函数
  * 如果没有定义，提供默认赋值运算符
  * 如果没有定义，提供默认析构函数
  * 如果没有定义，提供地址运算符

默认构造函数什么都不做，但它允许你声明数组和未初始对象。默认拷贝构造函数和默认赋值运算符使用赋值。默认析构函数什么都不做。地址运算符返回调用对象的地址（即该指针的值）。

- 4. `personality` 成员应该声明为字符数组或指向字符的指针。或者你可以将其定义为 String 对象或字符串对象。声明没有将方法设置为 `public`。这里有几个小错误。这是一个可能的解决方案，删除部分内容已**加粗**：

```cpp
#include <iostream>
#include <string>
using namespace std;
class nifty
{
    private: // 可选
    char personality[40]; // 提供数组大小
    int talents;
    public: // 需要
    // 方法
    nifty();
    nifty(const char * s);
    friend ostream &operator<<(ostream & os, const nifty & n);
}; // 注意分号

nifty::nifty()
{
    personality[0] = '\0';
    talents = 0;
}

nifty::nifty(const char * s)
{
    strcpy(personality, s);
    talents = 0;
}

ostream &operator<<(ostream & os, const nifty & n)
{
    os << n.personality << '\n';
    os << n.talent << '\n';
    return os;
}
```

另一个可能的解决方案：

```cpp
#include <iostream>
#include <string>
using namespace std;
class nifty
{
    private: // 可选
    char * personality; // 创建指针
```

# 附录 J 习题答案

```cpp
int talents;
public: // 需要
// 方法
nifty();
nifty(const char * s);
nifty(const nifty & n);
~nifty() { delete [] personality; }
nifty & &operator=(const nifty & n) const;
    friend ostream & operator<<(ostream & os, const nifty & n);
}; // 注意拷贝分号

nifty::nifty()
{
    personality = NULL;
    talents = 0;
}

nifty(const char * s)
{
    personality = new char[strlen(s) + 1];
    strcpy(personality, s);
    talents = 0;
}
```

```cpp
ostream & operator<<(ostream & os, const nifty & n)
{
    os << n.personality << '\n';
    os << n.talents << '\n';
    return os;
}
```

注意，某些编译器对于语句 5 和 6额外调用默认赋值运算符。

- b. 类应该定义一个拷贝数据而非地址的赋值运算符。

# 第13章章节习题答案

- 1. 基类的公共成员变为派生类的公共成员。基类的保护成员变为派生类的保护成员。基类的私有成员被继承，但无法直接访问。习题 2 的答案提供了这些通用规则的例外情况。

- 2. 构造函数方法不被继承，析构函数不被继承，赋值运算符不被继承，友元也不被继承。

- 3. 如果返回类型是 `void`，你仍然可以使用赋值，但不能链式赋值：
```cpp
baseDMA magazine("Pandering to Glitz", 1);
baseDMA gift1, gift2, gift3;
gift1 = magazine; // OK
gift2 = gift3; // 无效
```

如果方法返回对象而不是引用，速度会很慢。

- 4. 构造函数按照派生顺序调用。析构函数按相反顺序调用。

- 5. 是的，派生类需要自己的构造函数。如果派生类增加了新成员，这些成员必须存在。

- 6. 如果派生类没有重写该方法，则调用基类方法。

- 7. 如果派生类增加了类成员，它应该定义一个赋值运算符。

- 8. 是的，只有通过显式转换才能将派生类的地址赋值给基类指针（向下转型）。

- 9. 是的，如果派生类定义了转换运算符或赋值运算符，可以将派生类对象赋值给基类对象。

- 10. 可以这样做，因为 C++ 允许基类类型的引用指向任何派生自该类型。

- 11. 按值传递对象会调用拷贝构造函数。因为形式参数是基类对象，所以调用基类的拷贝构造函数。拷贝构造函数的参数是基类的引用，该引用可以指向派生对象。结果是产生了一个成员与派生对象的基类部分对应的新基类对象。

- 12. 按引用传递对象而不是按值可以利用虚函数。同样，按引用传递对象 own按值可能节省内存和时间，特别是对于大对象。按值传递的主要优点是保护原始数据，但你可以通过将引用传递为 `const` 类型来实现相同的效果。

