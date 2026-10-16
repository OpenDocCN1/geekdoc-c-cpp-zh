
{
return !(a==b);
}

添加 `<` 等运算符并不困难。

为了支持范围 `for` 循环，我们需要 `begin()` 和 `end()`（§9.5.1）。同样，我们可以将它们提供为独立的（非成员）函数，而无需直接访问 `String` 的实现：

```
char* begin(String& x) // C-string-style access
{
return x.c_str();
}

char* end(String& x)
{
return x.c_str()+x.size();
}

const char* begin(const String& x)
{
return x.c_str();
}

const char* end(const String& x)
{
return x.c_str()+x.size();
}
```

给定用于在末尾添加字符的成员函数 `+=`，很容易通过非成员函数提供连接运算符：

```
String& operator+=(String& a, const String& b) // concatenation
{
for (auto x : b) a+=x;

return a;
String operator+(const String& a, const String& b) // concatenation {
String res {a};
res += b;
return res;
}
```

我觉得自己在这里可能有一点“作弊”。我是否应该提供一个将 C 风格字符串添加到末尾的成员 `+=`？标准库字符串确实提供了这样的功能，但即使没有它，与 C 风格字符串进行连接仍然可以正常工作。例如：

```
String s = “Njal “;
s += “Gunnar”; // concatenate: add to the end of s
```

这里对 `+=` 的使用会被解释为 `operator+=(s,String(“Gunnar”))`。我的猜测是，我可以提供一个更高效的 `String::operator+=(const char*)`，但我不知道这种额外的性能在实际代码中是否值得。在这种情况下，我倾向于采取保守做法，提供最小化的设计。能够实现某件事本身，并不是实现它的充分理由。

同样，我也没有尝试通过考虑源字符串的大小来优化 `+=`。添加表示 `String` 的 `_s` 字符串字面量后缀非常简单：

```
String operator""_s(const char* p, size_t)
{
return String{p};
}
```

现在我们可以这样写：

```
void f(const char*); // C-style string
void f(const String&); // our string
void g() {
f(“Madden’s”); // f(const char*)
f(“Christopher’s”_s); // f(const String&);
}
```

## 19.3.6 使用我们的 String

主程序只是对 `String` 运算符进行了一些简单测试：

```
int main()
{
String s (“abcdefghij”); cout << s << ‘\n’;
s+=‘k’;
s += ‘l’;
s+=‘m’;
s += ‘n’;
cout << s << ‘\n’;
```

```
String s2 = “Hell”;
s2 += ” and high water”; cout << s2 << ‘\n’;
String s3 = “qwerty”;
s3 = s3;
String s4 =“the quick brown fox jumped over the lazy dog”; s4 = s4;
cout << s3 << ” ” << s4 << “\n”;
cout << s + “. ” + s3 + String(“.”) + “Horsefeathers\n”;
String buf;
while (cin>>buf && buf!=“quit”)
cout << buf << ” ” << buf.size() << ” ” << buf.capacity() << ‘\n’;
}
```

这个 `String` 缺少许多你可能认为重要甚至必不可少的功能。

不过，就其所实现的功能而言，它与 `std::string`（第 36 章）非常相似，并展示了标准库字符串实现中所使用的技术。

## 19.4 友元

普通的成员函数声明指定了三个逻辑上相互独立的事项：  
[1] 该函数可以访问类声明中的私有部分。  
[2] 该函数位于类的作用域中。  
[3] 必须在对象上调用该函数（拥有一个 `this` 指针）。

通过将成员函数声明为静态函数（§16.2.12），我们可以只赋予它前两个属性。通过将非成员函数声明为友元，我们可以只赋予它第一个属性。也就是说，被声明为友元的函数可以像成员函数一样访问类的实现，但在其他方面与该类相互独立。

例如，我们可以定义一个将 `Matrix` 与 `Vector` 相乘的运算符。自然地，`Vector` 和 `Matrix` 都会隐藏各自的表示，并提供一套完整的操作来处理其类型的对象。然而，我们的乘法例程不能同时成为这两个类的成员。此外，我们也不希望提供底层访问函数，让每个用户都能读写 `Matrix` 和 `Vector` 的完整表示。为避免这种情况，我们将 `operator*` 声明为二者的友元：

```
constexpr rc_max {4}; // row and column size
class Matrix;

class Vector {
float v[rc_max];
// ...
friend Vector operator*(const Matrix&, const Vector&);
};
class Matrix {
Vector v[rc_max];
// ...
friend Vector operator*(const Matrix&, const Vector&);
};
```

现在，`operator*()` 可以深入访问 `Vector` 和 `Matrix` 的实现。这为复杂的实现技术提供了可能，不过一种简单的实现方式是：

```
Vector operator *(const Matrix& m, const Vector& v)
{
Vector r;
for (int i = 0; i!=rc_max; i++) { // r[i] = m[i] * v;
r.v[i] = 0;
for (int j = 0; j!=rc_max; j++)
r.v[i] += m.v[i].v[j] * v.v[j];
}
return r;
}
```

**友元**声明既可以放在类声明的私有部分，也可以放在公有部分；这并没有区别。与成员函数一样，友元函数会显式声明在其所属友元类的声明中。因此，它和成员函数一样，都是该接口的一部分。

一个类的成员函数可以成为另一个类的友元。例如：

```
class List_iterator {
// ...
int* next();
};

class List {
friend int* List_iterator::next();
// ...
};
```

有一种简写形式，可以将一个类的所有函数都声明为另一个类的友元。例如：

```
class List {
friend class List_iterator;
// ...
};
```

这个 **友元** 声明会将 **List_iterator** 的所有成员函数都设为 **List** 的友元。

将一个类声明为**友元**，就会授予该类的每个函数访问权限。这意味着，仅通过查看授予访问权限的类本身，我们无法知道哪些函数可以访问其表示。在这一点上，友元类声明不同于成员函数和友元函数的声明。显然，应谨慎使用友元类，并且只能用来表达紧密相关的概念。

也可以将模板参数设为**友元**：

```
template<typename T>
class X {
friend T;
friend class T; // redundant “class”
// ...
};
```

通常，可以选择将一个类设为成员（嵌套类），或者将其设为非成员友元（§18.3.1）。

### 19.4.1 查找友元

友元必须已经在外围作用域中声明，或者定义在声明它为友元的类所直接处于的非类作用域中。对于首次作为友元声明的名称，不会考虑最内层外围命名空间作用域之外的作用域（§iso.7.3.1.2）。请看下面这个技术性示例：

```
class C1 { }; // will become friend of N::C
void f1(); // will become friend of N::C

namespace N {
class C2 { }; // will become friend of C void f2() { } // will become friend of C

class C {
int x;
public:
friend class C1; friend void f1();

// OK (previously defined)

friend class C3; friend void f3(); friend class C4; friend void f4();
};
// OK (defined in enclosing namespace)
// First declared in N and assumed to be in N
class C3 {}; // friend of C void f3() { C x; x.x = 1; } // OK: friend of C }// namespace N
class C4 { }; // not friend of N::C
void f4() { N::C x; x.x = 1; } // error :x is private and f4() is not a friend of N::C
```

即使友元函数没有在直接外围作用域中声明，也可以通过其参数找到它（§14.2.4）。例如：

```
void f(Matrix& m)
{
invert(m); // Matrix's friend invert()
}
```

因此，应当在外围作用域中显式声明友元函数，或者让它接受一个属于其类的参数，或接受一个派生自该类的类的参数。否则，无法调用该友元函数。例如：

```
// no f() in this scope

class X {
friend void f(); // useless
friend void h(const X&); // can be found through its argument
};

void g(const X& x) {
f(); // no f() in scope h(x); // X's friend h()
}
```

### 19.4.2 友元与成员

什么时候应该使用友元函数，什么时候成员函数是指定某种操作的更好选择？

首先，我们尽量减少访问类表示的函数数量，并尽力使访问函数集合尽可能合理。因此，第一个问题不应是“它应该是成员、静态成员，还是友元？”而应该是“它真的需要访问权限吗？”通常，需要访问权限的函数集合比我们最初愿意相信的要小。有些操作必须是成员，例如构造函数、析构函数和虚函数（§3.2.3、§17.2.5），但通常仍然存在选择。由于成员名称属于类的局部作用域，需要直接访问类表示的函数应当是成员，除非存在特定理由使其成为非成员。

考虑一个类 `X`，它为某个操作提供了多种调用方式：

```
class X {
// ...
X(int);

int m1(); // member int m2() const;

friend int f1(X&); // friend,not member
friend int f2(const X&);
friend int f3(X);
};
```

成员函数只能针对其所属类的对象调用；不会对 `.` 或 `->` 最左侧的操作数应用用户定义的转换（但请参见 §19.2.3）。例如：

```
void g()
{
99.m1(); // error :X(99).m1() not tried 99.m2(); // error :X(99).m2() not tried
```

第 19.4.2 节 友元与成员 575

全局函数 `f1()` 具有类似的性质，因为不会对非 `const` 引用参数使用隐式转换（§7.7）。但是，可以对 `f2()` 和 `f3()` 的参数应用转换：

```
void h()
{
f1(99); // error :f1(X(99)) not tried: non-const X& argument
f2(99); // OK: f2(X(99)); const X& argument
f3(99); // OK: f3(X(99)); X argument
}
```

因此，修改类对象状态的操作应当是成员函数，或者是接受非 `const` 引用参数（或非 `const` 指针参数）的函数。

修改操作数的运算符（例如 `=`、`*=` 和 `++`）对于用户定义类型而言，最自然的定义方式是成员函数。相反，如果希望对操作的所有操作数都进行隐式类型转换，实现该操作的函数就必须是非成员函数，并且接受 `const` 引用参数或非引用参数。对于那些应用于基本类型时不要求操作数为左值的运算符（例如 `+`、`–` 和 `||`），其实现函数通常就是这种情况。然而，这类运算符通常需要访问
