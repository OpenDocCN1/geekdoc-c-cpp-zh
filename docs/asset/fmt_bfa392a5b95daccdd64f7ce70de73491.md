
```
void f1(X a) // traditional use
{
X v[200];
X* p = &v[0];
p--;
*p=a; // oops: p out of range, uncaught
++p;
*p=a; // OK
}
```

这里，我们可能希望将`X*`替换为类`Ptr<X>`的对象，只有当它确实指向一个`X`时，才能对其解引用。我们还希望确保只有当`p`指向数组中的对象时，才能对其进行自增和自减，并且自增和自减操作的结果仍然指向该数组中的对象。也就是说，我们希望得到类似下面的代码：

```
void f2(Ptr<X> a) // checked
{
X v[200];
Ptr<X> p(&v[0],v);
p--;
*p=a; // run-time error: p out of range
++p;
```

```
*p=a; // OK
}
```

自增和自减运算符在 C++ 运算符中是独特的，因为它们既可以用作前缀运算符，也可以用作后缀运算符。因此，我们必须为`Ptr<T>`定义前缀和后缀自增、自减运算符。例如：

```
template<typename T>
class Ptr {
T* ptr;
T* array;
int sz;
public:
template<int N>
Ptr(T* p, T(&a)[N]); // bind to array a, sz==N, initial value p
Ptr(T* p, T* a, int s); // bind to array a of size s, initial value p
Ptr(T*p); // bind to single object, sz==0, initial value p

Ptr& operator++(); // prefix
Ptr operator++(int); // postfix
Ptr& operator--(); // prefix
Ptr operator--(int); // postfix
T& operator*(); // prefix
};
```

`int`参数用于表示该函数将被用于`++`的后缀形式。这个`int`从不使用；该参数只是一个哑元，用于区分前缀形式和后缀形式。记住哪个版本的`operator++`是前缀形式的方法是：不带哑元参数的版本是前缀形式，这一点与其他一元算术和逻辑运算符完全相同。哑元参数仅用于这种“特殊的”后缀`++`和`--`。

考虑在设计中省略后缀`++`和`--`。它们不仅在语法上比较特殊，实现起来通常也比前缀版本略困难，效率更低，而且使用频率也更低。例如：

```
template<typename T>
Ptr& Ptr<T>::operator++() // return the current object after incrementing
{
// ... check that ptr+1 can be pointed to ...
return *++ptr;
}
template<typename T>
Ptr Ptr<T>::operator++(int) // increment and return a Ptr with the old value
{
// ... check that ptr+1 can be pointed to ...
Ptr<T> old {ptr,array,sz};
++ptr;
return old;
}
```

前缀自增运算符可以返回其对象的引用。后缀自增运算符则必须创建一个新对象并返回它。

使用`Ptr`后，该示例等价于：

```
void f3(T a) // checked
{
T v[200];
Ptr<T> p(&v[0],v,200);
p.operator--(0); // suffix: p--
p.operator*() = a; // run-time error: p out of range
p.operator++(); // prefix: ++p
p.operator*() = a; // OK
}
```

完整实现类`Ptr`的任务留作练习。§27.2.2 给出了一个在可继承性方面行为正确的指针模板。

# 19.2.5 分配和释放

运算符`new`（§11.2.3）通过调用一个`operator new()`来获取内存。同样，运算符`delete`通过调用一个`operator delete()`来释放内存。用户可以重新定义全局的`operator new()`和`operator delete()`，也可以为特定类定义`operator new()`和`operator delete()`。

使用标准库类型别名`size_t`（§6.2.8）表示大小时，全局版本的声明如下：

```
void * operator new(size_t);
void* operator new[](size_t);
void operator delete(void*,size_t);
void operator delete[](void*,size_t);
```

```
// use for individual object // use for array
// use for individual object // use for array
```

```
// for more versions, see §11.2.4
```

也就是说，当`new`需要为`X`类型的对象从自由存储区获取内存时，它会调用`operator new(sizeof(X))`。同样，当`new`需要为包含`N`个`X`类型对象的数组从自由存储区获取内存时，它会调用`operator new[](N*sizeof(X))`。一个`new`表达式可能会请求多于`N*sizeof(X)`所表示的内存，但它始终会以字符数量（即字节数量）为单位进行请求。

替换全局的`operator new()`和`operator delete()`并非胆小者所为，也不推荐这样做。毕竟，其他人可能依赖默认行为的某些方面，甚至可能已经提供了这些函数的其他版本。

一种更有选择性、通常也更好的方法，是为特定类提供这些操作。这个类可能是许多派生类的基类。例如，我们可能希望让类`Employee`为自身及其所有派生类提供专用的分配器和释放器：

```
class Employee {
public:
// ...
void* operator new(size_t);
void operator delete(void*,size_t);
void* operator new[](size_t);
void operator delete[](void*,size_t);
};
```

成员`operator new()`和`operator delete()`隐式地都是静态成员。因此，它们没有`this`指针，也不会修改对象。它们提供由构造函数进行初始化、由析构函数进行清理的存储空间。

```
void* Employee::operator new(size_t s)
{
// allocate s bytes of memory and return a pointer to it
}
void Employee::operator delete(void* p, size_t s)
{
if (p) { // delete only if p!=0; see §11.2, §11.2.3
// assume p points to s bytes of memory allocated by Employee::operator new()
// and free that memory for reuse
}
}
```

此前神秘的`size_t`参数的用途现在显而易见了。它表示被删除对象的大小。删除一个“普通的”`Employee`时，参数值为`sizeof(Employee)`；删除一个派生自`Employee`且自身没有`operator delete()`的`Manager`时，参数值为`sizeof(Manager)`。这样，类专用分配器就不必在每次分配中存储大小信息。当然，类专用分配器也可以像通用分配器一样存储这些信息，并忽略传递给`operator delete()`的`size_t`参数。不过，这样做会使其难以在通用分配器的速度和内存消耗方面取得显著改进。

编译器如何知道应向`operator delete()`提供正确的大小？`delete`操作中指定的类型与被删除对象的类型相匹配。如果通过指向基类的指针删除对象，那么该基类必须具有虚析构函数（§17.2.5），才能提供正确的大小：

```
Employee* p = new Manager; // potential trouble (the exact type is lost)
// ...
delete p; // hope Employee has a virtual destructor
```

原则上，释放工作随后由析构函数完成（析构函数知道其类的大小）。

# 19.2.6 用户定义字面量

C++ 为各种内置类型提供了字面量（§6.2.6）：

```
123 // int
1.2 // double
1.2F // float
```

```
‘a’ // 字符
1ULL // 无符号长长整型
0xD0 // 十六进制无符号数
"as" // C 风格字符串（const char[3]）
```

此外，我们还可以为用户定义类型定义字面量，并为内置类型定义新的字面量形式。例如：

```
“Hi!”s // 字符串，而不是“以零结尾的 char 数组”
1.2i // 虚数
101010111000101b // 二进制数
123s // 秒
123.56km // 不是英里！（单位）
1234567890123456789012345678901234567890x // 扩展精度
```

这种用户定义字面量通过字面量运算符实现。字面量运算符可以将带有给定后缀的字面量映射为所需的类型。字面量运算符的名称是 `operator"""` 后跟后缀。例如：

```
constexpr complex<double> operator"""i(long double d) // 虚数字面量
{
return {0,d}; // complex 是字面量类型
}
```

```
std::string operator"""s(const char* p, size_t n) // std::string 字面量
{
return string{p,n}; // 需要从自由存储区分配内存
}
```

这两个运算符分别定义了后缀 i 和 s。我使用 constexpr 来启用编译期求值。有了它们，我们就可以这样写：

```
template<typename T> void f(const T&);

void g() {
f("Hello"); // 传递指向 char* 的指针
f("Hello"s); // 传递（五字符）字符串对象 f("Hello\n"s); // 传递（六字符）字符串对象

auto z = 2+1i; // complex{2,1}
}
```

其基本的（实现）思想是：在解析出可能是字面量的内容后，编译器总会检查其是否带有后缀。用户定义字面量机制只是允许用户指定新的后缀，并定义如何处理此前的字面量。不可能重新定义内置字面量后缀的含义，也不能扩展字面量的语法。

有四种字面量可以添加后缀，从而构成用户定义字面量（§iso.2.14.8）：

- 整数字面量（§6.2.4.1）：由接受 unsigned long long 或 `const char*` 参数的字面量运算符，或由模板字面量运算符接受，例如 `123m` 或 `12345678901234567890X`

- 浮点字面量（§6.2.5.1）：由接受 `long double` 或 `const char*` 参数的字面量运算符，或由模板字面量运算符接受，例如 `12345678901234567890.976543210x` 或 `3.99s`

- 字符串字面量（§7.3.2）：由接受一对（`const char*`，`size_t`）参数的字面量运算符接受，例如 `“string”s` 和 `R”(Foo\bar)”_path`

- 字符字面量（§6.2.3.2）：由接受 char、wchar_t、char16_t 或 char32_t 类型字符参数的字面量运算符接受，例如 `‘f’_runic` 或 `u’ BEEF’_w`。例如，我们可以定义一个字面量运算符，用于收集无法由任何内置整数类型表示的整数值的数字：

```
Bignum operator""" x(const char* p)
{
return Bignum(p);
}
```

```
void f(Bignum);
f(123456789012345678901234567890123456789012345x);
```

这里，C 风格字符串 “123456789012345678901234567890123456789012345” 被传递给 operator""" x()。注意，我没有将这些数字放在双引号中。我要求运算符接收一个 C 风格字符串，而编译器根据所提供的数字为我生成并传递了这个字符串。

若要将程序源文本中的 C 风格字符串传递给字面量运算符，我们需要同时请求字符串及其字符数。例如：

```
string operator""" s(const char* p, size_t n);
```

```
string s12 = “one two”s; // 调用 operator ""("one two",7)
string s22 = “two\ntwo”s; // 调用 operator ""("two\ntwo",7)
string sxx = R”(two\ntwo)”s; // 调用 operator ""("two\ntwo",8)
```

在原始字符串（§7.3.2.1）中，“\n”表示两个字符 ‘\’ 和 ‘n’。

之所以要求提供字符数，是因为如果我们想要“一种不同类型的字符串”，几乎总是也需要知道字符数。

只接受 `const char*` 参数（不接受长度参数）的字面量运算符可以应用于整数字面量和浮点字面量。例如：

```
string operator""" SS(const char*p); // 警告：这不会按预期工作
string s12 = “one two”SS; string s13 = 13SS;
// 错误：没有适用的字面量运算符 // 可以，但为什么有人要这样做？将数值转换为字符串的字面量运算符可能会令人相当困惑。模板字面量运算符是一种将其参数作为模板参数包，而不是函数参数来接收的字面量运算符。例如：
```

```
template<char...>
constexpr int operator""" _b3(); // 三进制，即以 3 为基数
```

本节介绍的相对简单的字符串类展示了若干技术，这些技术对于设计和实现使用约定俗成运算符的类非常有用。这个 String 是标准库字符串（§4.2，第 36 章）的简化版本。String 提供值语义、对字符的检查式和非检查式访问、流 I/O、对 rangefor 循环的支持、相等运算以及连接运算符。我还添加了一个 String 字面量，而 std::string 尚未提供这种字面量。

为了与 C 风格字符串（包括字符串字面量（§7.3.2））实现简单互操作，我将字符串表示为以零结尾的字符数组。为实现真实的使用场景，我实现了短字符串优化。也就是说，只有少量字符的 String 会将这些字符存储在类对象本身中，而不是自由存储区中。这可以优化短字符串的使用。经验表明，对于大量应用而言，大多数字符串都很短。在多线程系统中，这种优化尤其重要，因为此时通过指针（或引用）共享数据不可行，而自由存储区的分配和释放相对昂贵。

为了使 String 能够通过在末尾添加字符来高效地“增长”，我实现了一种为这种增长保留额外空间的方案，其原理类似于 vector（§13.6.1）所采用的方案。这使 String 成为各种输入形式的合适目标。

编写一个更好的字符串类，或编写一个提供更多功能的字符串类，是一项很好的练习。完成练习后，我们可以丢弃自己的练习成果，改用 std::string（第 36 章）。

# 19.3.1 基本操作

类 String 提供通常的一组构造函数、析构函数和赋值操作（§17.1）：

```
class String {
public:
String(); // 默认构造函数：x{""}
explicit String(const char*p); // 从 C 风格字符串构造：x{"Euler"}
String(const String&); // 复制构造函数 String& operator=(const String&); // 复制赋值 String(String&& x); // 移动构造函数 String& operator=(String&& x); // 移动赋值
~String() { if (short_max<sz) delete[] ptr; } // 析构函数
// ...
};
```

这个 String 具有值语义。也就是说，在执行赋值 s1=s2 后，字符串 s1 和 s2 完全彼此独立，之后对其中一个字符串的修改不会影响另一个字符串。另一种选择是让 String 具有指针语义，即允许在 s1=s2 之后对 s2 的修改也影响 s1 的值。在合理的情况下，我更倾向于使用值语义；complex、vector、Matrix 和 string 都是例子。不过，要使值语义具有可接受的开销，我们需要在不需要复制时通过引用传递 String，并实现移动语义（§3.3.2、§17.5.2）来优化返回操作。

String 稍微复杂的表示方式见 §19.3.3。注意，它

需要用户定义版本的复制操作和移动操作。

# 19.3.2 对字符的访问

字符串访问运算符的设计是一个困难的问题，因为理想情况下，访问应当使用约定俗成的表示法（即使用 []），效率最高，并且进行范围检查。

遗憾的是，这些性质无法同时具备。这里，我遵循标准库的做法：使用传统的 [] 下标表示法提供高效但不进行检查的操作，同时提供进行范围检查的 at() 操作：
