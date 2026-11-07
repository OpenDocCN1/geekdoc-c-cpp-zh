
### 声明静态数据成员

数据成员属于类，其声明必须包含在类定义中；*静态*成员必须用关键字 *static* 限定。下面展示如何在类定义中声明一个名为 *count* 的*静态*数据成员。

```cpp
class Rectangle
{
  private:
    ...
    static int count;          // Static data member
  public:
    ...
};
```

### 初始化静态数据成员

我们知道，实例数据成员通常在构造函数中初始化，但*静态*数据成员不属于任何实例，这意味着它不能在构造函数中初始化。*静态*数据成员必须在类定义之后初始化。这意味着它必须在程序的全局区域中初始化。我们将其写在类定义之后。我们必须通过在定义中添加类名和类作用域运算符（::）来表明它属于该类，但不应添加 *static* 限定符。它在类的定义部分已经被限定为*静态*数据成员。下面展示如何初始化已在类内声明的*静态*成员 *count*。

```cpp
int Rectangle::count = 0;          // initialization of static data member
```

## 7.5.2 静态成员函数

在声明并初始化*静态*数据成员之后，我们必须找到访问它的方法（例如，打印其值）。由于*静态*数据成员通常是*私有*的，我们需要一个*公有*成员函数来实现。虽然这可以通过实例成员函数完成，但通常我们为此使用*静态*成员函数。*静态*成员函数可以通过对象访问*静态*数据成员，也可以在不存在对象时通过类名访问。换句话说，使用*静态*成员函数使我们能够在实例想要访问相应*静态*数据成员时，或应用程序需要访问它时，访问该成员。注意，*静态*成员函数没有宿主对象，因为它不与任何实例关联。

> **静态成员函数没有宿主对象。**

### 声明静态成员函数

*静态*成员函数与*静态*数据成员一样，属于类。它应在类内声明，但必须用关键字 *static* 限定。下面展示如何向 *Rectangle* 类添加一个*静态*成员函数 *getCount*，以获取*静态*数据成员 *count* 的值。

```cpp
class Rectangle
{
    private:
        ...
        static int count;              // Static data member
    public:
        static int getCount();         // Static member function
        ...
};
```

### 定义静态成员函数

静态成员函数必须像实例成员函数一样在类外定义。静态成员函数的定义与实例成员函数的定义没有区别。如果我们想判断一个函数定义是实例成员函数还是静态成员函数，需要参考其声明。

```cpp
int Rectangle::getCount()
{
    return count;
}
```

注意，我们不能使用 const 限定符，因为没有宿主对象。

### 调用静态成员函数

静态成员函数既可以通过实例调用，也可以通过类调用（例如 Rectangle）。通过实例调用静态成员函数时，我们使用与调用实例成员函数相同的语法；通过类调用静态成员函数时，我们使用类名和类解析运算符（::）。下面展示这两种方法。

```cpp
rect.getCount ();             // Through an instance
Rectangle :: getCount();      // Through the class
```

警告：我们不能使用静态成员函数访问实例数据成员，因为静态成员函数没有隐藏的 this 指针，而该指针定义了需要引用的实例。

> 静态成员函数不能用于访问实例数据成员，因为它没有 this 指针参数。

另一方面，实例成员函数可以用于访问静态数据成员（不使用 this 指针），但我们通常避免这样做。良好的做法是使用实例成员函数访问实例数据成员，使用静态成员函数访问静态数据成员。我们建议在程序中象征性地将实例成员的领域与静态成员分开，如图 7.13 所示。

![](img/d68f6199646ca63591a6d8419e0ed4ba_323_0.png)

**图 7.13** 实例与静态领域的分离

**例 7.4**

在本例中，我们编写一个程序，使用 *Rectangle* 类测试静态数据成员及相应的静态成员函数。程序 7.5 还展示了如何对实例进行计数。

**程序 7.5** 测试静态成员

```cpp
/****************************************************
 * A program to create objects and count them.       *
 ****************************************************/
#include <iostream>
using namespace std;
/****************************************************
 * Definitions of the class Rectangle              *
 ****************************************************/
class Rectangle
{
private:
    double length;
    double height;
    static int count;   // Static data member
public:
    Rectangle (double length, double height);
    Rectangle ();
    ~Rectangle ();
    Rectangle (const Rectangle& rect);
    static int getCount ();  // Static member function
};
// Initialization of static data member
int Rectangle :: count = 0;
/****************************************************
 * Definitions of instance member functions        *
 ****************************************************/
// Definition of parameter constructor

Rectangle :: Rectangle (double len, double hgt)
: length (len), height (hgt)
{
    count++;
}
// Definition of default constructor
Rectangle :: Rectangle ()
: length (0.0), height (0.0)
{
    count++;
}
// Definition of copy constructor
Rectangle :: Rectangle (const Rectangle& rect)
: length (rect.length), height (rect.height)
{
    count++;
}
// Definition of destructor
Rectangle :: ~Rectangle ()
{
    count--;
}
/************************************************************
 * Definitions of the static member function
 ************************************************************/
int Rectangle :: getCount ()
{
    return count;
}

/************************************************************
 * Application to create and count Rectangle objects        *
 ************************************************************/
int main ()
{
    {
        Rectangle rect1 (3.2, 1.2);
        Rectangle rect2 (1.5, 2.1);
        Rectangle rect3;
        Rectangle rect4 (rect1);
        Rectangle rect5 (rect2);
        cout << "Count of objects: " << rect5.getCount() << endl;
    }
    cout << "Count of objects: " << Rectangle::getCount();
    return 0;
}
```

运行：

```
Count of objects: 5
Count of objects: 0
```

静态成员的声明在第 14 行使用关键字 *static* 完成。该成员的初始化在第 23 行于类外完成。函数的定义在第 53–56 行完成。我们在 *main* 函数中添加了一个嵌套块（第 63–70 行），以创建一个创建对象的作用域。这意味着在该块之外没有实例，但我们可以使用类名检查静态数据成员的值。在离开该块之前，我们创建了五个实例；我们通过最后一个对象检查静态数据成员的值，发现它为 5。离开该块之后，所有实例都被销毁，我们可以通过类名检查静态数据成员的值，看到它为 0。

**例 7.5**

在本例中，我们设计一个表示支票账户的类。我们为这个类设计的仅有的两个实例数据成员是*账号*和*余额*。虽然余额可以在创建实例时由类的用户初始化，但账号不能由用户输入，因为它必须是唯一的。为了防止账号重复，我们使用了一个名为 *base* 的静态数据成员，它初始化为 0，并在每开立一个新账户时递增。我们按惯例给这个静态数据成员加上 100000，使其成为一个较大的数字。我们不需要静态成员函数，因为不检查静态数据成员的值。程序 7.6 展示了这个类及其应用。

**程序 7.6** 银行账户示例

```cpp
/********************************************************
 * A program to declare, define, and use a bank account class       *
 ********************************************************/
#include <iostream>
#include <cassert>
using namespace std;

/********************************************************
 * Class Definition (Declaration of all members)                  *
 ********************************************************/
class Account
{
    private:
        long accNumber;
        double balance;
```
