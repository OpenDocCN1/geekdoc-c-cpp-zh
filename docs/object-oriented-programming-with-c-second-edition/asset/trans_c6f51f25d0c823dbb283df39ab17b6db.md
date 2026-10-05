

# 使用 C++ 进行面向对象编程

4. 某些操作符只能通过非静态成员函数进行重载：以下操作符仅可以使用非静态成员函数进行重载。
- =（赋值运算符）
- ()（函数运算符）
- []（下标运算符）
- ->（指针访问运算符）

这些操作符不能通过友函数或静态函数进行重载。

5. 现有操作符无法更改的参数数量：运算符重载函数的参数数量应与被重载运算符通常的参数数量相同。例如，除法运算符接受两个参数。因此，列表 8.8 所示的类定义会导致运算符重载函数产生“operator / takes too few arguments”的编译时错误。

列表 8.8 修改操作符默认参数数量的非法尝试

```cpp
class A {
  public:
    void operator / ();
};
```

6. 重载的操作符不能带有默认参数：列表 8.9 所示的类定义会导致运算符重载函数产生“operator/ cannot take default arguments”的编译时错误。

列表 8.9 尝试为运算符重载函数的参数分配默认值的非法尝试。

最后，我们必须注意，修改传递给运算符重载函数的操作数是非常轻率的。为了更好地理解这一点，让我们考虑为 `String` 类重载加法运算符函数。

```cpp
class String {
  char *cStr;
  long len;
  public:
    String operator + (String &);
};
```

库程序员可能会错误地编写某些语句，来修改 `String::operator + () 函数的隐式或显式参数的值（见列表 8.10）。

# 运算符重载、类型转换、新风格强制转换和 RTTI

**列表 8.10** 在重载加法运算符的函数中修改左侧和右侧的操作数

```cpp
String String :: operator + (String & ss)
{
    /*
    String :: operator + () 的剩余部分
    */
    this->cStr = NULL; // Bug：左侧参数
                     // 被修改了！
    /*
    String :: operator + () 的剩余部分
    */
    ss.cStr = NULL; // Bug：右侧参数
                   // 被修改了！
    /*
    String :: operator + () 的剩余部分
    */
}
```

为了防止这种意外，可以像列表 8.11 所示声明运算符重载函数。

**列表 8.11** 恰善使用 const 关键字以防止 bug

```cpp
class String
{
    char * cStr;
    long int len;
public:
    String operator + (const String &) const;
};
```

列表 8.10 中带有 bug 的语句都无法编译。
现在让我们看看操作符实际上是如何重载的。

# 8.2 重载运算符

## 8.2.1 重载递增和递运算符（前缀和后置）

让我们回想 `Distance` 类。我们可以为该类的对象重载递增运算符。我们希望这个函数做什么呢？如果 `d1` 和 `d2` 是 `Distance` 类的对象，那么以下语句

```cpp
d2 = ++d1;
```

会被编译器解释为：

```cpp
d2 = d1.operator ++ ();
```

想象一下，这个运算符重载函数应该首先增加 `d1` 的 `iFeet` 部分。它将保持 `d1` 的 `inches` 不变。然后它返回结果对象。基于这些原则，运算符重载函数的原型和定义将如列表 8.12 所示。

# 列表 8.12 声明重载递增运算符的成员函数

```cpp
/*Distance.h 开始*/
class Distance
{
    public:
    /*
    Distance类的类的部分
    */
    Distance operator ++ ();
};
/*Distance.h 结束*/
/*Distance.cpp 开始*/
#include "Distance.h"
Distance Distance :: operator ++ ()
{
    return Distance(+iFeet, fInches);
}
/* Distance 类其他函数的定义 */
/*Distance.cpp 结束*/
```

运算符重载函数应该是公共的，因为大多数情况下它会从不是 `Distance` 类成员的函数中调用。它不应该是常量成员函数，因为它确实会修改调用对象至少一个数据成员（`iFeet`）的值。虽然运算符重载函数的定义看起来很晦懂，但实际上非常简单（且高效）。首先，递增运算符起作用了（它是前置符号）。因此，调用对象的 `iFeet` 数据成员被增加了。其次，对构造函数的显式调用通过传递增加后的 `iFeet` 值和未改变的 `inches` 值作为参数，创建了一个 `Distance` 类的匿名对象。第三，运算符重载函数返回构造好的匿名对象。如果运算符重载函数的调用是在赋值运算符的右侧，则返回对象的值将如预期般复制到左侧的对象。这样，我们的目的实现了。

然而，如果我们写语句，我们希望产生不同的效果：

```cpp
d2 = d++;
```

在这种情况下，运算符重载函数应该在递增 `d` 之前返回其原始值。为了做到这一点，我们必须先对象的拷贝，然后增加原始对象，最后返回拷贝。实现方式如下：

```cpp
Distance operator ++ (int)
{
    Distance temp = *this;
    iFeet++;
    return temp;
}
```

`int` 参数是一个哑参数，用于区分后置运算符和前置运算符。类似地，递减运算符将实现为：

```cpp
Distance operator -- ()
{
    iFeet--;
    return *this;
}

Distance operator -- (int)
{
    Distance temp = *this;
    iFeet--;
    return temp;
}
```

## 8.2.2 重载一负运算符和一正运算符

重载一负运算符如列表 8.15 所示。

```cpp
/*A.h 开始*/
class A
{
    int x;
public:
    A(int = 0);
    A operator - (();
};
/*A.h 结束*/
```