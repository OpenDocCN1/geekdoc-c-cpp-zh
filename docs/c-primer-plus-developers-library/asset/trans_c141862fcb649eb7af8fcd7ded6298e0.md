

指向由 `new` 分配的内存。然后，当 `Singer` 对象过期时，调用 `~Singer()` 析构函数来释放该内存至关重要。

现在考虑下面的代码：

```cpp
Employee * pe = new Singer; // legal because Employee is base for Singer
...
delete pe;                  // ~Employee() or ~Singer()?
```

如果采用默认的静态绑定，`delete` 语句将调用 `~Employee()` 析构函数。这会释放 `Singer` 对象中 `Employee` 部分所指向的内存，但不会释放新类成员所指向的内存。然而，如果析构函数是虚函数，同样的代码将调用 `~Singer()` 析构函数，它释放 `Singer` 部分指向的内存，然后调用 `~Employee()` 析构函数来释放 `Employee` 部分指向的内存。

注意，这意味着即使基类不需要显式析构函数的服务，也不应依赖默认析构函数。相反，应提供一个虚析构函数，即使它什么也不做：

```cpp
virtual ~BaseClass() { }
```

顺便说一句，即使一个类不打算作为基类，拥有虚析构函数也不是错误；只是效率问题。

> **提示**
> 
> 通常，即使基类不需要析构函数，你也应该为基类提供虚析构函数。

## 友元

友元不能是虚函数，因为友元不是类成员，只有成员才能是虚函数。如果这对设计造成问题，你可以让友元函数在内部使用虚成员函数来绕过这一问题。

## 不重定义

如果派生类未能重定义一个函数（无论是否为虚函数），该类将使用该函数的基类版本。如果派生类处于很长的派生链中，它将使用该函数最近定义的版本。例外情况是基类版本被隐藏，如下所述。

## 重定义隐藏方法

假设你创建了类似下面的代码：

```cpp
class Dwelling
{
public:
    virtual void showperks(int a) const;
...
};
class Hovel : public Dwelling
{
public:
    virtual void showperks() const;
    ...
};
```

这会导致一个问题。你可能会得到类似如下的编译器警告：

```text
Warning: Hovel::showperks(void) hides Dwelling::showperks(int)
```

或者你根本不会收到警告。无论如何，这段代码具有以下含义：

```cpp
Hovel trump;
trump.showperks();    // valid
trump.showperks(5);   // invalid
```

新定义定义了一个不带参数的 `showperks()` 函数。这种重定义并不会产生该函数的两个重载版本，而是 *隐藏* 了接受 `int` 参数的基类版本。简而言之，重定义继承的方法不是重载的变体。如果你在派生类中重定义一个函数，它不仅仅是覆盖相同函数签名的基类声明。相反，它会隐藏基类中所有同名的方法，无论参数签名如何。

这个事实引出了一些经验法则。首先，如果你重定义一个继承的方法，需要确保与原始原型完全匹配。这个规则的一个相对较新的例外是，返回类型为指向基类的引用或指针时，可以被指向派生类的引用或指针替换。这个特性被称为 *返回类型协变*，因为返回类型允许与类类型平行变化：

```cpp
class Dwelling
{
public:
    // a base method
    virtual Dwelling & build(int n);
    ...
};
class Hovel : public Dwelling
{
public:
    // a derived method with a covariant return type
    virtual Hovel & build(int n);  // same function signature
    ...
};
```

注意，这个例外仅适用于返回值，不适用于参数。其次，如果基类声明是重载的，你需要在派生类中重新定义所有基类版本：

```cpp
class Dwelling
{
public:
// three overloaded showperks()
        virtual void showperks(int a) const;
        virtual void showperks(double x) const;
        virtual void showperks() const;
        ...
};
class Hovel : public Dwelling
{
public:
// three redefined showperks()
        virtual void showperks(int a) const;
        virtual void showperks(double x) const;
        virtual void showperks() const;
        ...
};
```

如果你只重定义一个版本，其他两个版本将被隐藏，派生类对象无法使用它们。注意，如果不需要更改，重定义可以简单地调用基类版本：

```cpp
void Hovel::showperks() const {Dwelling::showperks();}
```

## 访问控制：protected

到目前为止，本书中的类示例使用关键字 `public` 和 `private` 来控制对类成员的访问。还有另一种访问类别，用关键字 `protected` 表示。`protected` 关键字类似于 `private`，外部世界只能通过使用公有类成员来访问 `protected` 部分中的类成员。`private` 和 `protected` 之间的区别仅在从基类派生的类中体现。派生类的成员可以直接访问基类的 `protected` 成员，但不能直接访问基类的 `private` 成员。因此，`protected` 类别的成员对外部世界而言行为类似 `private` 成员，但对派生类而言行为类似 `public` 成员。

例如，假设 `Brass` 类将 `balance` 成员声明为 `protected`：

```cpp
class Brass
{
protected:
        double balance;
...
};
```

在这种情况下，`BrassPlus` 类可以不使用 `Brass` 方法而直接访问 `balance`。例如，`BrassPlus::Withdraw()` 的核心代码可以这样写：

```cpp
void BrassPlus::Withdraw(double amt)
{
    if (amt < 0)
        cout << "Withdrawal amount must be positive; "

             << "withdrawal canceled.\n";
    else if (amt <= balance)        // access balance directly
        balance -= amt;
    else if ( amt <= balance + maxLoan - owesBank)
    {
        double advance = amt - balance;
        owesBank += advance * (1.0 + rate);
        cout << "Bank advance: $" << advance << endl;
        cout << "Finance charge: $" << advance * rate << endl;
        Deposit(advance);
        balance -= amt;
    }
    else
        cout << "Credit limit exceeded. Transaction cancelled.\n";
}
```

使用 `protected` 数据成员可能会简化代码编写，但存在设计缺陷。例如，继续使用 `BrassPlus` 示例，如果 `balance` 是 `protected`，你可以编写如下代码：

```cpp
void BrassPlus::Reset(double amt)
{
    balance = amt;
}
```

`Brass` 类的设计初衷是让 `Deposit()` 和 `Withdraw()` 接口成为修改 `balance` 的唯一途径。但 `Reset()` 方法实际上使 `balance` 对 `BrassPlus` 对象而言变成了公有变量，例如忽略了 `Withdraw()` 中的保护措施。

> **警告**
> 
> 对于类数据成员，你应该优先使用 `private` 而不是 `protected` 访问控制，并且应该使用基类方法为派生类提供对基类数据的访问。

然而，`protected` 访问控制对于成员函数可能非常有用，它允许派生类访问不对外公开的内部函数。

## 抽象基类

到目前为止，你已经了解了简单的继承和更复杂的多态继承。下一步更复杂的层次是抽象基类（ABC）。让我们看一些为 ABC 提供背景的编程情况。

有时应用 *是一个* 规则并不像看起来那么简单。例如，假设你正在开发一个图形程序，该程序应当表示圆和椭圆等内容。圆是椭圆的一种特殊情况：它是长轴与短轴相同的椭圆。因此，所有圆都是椭圆，人们自然倾向于从 `Ellipse` 类派生 `Circle` 类。但当你深入细节时，可能会发现问题。

为了理解这一点，首先考虑 `Ellipse` 类可能包含哪些内容。数据成员可以包括椭圆中心的坐标、长半轴（长直径的一半）、短半轴（短直径的一半）以及一个方向角，该角度给出从水平坐标轴到长半轴的夹角。该类还可以包含移动椭圆、返回椭圆面积、旋转椭圆以及缩放长半轴和短半轴的方法：

```cpp
class Ellipse
{
private:
    double x;      // x-coordinate of the ellipse's center
    double y;      // y-coordinate of the ellipse's center
    double a;      // semimajor axis
    double b;      // semiminor axis
    double angle;  // orientation angle in degrees
    ...
public:
    ...
    void Move(int nx, int ny) { x = nx; y = ny; }
    virtual double Area() const { return 3.14159 * a * b; }
    virtual void Rotate(double nang) { angle += nang; }
    virtual void Scale(double sa, double sb) { a *= sa; b *= sb; }
    ...
};
```

现在假设你从 `Ellipse` 类派生一个 `Circle` 类：

```cpp
class Circle : public Ellipse
{
    ...
};
```

尽管圆是椭圆，但这种派生很别扭。例如，圆只需要一个值，即它的半径，来描述其大小和形状，而不是有长半轴（a）和短半轴（b）。`Circle` 构造函数可以通过将相同的值赋给 `a` 和 `b` 成员来处理这一点，但这样你就会对相同的信息有冗余的表示。`angle` 参数和 `Rotate()` 方法对于圆来说实际上没有意义，而 `Scale()` 方法就其现状而言，可以通过不同地缩放两个轴将圆变成非圆。你可以尝试用技巧来修复这些问题，例如在 `Circle` 类的 `private` 部分放置一个重定义的 `Rotate()` 方法，以便

