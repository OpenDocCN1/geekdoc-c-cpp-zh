

# 可以实例化调试或生产环境的驱动程序。
两者都以签名类作为基类。

```cpp
// https://qdbbolt.org/z/xWr7axonx
#include <iostream>    // cout
#include <memory>       // unique_ptr
using std::cout;
class Driver {                            // 抽象基类
public:
    virtual void init() = 0;
    virtual void done() = 0;
    virtual void send(const std::string &data) = 0;
};
class ProductionDriver : public Driver {
public:
    void init() override {}
    void done() override {}
    void send(const std::string &data) override { cout << data << "\n"; }
};
class DebuggingDriver : public Driver {
size_t countSend_ = 0;
public:
    void init() override {
        countSend_ = 0; cout << "Ok, I'm initialized.\n";
    }
    void done() override {
        cout << "send used:" << countSend_ << " times\n";
    }
    void send(const std::string &data) override {
        cout << "send" << countSend_ << ":" << data << "\n";
        ++countSend_;
    }
};
struct RAIIWrapper {                            // init() 和 done() 的封装
    Driver &driver;
    explicit RAIIWrapper(Driver& driver) : driver(driver) {
        driver.init();
    }
    ~RAIIWrapper() { driver.done(); }
    RAIIWrapper(const RAIIWrapper&) = delete; // 禁止拷贝
};
void doWork(Driver& driver) { // 有人自由使用任何驱动程序
    RAIIWrapper wrapper(driver); // 调用 init() 和 done()
    driver.send("An Unexpected Journey");
    driver.send("The Desolation Of Smaug");
}

int main() {
    // doWork，一次使用生产驱动，一次使用调试驱动
    ProductionDriver production();
    doWork( production );
    DebuggingDriver debugging();
    doWork( debugging );

    // 动态创建的驱动程序的更常见变体
    std::unique_ptr<Driver> driver( new ProductionDriver{} );
    doWork(* driver);
}
```

**Listing 18.11** 带有实现 "=0" 的虚方法是抽象的。

在 `Driver` 类中，我将所有方法都设为虚方法。此外，没有实现，而是 `0`。这种没有实现的方法被称为**纯虚方法或抽象方法**。至少包含一个抽象方法的类也称为*抽象类*。你不能创建抽象类的实例。编译器将对以下内容报错：

```cpp
Driver driver(); // 抽象
```

你也可以创建包含许多虚方法但仅有一或两个抽象方法的大类，但对于这类抽象类的具体应用——正如名称 `Driver` 所示——其特点是你可以在运行时决定使用哪一个。想象一个应该运行在多种图形卡上的程序：你创建一个基驱动程序，其中所有方法都是抽象的。程序的各个部分都使用指向该类的引用（或指针）并调用虚方法。当程序启动时，你将确定加载哪一个还是另一个实现到内存中。这种实现方式取决于系统，在这里解释将超出了本书的范围。然而，这在几乎任何地方都是可行的。无论如何，这种实现灵活性的基础在于基类*仅*拥有抽象方法。如果你对该抽象类有其他用例，那么你可以在基类中提供任意数量的实现。

## 18.4 多重继承

如果你想尝试多重继承，那是可以的。但帮其他阅读你代码的人一个忙：不要在长期项目中引入多重继承——有一个例外，就是你可以使用类来模拟像 Java 中那样存在的接口。不要误会我的意思。多重继承作为一个概念是好的，并且在面向对象教学中有其用武之地。它对于良好地建模甚至是必要的。毕竟，现实世界中并非所有事物都能强行归入树形层次结构。但在 C++ 中，如果不加思考地使用多重继承，将会变得不可维护。相反，必须自愿地限制自己，并采用 C++ 的技术方案，以便以可管理的方式映射必要的世界。

### 完全不要使用多重继承，或者极少量使用

遵循这一准则：不要让一个类从两个基类继承实现。例外一：如果你确实这样做，请仅在类层次结构的最底部进行。这在某些编程模式（如观察者模式）中很有用。例外二：可以尽可能多添加没有实现的类（签名类），如果你习惯的话，可以用来模拟 Java 接口。在这一警告之后，将解释如果你不使用多重继承会错过什么。这些较短的示例显然足够清晰。

```cpp
// https://godbolt.org/z/TM35
#include <iostream>
using std::cout;
class Mammal {
public:
    void giveBirth() { cout << "Birth\n"; }
};
class Flying {
public:
    void fly() { cout << "Flight\n"; }
};
class Base: public Mammal, public Flying {
public:
    void call() { cout << "Ultrasound\n"; }
};
int main() {
    Base bruce;
    bruce.giveBirth(); // 输出: Birth!
    bruce.fly(); // 输出: Flight!
    bruce.call(); // 输出: Ultrasound!
}
```
**Listing 18.12** 多重继承意味着拥有所有基类的属性。对于像 `bruce` 这样的实例，你可以同时调用 `Mammal` 的 `giveBirth()` 和 `Flying` 的 `fly()`。此外，该类还可以添加它自己的任何成员，如 `call()`。图 18.1 提醒了普通的层次结构，其中每个类只有一个祖先。相比之下，图 18.2 中的 `Bat` 类有多个祖先。

![img/290cf5dfcaad536de98cca8ef_803_0.png]
**图 18.1** 经典继承。

![img/290cf5dfcaad536de98cca8ef_803_1.png]
**图 18.2** 多重继承。

## 18.4.1 实践中的多重继承

尽管我认为以下示例应该实现为“拥有一个”（has-a）关系，但它仍然可以作为多重继承的示例。这里的基类是时钟和日历，组合成一个带日历的时钟。在 Listing 18.13 中，你首先看到一个你可以初始化、显示并递进一秒的简单时钟。在 Listing 18.13 中，你可以通过增加代码来使示例更加类型安全，特别是在交换相应的单位时。

```cpp
// https://godbolt.org/z/eofTs
#include <iostream>
#include <iomanip>
#include <format>
using std::cout;
using std::format;
class Clock {
protected:
    int h_, m_, s_;
public:
    Clock(int hours, int minutes, int seconds)
        : h_(hours), m_(minutes), s_(seconds) {}
    void setClock(int hours, int minutes, int seconds) {
        h_ = hours; m_ = minutes; s_ = seconds;
    }
    friend std::ostream& operator<<(std::ostream& os, const Clock& c) {
        return os << format("{:02}:{:02}:{:02}", c.h_, c.m_, c.s_);
    }
    void tick() { // +1秒
    if(s_ >= 59) {InListing 18.13.
```
**Listing 18.13** 时钟和日历的组合成了一个带日历的时钟。

# 使用这个时钟非常简单：

```cpp
int main() {
  Clock clock(23, 59, 59);
  std::cout << clock << '\n'; // 输出: 23:59:59
  clock.tick();
  std::cout << clock << '\n'; // 输出: 00:00:00
}
```

# 日历同样简单：

```cpp
// https://godbolt.org/z/56Ec35Tf
// includes and usings
struct Calendar {
  int y_, m_, d_;
  static const std::vector<int> mlens;
  bool leapyear() const {
    if(y_ % 4 != 0) return false;
    if(y_ % 100 != 0) return true;
    if(y_ % 400 == 0) return false;
    return true;
  }
public:
  Calendar(int year, int month, int day)
    : y_(year), m_(month), d_(day) {}
  void setCalendar(int year, int month, int day) {
    y_ = year; m_ = month; d_ = day;
  }
};
```

