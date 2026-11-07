
```cpp
class Employee
{
private:
    char name[40];
    ...
public:
    void show_name();
    ...
};
class Singer : public Employee
{
    ...
public:
    void range();
    ...
};
...
Employee veep;
Singer trala;
...
Employee * pe = &trala;      // upcast—implicit type cast allowed
Singer * ps = (Singer *) &veep; // downcast—explicit type cast required
pe->show_name();              // Upcasting leads to a safe operation because
                              // a Singer is an Employee (every Singer
                              // inherits name).
ps->range();                  // Downcasting can lead to an unsafe operation
                              // because an Employee isn’t a Singer (an
                              // Employee need not have a range() method).
```

![](img/9afc44517b591d64e2e19f623c9308ef_787_0.png)

图13.4 向上转换与向下转换。

## 赋值运算符注意事项

如果编译器检测到程序将一个对象赋给同一类的另一个对象，它会自动为该类提供一个赋值运算符。该运算符的默认版本（即隐式版本）使用逐成员赋值，目标对象的每个成员都被赋予源对象对应成员的值。然而，如果对象属于派生类，编译器会使用基类的赋值运算符来处理派生类对象中基类部分的赋值。如果你已经为基类显式提供了赋值运算符，就使用该运算符。同样，如果一个类包含一个属于另一个类的对象成员，则该成员使用那个类的赋值运算符。

正如你已经多次看到的，如果类构造函数使用 `new` 来初始化指针，就需要提供显式的赋值运算符。由于 C++ 使用基类赋值运算符处理派生对象的基类部分，因此除非派生类添加了需要特殊处理的数据成员，否则不需要为派生类重新定义赋值运算符。例如，baseDMA 类显式定义了赋值，而派生类 lacksDMA 使用为该类生成的隐式赋值运算符。

不过，假设派生类确实使用了 `new`，并且你必须提供显式的赋值运算符。该运算符必须处理类的每个成员，而不仅仅是新增的成员。`hasDMA` 类说明了如何做到这一点：

```cpp
hasDMA & hasDMA::operator=(const hasDMA & hs)
{
    if (this == &hs)
        return *this;
    baseDMA::operator=(hs);  // copy base portion
    delete [] style;         // prepare for new style
    style = new char[std::strlen(hs.style) + 1];
    std::strcpy(style, hs.style);
    return *this;
}
```

那么，将派生类对象赋给基类对象会怎样呢？（注意，这与将基类引用初始化为派生类对象并不相同。）看看下面这个例子：

```cpp
Brass blips;                                      // base class
BrassPlus snips("Rafe Plosh", 91191, 3993.19, 600.0, 0.12); // derived class
blips = snips;                                    // assign derived object to base object
```

使用的是哪个赋值运算符？请记住，赋值语句会被转换为由左侧对象调用的方法：

```cpp
blips.operator=(snips);
```

这里的左侧对象是一个 `Brass` 对象，因此它调用 `Brass::operator=(const Brass &)` 函数。*is-a* 关系允许 `Brass` 引用指向派生类对象，例如 `snips`。赋值运算符只处理基类成员，因此在赋值中会忽略 `snips` 的 `maxLoan` 成员和其他 `BrassPlus` 成员。简而言之，你可以将派生对象赋给基类对象，并且只涉及基类成员。

反过来呢？可以将基类对象赋给派生对象吗？看看下面这个例子：

```cpp
Brass gp("Griff Hexbait", 21234, 1200);   // base class
BrassPlus temp;                          // derived class
temp = gp;   // possible?
```

这里的赋值语句会被转换为如下形式：

```cpp
temp.operator=(gp);
```

左侧对象是一个 `BrassPlus` 对象，因此它调用 `BrassPlus::operator=(const BrassPlus &)` 函数。然而，派生类引用不能自动指向基类对象，因此除非还有一个转换构造函数，否则这段代码*不会*运行：

```cpp
BrassPlus(const Brass &);
```

也可能像 BrassPlus 类那样，转换构造函数是一个带有基类实参以及额外实参的构造函数，前提是额外实参具有默认值：

```cpp
BrassPlus(const Brass & ba, double ml = 500, double r = 0.1);
```

如果有转换构造函数，程序会使用该构造函数从 gp 创建一个临时 BrassPlus 对象，然后将该对象用作赋值运算符的实参。

或者，你也可以定义一个赋值运算符，用于将基类赋给派生类：

```cpp
BrassPlus & BrassPlus::operator=(const Brass &) {...}
```

这里的类型与赋值语句完全匹配，不需要任何类型转换。

简而言之，对于“能否将基类对象赋给派生对象？”这个问题，答案是“也许可以”。如果派生类有一个定义如何将基类对象转换为派生类对象的构造函数，就可以；如果派生类定义了一个用于将基类对象赋给派生对象的赋值运算符，也可以。如果这两个条件都不成立，那么除非使用显式类型转换，否则不能进行这种赋值。

## 私有成员与受保护成员

请记住，就派生类而言，受保护成员的行为像公有成员；但对外界而言，它们的行为像私有成员。派生类可以直接访问基类的受保护成员，但只能通过基类的成员函数访问私有成员。因此，将基类成员设为私有提供了更高的安全性，而将它们设为受保护则简化了编码并加快了访问速度。Stroustrup 在其著作 *The Design and Evolution of C++* 中指出，使用私有数据成员比使用受保护数据成员更好，但受保护方法很有用。

## 虚方法注意事项

设计基类时，你必须决定是否将类方法设为虚方法。如果希望派生类能够重定义某个方法，就在基类中把该方法定义为虚方法。这会启用后期绑定（即动态绑定）。如果不希望该方法被重定义，就不要把它设为虚方法。这并不能阻止别人重定义该方法，但应将其理解为你不希望它被重定义。

注意，不恰当的代码会绕过动态绑定。例如，考虑下面两个函数：

```cpp
void show(const Brass & rba)
{
    rba.ViewAcct();
    cout << endl;
}
```

```cpp
void inadequate(Brass ba)
{
    ba.ViewAcct();
    cout << endl;
}
```

第一个函数按引用传递对象，第二个函数按值传递对象。现在假设用派生类实参分别调用它们：

```cpp
BrassPlus buzz("Buzz Parsec", 00001111, 4300);
show(buzz);
inadequate(buzz);
```

`show()` 函数调用会使 rba 实参成为对 BrassPlus 对象 buzz 的引用，因此 rba.ViewAcct() 会按 BrassPlus 版本解释，这是正确的。但在按值传递对象的 inadequate() 函数中，ba 是由 Brass(const Brass &) 构造函数构造的 Brass 对象。（自动向上转换允许构造函数实参引用 BrassPlus 对象。）因此，在 inadequate() 中，ba.ViewAcct() 是 Brass 版本，所以只显示 buzz 的 Brass 部分。

## 析构函数注意事项

如前所述，基类析构函数应为虚函数。这样，当你通过基类指针或引用删除派生对象时，程序会先调用派生类析构函数，再调用基类析构函数，而不是只调用基类析构函数。

## 友元注意事项

由于友元函数实际上不是类成员，所以它不会被继承。不过，你可能仍希望派生类的友元函数使用基类的友元。实现方法是将派生类引用或指针强制转换为基类等价类型，然后使用转换后的引用或指针调用基类友元：

```cpp
ostream & operator<<(ostream & os, const hasDMA & hs)
{
    // type cast to match operator<<(ostream & , const baseDMA &)
    os << (const baseDMA &) hs;
    os << "Style: " << hs.style << endl;
    return os;
}
```

也可以使用第15章“友元、异常及其他”中讨论的 dynamic_cast<> 运算符进行类型转换：

```cpp
os << dynamic_cast<const baseDMA &> (hs);
```

由于第15章讨论的原因，这将是首选的类型转换形式。
