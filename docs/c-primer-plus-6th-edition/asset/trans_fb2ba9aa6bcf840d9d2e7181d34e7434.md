

# 1346 附录 J 章节习题答案

接下来，新的 `fill()` 应该是这样的：

```cpp
void fill(std::array<double, Seasons> & pa) // 已更改
{
    using namespace std;
    for (int i = 0; i < Seasons; i++)
    {
        cout << "Enter " << Snames[i] << " * expenses: ";
        cin >> pa[i]; // 已更改
    }
}
```

注意 (*pa)[i] 变为更简单的 pa[i]。

最后，`show()` 的唯一变化是函数头：
`void show(std::array<double, Seasons> & da)`

- 6. 这可以通过为第二个参数设置默认值来实现：
  `double mass(double d, double v = 1.0);`

  它也可以通过函数重载来实现：
  `double mass(double d, double v);`
  `double mass(double d);`

- b. 你不能为返回值使用默认值，因为必须从右到左提供默认值。你可以使用重载：
  `void repeat(int times, const char * str);`
  `void repeat(const char * str);`

- c. 你可以使用函数重载：
  `int average(int a, int b);`
  `double average(double x, double y);`

- d. 你不能这样做，因为两个版本的签名将相同。

- 7.
```cpp
template<class T>
T max(T t1, T t2) // 或 max(const T & t1, const T & t2)
{
    return t1 > t2 ? t1 : t2;
}
```

- 8.
```cpp
template<> box max(box b1, box b2)
{
    return b1.volume > b2.volume ? b1 : b2;
}
```

# 1347 第 9 章节习题答案

9. v1 是 float 类型，v2 是 float 类型，&v3 是 float & 类型，v4 是 int 类型，v5 是 double 类型。字面量 2.0 是 double 类型，所以乘积 2.0 * m 是 double 类型。

# 第 9 章节习题答案

- a. homer 自动是一个原子变量。
- b. secret 应该在一个文件中定义为外部变量，并在另一个文件中使用 `extern` 进行声明。
- c. topsecret 可以在在外部定义前加上 `static` 关键字，将其定义为具有内部链接的静态变量。或者也可以将其定义在匿名命名空间中。
- d. beencelled 应该通过在函数中的声明前加上 `static` 关键字来定义为局部变量。

- 2. `using` 声明（declaration）使命名空间中的单个名称可用，其作用域与该声明所在的声明区域对应。`using` 指令（directive）使命名空间中的所有名称可用。当你使用指令时，就好像包含该 `using` 声明和命名空间区域的最小声明区域内声明了这些名称。

- 3.
```cpp
#include <iostream>
int main() 
{
    double x;
    std::cout << "Enter value: ";
    while (!(std::cin >> x))
    {
        std::cout << "Bad input. Please enter a number: ";
        std::cin.clear();
        while (std::cin.get() != '\n')
            continue;
    }
    std::cout << "Value = " << x << std::cin::endl;
    return 0;
}
```

- 4. 这里是修改后的代码：
```cpp
#include <iostream>
int main() 
{
    using std::cin;
    using std::cout;
    using std::endl;

    double x;
    cout << "Enter value: ";
    while (! (cin >> x) ) {
        cout << "Bad input. Please enter a number: ";
        cin.clear();
        while (cin.get() != '\n')
            continue;
    }
    cout << "Value = " << x << endl;
    return 0;
}
```

- 5. 你可以在每个文件中分别拥有静态函数定义。或者在每个文件中于匿名命名空间中定义相应的 `average()` 函数。

- 6. 10
4
0
Other: 10, 1
another(): 10, -4

- 7. 1
4, 1, 2
2
2
4, 1, 2
2

# 第 10 章节习题答案

- 1. 类（class）是用户定义类型的定义。类声明指定了如何存储数据，并指定了可以访问和操作这些数据的方法（类成员函数）。

- 2. 类表示了你通过类方法的公共接口对类对象可以执行的操作；这称为抽象。类可以对数据成员使用私有可见性（默认值），这意味着数据只能通过成员函数访问；这称为数据隐藏。实现细节（如数据表示和方法代码）被隐藏了；这称为封装。

- 3. 类定义了一个类型，包括该类型如何被使用。对象是一个变量或其他数据对象（例如由 `new` 产生的），它根据类的定义被创建和使用。类与对象之间的关系与标准类型与该类型变量之间的关系相同。

- 4. 如果你创建一个类，可以使用作用域解析运算符 (::) 在类声明之外定义它的方法。这有助于组织代码。

- 5. 示例：
```cpp
#include <string>
class BankAccount
{
private:
    std::string name;
    double balance;
public:
    BankAccount(std::string n, double b = 0.0) : name(n), balance(b) {}
    void deposit(double amount) { balance += amount; }
    void withdraw(double amount) { balance -= amount; }
    void show() const {
        std::cout << "Account: " << name << ", Balance: " << balance << std::endl;
    }
};

int main() {
    BankAccount account("Alice", 1000.0);
    account.deposit(500.0);
    account.withdraw(200.0);
    account.show();
    return 0;
}
```

- 6. 构造函数用于初始化对象。它们与类名相同，且没有返回值。

- 7. 析构函数用于在对象销毁时清理资源。它们与类名相同，前面带有一个波浪号 (~)。

- 8. 友函数（Friend functions）允许外部函数访问类的私有和保护成员。

- 9. 内联函数（Inline functions）是对编译器的建议，用实际的函数代码替换函数调用以减少开销。

- 10. 模板（Templates）允许你编写适用于任何类型的泛型代码。

- 11. 封装（Encapsulation）是隐藏对象内部细节并仅暴露接口的做法。

- 12. 继承（Inheritance）允许新类（派生类）从另一个类（基类）继承属性和方法。

- 13. 多态（Polymorphism）是不同对象以自己的方式响应同一个函数调的能力。

- 14. 函数重载（Function overloading）允许多个函数具有相同的名称但不同的参数。

- 15. 运算符重载（Operator overloading）允许你为用户定义类型重新定义运算符的行为。

