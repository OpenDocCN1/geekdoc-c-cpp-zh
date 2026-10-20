
很接近。不过，你仍然可以用接受 const 左值引用的传统构造函数测出一个轻微的缺点。不过，这肯定要求启用良好的优化。

除了尝试各种不同的测试程序之外，你还可以使用 basics/initperf.cpp 作为组合程序，在你喜欢的平台上执行所有这些不同的测量。

然而，你可能会有一些非常昂贵的成员，无法从移动语义中获益（例如包含 10000 个 double 值的数组）：

```
class Person {
  private:
    std::string name;
    std::array<double, 10000> values;  // move can’t optimize here
  public:
    ...
};
```

在这种情况下，按值接收 10000 个 double 作为初始参数并移动的做法就会产生问题。我们必须复制该参数两次，这几乎需要两倍的时间。完整的测量示例程序见 basics/initbigperf.cpp。

### 4.3.5 成员初始化小结

总之，要初始化那些移动语义能造成显著差异的成员（字符串、容器，或包含此类成员的类/数组），你应该采用以下移动语义方案之一：

- 将参数从按左值引用接收改为按值接收，并将其移动到成员中
- 为移动语义重载构造函数

第一种方案只要求我们有一个构造函数，因此代码更易于维护。不过，这确实会导致多余的移动操作。因此，如果移动操作可能很耗时，最好使用多个重载。

例如，如果我们的类有一个字符串和一个值 vector，按值接收并移动通常是正确的做法：

```
class Person {
  private:
    std::string name;
    std::vector<std::string> values;
  public:
    Person(std::string n, std::vector<std::string> v)
      : name{std::move(n)}, values{std::move(v)} {
    }
    ...
};
```

然而，如果我们有 std::array 成员，最好进行重载，因为即使成员会被移动，移动 std::array 仍然需要相当多的时间：

```
class Person {
private:
    std::string name;
    std::array<std::string, 1000> values;
public:
    Person(std::string n, const std::array<std::string, 1000>& v)
        : name{std::move(n)}, values{v} {
    }
    Person(std::string n, std::array<std::string, 1000>&& v)
        : name{std::move(n)}, values{std::move(v)} {
    }
    ...
};
```

### 4.3.6 我们现在是否应该总是按值传递并移动？

上面的讨论引出了一个问题：我们现在是否应该总是按值接收参数，然后将它们移动以设置内部值或成员？答案是否定的。

这里讨论的特殊情况是我们创建并初始化一个新值。在这种情况下，这种策略是值得的。如果我们已经有一个值需要更新或修改，使用这种方法会适得其反。

一个简单的例子是 setter。考虑以下 Person 类的实现：

```
class Person {
private:
    std::string first;  // first name
    std::string last;   // last name
public:
    Person(std::string f, std::string l)
        : first{std::move(f)}, last{std::move(l)} {
    }
    ...
    void setFirstname(std::string s) {      // take by value
        first = std::move(s);               // and move
    }
    ...
};
```

假设我们按如下方式使用这个类：

```
Person p{"Ben", "Cook"};
std::string name1{"Ann"};
std::string name2{"Constantin Alexander"};

p.setFirstname(name1);
p.setFirstname(name2);
p.setFirstname(name1);
p.setFirstname(name2);
```

每次设置新的 firstname 时，我们都会创建一个新的临时参数 s，它会分配自己的内存，然后被移动到成员的值中。因此，我们有四次分配（前提是我们没有 SSO，即短字符串优化）。

现在考虑我们以传统方式实现 setter，接受 const 左值引用：

```
class Person {
private:
    std::string first;  // first name
    std::string last;   // last name
public:
    Person(std::string f, std::string l)
    : first{std::move(f)}, last{std::move(l)} {
    }
    ...
    void setFirstname(const std::string& s) {  // take by reference
        first = s;                           // and assign
    }
    ...
};
```

将 s 绑定到传入的参数不会创建新字符串。此外，赋值运算符只会在新长度超过当前为该值分配的内存量时才分配新内存。这意味着，由于我们已经拥有一个值，按值接收参数并移动的方法可能会适得其反。

你可能想知道是否应该重载 setter，以便在新长度超过现有长度时从移动语义中获益：

```
class Person {
private:
    std::string first;  // first name
    std::string last;   // last name
public:
    Person(std::string f, std::string l)
    : first{std::move(f)}, last{std::move(l)} {
    }
    ...
    void setFirstname(const std::string& s) {  // take by lvalue reference
        first = s;                           // and assign
    }
    void setFirstname(std::string&& s) {       // take by rvalue reference
        first = std::move(s);                // and move assign
    }
    ...
};
```

然而，即使这种方法也可能适得其反，因为移动赋值可能会缩小 first 的容量：

```
Person p{"Ben", "Cook"};

p.setFirstname("Constantin Alexander");  // would allocate enough memory
p.setFirstname("Ann");                  // would reduce capacity
p.setFirstname("Constantin Alexander");  // would have to allocate again
```

即使使用移动语义，设置已有值的最佳方法仍然是通过 const 左值引用接收新值，并在不使用 std::move() 的情况下进行赋值。

按值接收参数并将其移动到需要新值的地方，只有在我们把传入的值作为新值存储到某处时才有用（因为此时反正都需要为它分配新内存）。在修改已有值时，这种策略可能会适得其反。

然而，初始化成员并不是“按值接收并移动”的唯一应用。（成员）函数向容器中添加新值是另一个应用：

```
class Person {
private:
    std::string name;
    std::vector<std::string> values;
public:
    Person(std::string n, std::vector<std::string> v)
        : name{std::move(n)}, values{std::move(v)} {
    }
    ...
    // better pass by value and move to create a new element:
    void addValue(std::string s) {        // take by value
        values.push_back(std::move(s));    // and move into the collection
    }
    ...
};
```

## 4.4 类层次结构中的移动语义

正如我们所看到的，任何拷贝构造函数、拷贝赋值或析构函数的声明都会禁用移动语义的自动支持。这也适用于多态基类。不过，还有一些额外的方面需要考虑。

### 4.4.1 实现多态基类

多态基类通常会引入你可以对所有派生类对象调用的虚成员函数。例如：

```
class GeoObj {
public:
    virtual void draw() const = 0;    // pure virtual function (introducing the API)
    ...
virtual ~GeoObj() = default;        // let delete call the right destructor
...    // other special member functions due to the problem of slicing
};
```

在这个基类中，移动语义被禁用，这意味着如果我们移动一个几何对象，基类中在此声明的成员不会自动获得移动语义的支持。即使我们有受保护的拷贝构造函数和被删除的赋值运算符，情况也是如此；为了避免切片问题，多态基类中通常应该有这样两个函数。

只要基类没有引入成员，不支持移动语义就没有影响。然而，如果这个基类中有昂贵的成员，你就禁用了对它的移动支持。例如：

```
class GeoObj {
protected:
    std::string name;                // name of the geometric object
public:
    ...
    virtual void draw() const = 0;   // pure virtual function (introducing the API)
    ...
    virtual ~GeoObj() = default;     // disables move semantics for name
    ...    // other special member functions due to the problem of slicing
};
```

要重新启用移动语义，你可以显式地将移动操作声明为 defaulted。然而，正如我们刚才了解到的，这会禁用拷贝特殊成员函数。因此，如果你希望保留这些函数，就必须显式提供它们。

### 处理切片问题

然而，还存在切片问题。考虑以下代码，它使用基类 GeoObj 的引用来引用派生类 Circle 的对象：

```
Circle c1{...}, c2{...};

GeoObj& geoRef{c1};
geoRef = c2;    // OOPS: uses GeoObj::operator=() and assigns no Circle members
```

因为我们调用的是 GeoObj 的赋值运算符，而该运算符不是虚函数，所以编译器会调用 GeoObj::operator=()，它不会处理任何派生类的成员。即使将赋值运算符声明为 virtual 也无济于事，因为派生类的运算符并不会覆盖基类的赋值运算符（第二个操作数的参数类型不同）。

为了避免这个问题，你应该在多态类层次结构中禁用赋值运算符。此外，如果类不是抽象类，你还应该避免提供公共拷贝构造函数，以禁用对基类的隐式类型转换。因此，带有移动语义（和成员）的多态基类应该声明如下：

```
class GeoObj {
protected:
    std::string name;                // name of the geometric object
```
