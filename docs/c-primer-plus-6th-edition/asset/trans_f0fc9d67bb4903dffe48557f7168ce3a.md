

# 第10章 对象与类

```cpp
class Ik
{
private:
    int fuss; // fuss 有类作用域
public:
    Ik(int f = 9) {fuss = f; } // fuss 在作用域内
    void ViewIk() const; // ViewIk 有类作用域
};
```

```cpp
void Ik::ViewIk() const //Ik: 将 ViewIk 放入 Ik 中
{
    cout << fuss << endl; // fuss 在类方法内作用域内
}
```

```cpp
int main()
{
    Ik *pik = new Ik;
    Ik ee = Ik(8); // 因为类名，构造函数在作用域内
    ee.ViewIk(); // 类对象将 ViewIk 引入作用域
    pik->ViewIk(); // 指向 Ik 的指针将 ViewIk 引入作用域
}
```

# 类作用域常量

有时，具有类作用域的符号常量会很不错。例如，一个类声明可能会使用字面量 30 来指定数组大小。由于该常量对于所有对象都是相同的，如果能创建一个由所有对象共享的单一常量就太好了。你可能认为以下方案是一个解决方案：

```cpp
class Bakery
{
private:
    const int Months = 12; // 声明常量？失败
    double costs[Months];
}
```

但这行不通，因为声明一个类描述的是对象的结构，但并没有创建对象。因此，在创建对象之前，没有地方来存储值。（实际上，C++11 提供了成员初始化，但其方式无法让上述数组声明生效；第12章会回到这个主题。）不过，有几种方法可以实现基本上相同的预期效果。

首先，你可以在类内部声明一个枚举。枚举声明具有类作用域，因此你可以使用枚举为整数常量提供类作用域的符号名称。也就是说，你可以这样开始 Bakery 的声明：

# 类作用域

```cpp
class Bakery {
private:
    enum {Months = 12};
    double costs[Months];
    ...
};
```

注意，以这种方式声明枚举并没有创建数据成员。也就是说，每个单独的对象内部并不携带一个枚举。相反，Months 只是一个符号名称，编译器在类类作用域中遇到它时会替换为 30。

由于 Bakery 使用枚举来创建符号常量，并没有意图创建枚举类型的变量，因此你不需要提供枚举标签。顺便提一下，对于许多实现，ios_base 类在其公共部分做了类似的事情，例如 `ios_base::fixed`。这里 fixed 通常是定义在 ios_base 类中的枚举的另一种使用方式。

C++ 还有另一种在类内部定义常量的方法——使用 `static` 关键字：

```cpp
class Bakery
private:
    static const int Months = 12;
    double costs[Months];
    ...
};
```

这创建了一个名为 Months 的单一常量，它与其他静态变量一起存储，而不是在对象中。因此，所有的 Bakery 对象共享一个 Months。第12章将进一步研究静态类成员。在 C++98 中，你可以使用这种技术来声明具有整数和枚举值的静态常量。因此，C++98 不允许你用这种方式存储双精度常量。C++11 移除了这一限制。

# 作用域枚举 (C++11)

传统的枚举有些问题。其中一个是来自两个不同定义的枚举值可能会冲突。假设你正在处理一个涉及鸡蛋和 T 恤的项目。你可能会尝试这样的代码：

```cpp
enum egg {Small, Medium, Large, Jumbo};
enum t_shirt {Small, Medium, Large, XLarge};
```

这是不通的，因为 egg 和 t_shirt 的 Small 都会在同一个作用域内，导致名称冲突。C++11 提供了一种新的枚举形式，通过使其枚举值具有类作用域来避免这个问题。这种形式的声明如下：

```cpp
enum class egg {Small, Medium, Large, Jumbo};
enum class t_shirt {Small, Medium, Large, XLarge};
```

# 第10章 对象与类

或者，你可以使用 `struct` 关键字代替 `class`。在任何情况下，你都需要使用枚举名来限定枚举值：

```cpp
egg choice = Large; // egg 枚举中的 Large 枚值
t_shirt Floyd = t_shirt::Large; // t_shirt 枚举中的 Large 枚值
```

现在枚举值有了作用域，来自不同枚举定义的枚举值不再有名称冲突，你的鸡蛋和 T恤项目可以继续进行了。
C++11 还加强了作用域枚举的类型安全。普通枚举在某些情况下会自动转换类型，例如赋值给枚举类型的 int 变量或在比较中使用，但作用域枚举不会隐式转换为整数类型：

```cpp
enum egg_old {Small, Medium, Jumbo}; // 非作用域的
enum t_shirt {Small, Medium, Large, XLarge}; // 作用域的
egg_old = Medium; // 作用域
t_shirt rolf = t_shirt; // 非作用域的隐式类型转换
int kind = rol; // 不允许，没有隐式类型转换
if (kind < jumbo) // 允许
std::cout << "Jumbo converted to int before comparison.\n";
if (kind < t_shirt::Medium) // 不允许
std::cout << "Not allowed: not defined for scoped enum.\n";
```

但如果你必须这样做，可以进行显式类型转换：
int Frodo = (int)t_shirt::Small; // 显式类型转换

除非使用显强制转换，否则枚举不会隐式转换为整数类型。这是因为作用域枚举是强类型的。

