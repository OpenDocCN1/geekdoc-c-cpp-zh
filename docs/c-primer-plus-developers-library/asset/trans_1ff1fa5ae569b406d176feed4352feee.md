
```
Stonewt jennySt(9, 12);
Stonewt bennySt(12, 8);
Stonewt total;
total = jennySt + bennySt;
```

此外，给定 Stonewt (double) 构造函数，每种形式都允许你执行以下操作：

```
Stonewt jennySt(9, 12);
double bennyD = 176.0;
Stonewt total;
total = jennySt + bennyD;
```

但只有友元函数允许你这样做：

```
Stonewt jennySt(9, 12);
double bennyD = 146.0;
Stonewt total;
total = bennyD + jennySt;
```

要明白为什么，你可以将每个加法转换为对应的函数调用。首先，

```
total = jennySt + bennySt;
```

变为

```
total = jennySt.operator+(bennySt);   // member function
```

或者

```
total = operator+(jennySt, bennySt);  // friend function
```

无论哪种情况，实参类型都与形参匹配。此外，成员函数按要求由 Stonewt 对象调用。

接下来，

```
total = jennySt + bennyD;
```

变为

```
total = jennySt.operator+(bennyD);   // member function
```

或者

```
total = operator+(jennySt, bennyD);  // friend function
```

同样，成员函数按要求由 Stonewt 对象调用。这一次，在每种情况下，都有一个参数（bennyD）是 double 类型，这会调用 Stonewt (double) 构造函数将该参数转换为 Stonewt 对象。

顺便说一句，此时如果定义了 operator double() 成员函数，会造成混淆，因为那会为解释提供另一种选择。编译器可以将 jennySt 转换为 double 并执行 double 加法，而不是将 bennyD 转换为 double 并执行 Stonewt 加法。拥有过多的转换函数会产生歧义。

最后，

```
total = bennyD + jennySt;
```

变为

```
total = operator+(bennyD, jennySt);  // friend function
```

这里，两个参数都是 double 类型，这会调用 Stonewt (double) 构造函数将它们转换为 Stonewt 对象。

然而，成员函数版本无法将 jennySt 加到 bennyD 上。将加法语法转换为函数调用会看起来像这样：

```
total = bennyD.operator+(jennySt);  // not meaningful
```

但这是无意义的，因为只有类对象才能调用成员函数。C++ 不会尝试将 bennyD 转换为 Stonewt 对象。转换发生在成员函数参数上，而不是成员函数调用者上。

这里的教训是，将加法定义为友元可以使程序更容易适应自动类型转换。原因是两个操作数都成为函数参数，因此函数原型机制对两个操作数都起作用。

## 实现加法的选择

假设你想将 double 量加到 Stonewt 量上，你有几个选择。第一种，正如你刚才看到的，是将以下内容定义为友元函数，并让 Stonewt (double) 构造函数处理 double 类型参数到 Stonewt 类型参数的转换：

```
operator+(const Stonewt &, const Stonewt &)
```

第二种选择是用显式使用一个 double 类型参数的函数进一步重载加法运算符：

```
Stonewt operator+(double x);  // member function
friend Stonewt operator+(double x, Stonewt & s);
```

这样，以下语句与 operator+(double x) 成员函数完全匹配：

```
total = jennySt + bennyD; // Stonewt + double
```

而以下语句与 operator+(double x, Stonewt & s) 友元函数完全匹配：

```
total = bennyD + jennySt; // double + Stonewt
```

之前，我们对 Vector 乘法做了类似的事情。

每种选择都有优点。第一种选择（依赖隐式转换）会产生更短的程序，因为你定义的函数更少。这也意味着你的工作更少，出错的机会更少。缺点是每当需要转换时调用转换构造函数所需的时间和内存开销增加。然而，第二种选择（显式匹配类型的附加函数）则相反。它使程序更长，你的工作量更多，但运行速度稍快。

如果你的程序大量使用将 double 值加到 `Stonewt` 对象上，那么重载加法以直接处理这种情况可能是值得的。如果程序只是偶尔使用这种加法，那么依赖自动转换更简单，或者如果你想更谨慎，可以依赖显式转换。

## 总结

本章涵盖定义和使用类的许多重要方面。在你自己的经验丰富你的理解之前，本章中的一些材料可能对你来说显得模糊。

通常，访问私有类成员的唯一方法是使用类方法。C++ 通过友元函数缓解了这一限制。要使函数成为友元函数，你在类声明中声明该函数，并在声明前加上关键字 `friend`。

C++ 将重载扩展到运算符，允许你定义特殊的运算符函数，描述特定运算符如何与特定类相关联。运算符函数可以是类成员函数或友元函数。（少数运算符只能是类成员函数。）C++ 允许你通过调用函数或使用重载运算符的通常语法来调用运算符函数。运算符 `op` 的运算符函数具有以下形式：

```
operator<argument-list>
```

`argument-list` 表示运算符的操作数。如果运算符函数是类成员函数，那么第一个操作数是调用对象，不是 `argument-list` 的一部分。例如，本章通过为 `Vector` 类定义 `operator+()` 成员函数来重载加法。如果 up、right 和 result 是三个向量，你可以使用以下任一语句来调用向量加法：

```
result = up.operator+(right);
result = up + right;
```

对于第二个版本，操作数 `up` 和 `right` 是 `Vector` 类型这一事实告诉 C++ 使用 `Vector` 的加法定义。

当运算符函数是成员函数时，第一个操作数是调用该函数的对象。例如，在前面的语句中，`up` 对象是调用对象。如果你希望定义运算符函数使第一个操作数不是类对象，你必须使用友元函数。然后你可以按任意顺序将操作数传递给函数定义。

运算符重载最常见的任务之一是定义 `<<` 运算符，以便它可以与 `cout` 对象一起使用来显示对象的内容。为了让 `ostream` 对象成为第一个操作数，你将运算符函数定义为友元。为了让重新定义的运算符可以与自己连接，你将返回类型设为 `ostream &`。以下是满足这些要求的一般形式：

```
ostream & operator<<(ostream & os, const c_name & obj)
{
    os << ... ;  // display object contents
    return os;
}
```

然而，如果类具有返回你想显示的数据成员值的方法，你可以在 `operator<<( )` 中使用这些方法而不是直接访问。在这种情况下，函数不需要（也不应该）是友元。

C++ 允许你建立到类类型和从类类型的转换。首先，任何接受单个参数的类构造函数都充当转换函数，将参数类型的值转换为类类型。如果你将参数类型的值赋给对象，C++ 会自动调用该构造函数。例如，假设你有一个 `String` 类，其构造函数接受一个 `char *` 值作为唯一参数。那么，如果 `bean` 是一个 `String` 对象，你可以使用以下语句：

```
bean = "pinto";   // converts type char * to type String
```

然而，如果你在构造函数声明前加上关键字 `explicit`，则该构造函数只能用于显式转换：

```
bean = String("pinto");   // converts type char * to type String explicitly
```

要从类转换为另一种类型，你必须定义转换函数并提供如何执行转换的说明。转换函数必须是成员函数。如果它要转换为 `typeName` 类型，则应具有以下原型：

```
operator typeName();
```

注意，它不能有声明的返回类型，不能有参数，并且（尽管没有声明的返回类型）必须返回转换后的值。例如，将 `Vector` 类型转换为 `double` 类型的函数将具有以下函数形式：

```
Vector::operator double()
{
    ...
    return a_double_value;
}
```

经验表明，通常最好不要依赖这种隐式转换函数。

你可能已经注意到，类比简单的 C 风格结构体需要更多的关心和对细节的注意。作为回报，它们为你做的也更多。

