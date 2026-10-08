
```cpp
    virtual int getTomorrowFahrenheit() const;

    // 获取明天降雨概率。1 表示会下雨，0 表示没有机会。

    virtual double getRainProbability() const;

    // 以这种格式向用户显示结果：

// Result: x.xx chan. Temp.

    virtual void setResult() const;

    // 返回温度的字符串表示

    virtual std::string getType() const;

private:

    int mTempFahrenheit;

    int mDistanceFromMars;

};
```

注意，该类将所有方法标记为虚方法，因为该类假设其方法可能会派生类中被重写。

该类解决了你程序的大部分问题。然而，正如通常一样，它并不完全符合你的需求。首先，温度是华氏度的。你的程序还需要以摄度运行。此外，`setResult()` 方法可能无法以你的方式显示结果。

# 在派生类中添加功能

当你在第 5 章学习继承时，添加功能是所描述的第一种技术。基本上，你的程序需要一个类似于 `WeatherPrediction` 的类，但带有一些额外的功能。首先，定义一个继承自 `WeatherPrediction` 的新类 `MyWeatherPrediction`。

```cpp
#include "WeatherPrediction.h"

class MyWeatherPrediction : public WeatherPrediction
{
};
```

# 为了复用而继承 | 227

之前的类定义可以正常编译。`MyWeatherPrediction` 已经可以替代 `WeatherPrediction`。它将提供相同的功能，但又有所不同。对于第一次修改，你可能想向类中添加对摄氏（Celsius）单位的支持。这有点进退为难，因为你不知道该类在内部具体做什么。如果所有内部计算都是使用华氏进行的，你该如何添加摄氏的支持呢？一种方法是将派生类作为中间人，在用户（可以使用任何一种单位）和基类（只理解华氏）之间进行接口交互。

支持摄氏的第一步是添加新方法，允许客户端设置当前的摄氏温度，并获取以摄氏或华氏为单位的明天预测。你还需要私有的辅助方法来在摄氏和华氏之间进行转换。这些方法可以是静态的，因为它们适用于该类的所有实例。

```cpp
#include "WeatherPrediction.h"

class MyWeatherPrediction : public WeatherPrediction
{
public:
    virtual void setCurrentTempCelsius(int inTemp);
    virtual int getTomorrowTempCelsius() const;
private:
    static int convertCelsiusToFahrenheit(int inCelsius);
    static int convertFahrenheitToCelsius(int inFahrenheit);
};
```

新方法遵循与父类相同的命名约定。请记住，从其他代码的角度来看，`MyWeatherPrediction` 对象将拥有 `MyWeatherPrediction` 和 `WeatherPrediction` 中定义的所有功能。采用父类的命名约定可以防止接口不一致。

摄氏/华氏转换方法的实现留给读者练习——而且还是一个很有趣练习！另外两个方法更有趣。要设置摄氏温度，你需要先转换温度，然后以类所理解的单位将其呈现给类。

```cpp
void MyWeatherPrediction::setCurrentTempCelsius(int inTemp)
{
    int fahrenheitTemp = convertCelsiusToFahrenheit(inTemp);
    setCurrentTempFahrenheit(fahrenheitTemp);
}
```

如你所见，温度经过了转换，方法调用了基类现有的功能。同样，`getTomorrowTempCelsius()` 的实现使用了父类的现有功能获取华氏温度，但在返回之前对其进行了转换。

```cpp
int MyWeatherPrediction::getTomorrowTempCelsius() const
{
    int fahrenheitTemp = getTomorrowTempFahrenheit();
    return convertFahrenheitToCelsius(fahrenheitTemp);
}
```

这两个新方法有效地复用了父类，因为它们以某种方式“封装”了现有功能，为使用这些功能提供了新的接口。

你也可以添加与父类现有功能完全无关的新功能。例如，你可以添加一个从互联网检索备选预报的方法，或者一个根据预测天气建议活动的方法。

## 在派生类中替换功能

继承的另一个主要技术是替换现有功能。`WeatherPrediction` 类中的 `showResult()` 方法急需一次改新。`MyWeatherPrediction` 可以重写此方法，用它自己的实现来替换行为。

`MyWeatherPrediction` 的新定义如下：

```cpp
#include "WeatherPrediction.h"

class MyWeatherPrediction : public WeatherPrediction
{
    public:
        virtual void setTomorrowCelsius(int inTemp);
        virtual int getTomorrowCelsius() const;
        virtual void showResult() const override;
    private:
        static int convertCelsiusToFahrenheit(int Celsius);
        static int convertFahrenheitToCelsius(int inFahrenheit);
};
```

这是一个可能的、友好的实现：

```cpp
void MyWeatherPrediction::showResult() const
{
    cout << "Tomorrow's temperature will be " <<
         << getTomorrowCelsius() << " degrees Celsius ( <<
         << getTomorrowFahrenheit() << " degrees Fahrenheit)" << endl;
    cout << "Chance of rain is " << (getChanceOfRain() * 100) << " percent" << endl;
    if (getChanceOfRain() > 0.5) {
        cout << "Bring an umbrella!" << endl;
    }
}
```

对于该类的客户端来说，就好像旧版本的 `showResult()` 从未存在过一样。只要对象是 `MyWeatherPrediction` 对象，就会调用新版本。

由于这些更改，`MyWeatherPrediction` 变成了一个具有更特定目的的定制新功能的新类。然而，事实并非如此。

## 父类构造函数

当你编写派生类时，必须意识到父类和子类之间的相互作用。C++ 定义了以下顺序：

- 如果类有一个基类，则首先调用基类构造函数。
- 初始化类的任何数据成员。
- 执行类体。

以下代码显示了这种顺序。结果将输出 123：

```cpp
class Something {
public:
    Something() { cout << "2"; }
};

class Parent {
public:
    Parent() { cout << "1"; }
};

class Child : public Parent {
public:
    Child() { cout << "3"; }
private:
    Something mDataMember;
};

int main() {
    Child myChild;
    return 0;
}
```

当 `myChild` 对象被创建时，首先调用 `Parent` 构造函数输出 1。接着初始化 `mDataMember`，调用 `Something` 构造函数。最后调用 `Child` 构造函数，输出 3。

注意父类构造函数是自动调用的。如果没有默认构造函数，C++ 将自动调用父类的默认构造函数，除非你进行构造链。

以下代码显示了一个缺少默认构造函数的 `Super` 版本。相关的 `Sub` 版本必须显式告诉编译器如何调用 `Super` 构造函数：

```cpp
class Super
{
  public:
    Super(int i);
};

class Sub : public Super
{
  public:
    Sub();
}

Sub::Sub() : Super(7)
{
  // Sub 的其他初始化
}
```

在前面的代码中，`Sub` 构造函数将一个固定值 (7) 传递给 `Super` 构造函数。如果其构造函数需要参数，`Sub` 也可以传递一个值：

```cpp
Sub::Sub(int i) : Super(i) {
```

从派生类将构造参数传递给基类完全没有问题。然而，传递数据成员无效。代码可以编译，但记住数据成员在基类构造之前不会初始化。如果你将数据成员作为参数传递给父构造函数，它将是未初始化的。

虚方法在构造函数中的行为不同。如果你的派生类覆盖了基类的虚方法，在基类构造函数中调用该方法将调用基类的虚方法实现，而不是派生类中的覆盖版本。

## 父类析构函数

由于析构函数不能接受参数，语言总是自动调用父类的析构函数。析构顺序方便地是构造顺序的反序：

- 调用类的析构函数体。
- 类的任何数据成员按照构造顺序的反序被析毁。
- 父类（如果有）被析毁。

再次，这些规则是递归适用的。链中最底层的成员总是先被析构。以下代码为之前的示例添加了析构函数。这些析构函数都被声明为 `virtual`（虚函数），这非常重要，将在本示例之后进行讨论。如果执行，这段代码将输出“123221”。

```cpp
class Something {
  public:
    Something() { cout << "2"; }
    virtual ~Something() { cout << "2"; }
}

class Parent {
  public:
    Parent() { cout << "1"; }
    virtual ~Parent() { cout << "1"; }
}

class Child : public Parent {
  public:
    Child() { cout << "3"; }
    virtual ~Child() { cout << "3"; }
  private:
    Something MDataMember;
}

int main() {
  Child myChild;
  return 0;
}
```

注意这些析构函数都是虚函数。根据惯例，所有的析构函数都应该声明为虚函数。如果之前的析构函数没有声明为虚函数，代码仍然可以正常工作。然而，如果对一个指向派生类的基类指针调用 `delete`，析构过程将从错误的地方开始。例如，下面的代码与之前的示例类似，但析构函数不是虚函数。当一个 `Child` 对象赋值给一个 `Parent` 指针并被删除时，就会出现问题。

```cpp
class Something {
  public:
    Something() { cout << "2"; }
    ~Something() { cout << "2"; } // 应该是虚的，但可以工作
}

class Parent {
  public:
    Parent() { cout << "1"; }
    ~Parent() { cout << "1"; } // 错误！将此设为虚函数！
}

class Child : public Parent {
public:
    Child() { cout << "3"; }
    virtual ~Child() { cout << "3"; } // 应该是虚的，但可以工作
private:
    Something mDataMember;
};

int main()
{
    Parent* ptr = new Child();
    delete ptr;
    return 0;
}
```

这段代码的输出是令人惊讶的简短“1231”。当 `ptr` 变量被删除时，只有 `Parent` 的析构函数被调用，因为该析构函数没有声明为虚函数。结果是 `Child` 的析构函数没有被调用，其数据成员的析构函数也没有被调用。

从技术上讲，你可以通过将 `Parent`析构函数变为虚来解决上述问题。“虚性”会被任何子类自动。然而然而我建议显式地将所有析构函数声明为虚，这样你就永远不需要担心这个问题。

> WARNING 始终让你的析构函数变为虚函数！编译器生成的默认析构函数不是虚的，因此你应该定义自己的虚析构函数，至少对于你的父类。

> WARNING 就像构造函数一样，虚方法在从析构函数中调用时表现不同。如果你的派生类重写了基类的虚方法，从基类析构函数调用该方法将调用基类的虚方法实现，而不是你在派生类中的重写版本。

## 引用父类名称

当你在派生类中重写方法时，对于其他代码来说，你实际上替换了原始方法。然而，该方法仍然存在，你可能想要使用它。例如，一个重写的方法可能保留基类实现的功能，再加上其他内容。看看 `WeatherPrediction` 类中的 `getWeather()` 方法，它返回当前温度的字符串表示。

```cpp
class WeatherPrediction
{
public:
    virtual std::string getWeather() const;
    // 为了简洁已省略
}
```

你可以在 `MyWeatherPrediction` 类中如下所示重写该方法：

```cpp
class MyWeatherPrediction : public WeatherPrediction
{
    public:
        virtual std::string getTemperature() const override;
        // 为了简洁已省略
}
```

假设派生类想要通过先调用基类的 `getTemperature()` 方法然后在字符串后添加“F”来修改字符串。你可能想尝试写成如下形式：

```cpp
string MyWeatherPrediction::getTemperature() const
{
    // 注意：° 是 ISO/IEC 10646 对度符号的表示。
    return getTemperature() + "°"; // 错误
}
```

然而，这是不可行的，因为 C++ 的名称解析机制，它首先在局部作用域中解析，结果将是调用 `MyWeatherPrediction::getTemperature()`。这将导致无限递归，直到耗尽栈空间（某些编译器会检测到并在编译时报告）。要实现这一点，你需要如下所示使用作用域解析运算符：

```cpp
string MyWeatherPrediction::getTemperature() const
{
    // 注意：° 是 ISO/IEC 10646 对度符号的表示。
    return MyWeatherPrediction::getTemperature() + "°";
}
```

> NOTE Microsoft C++ 支持 `__super` 关键字（带下划线）。这允许你编写如下代码：`return __super::getTemperature() + "°";`

调用当前方法的父类版本是 C++ 中的常用模式。如果你有一个派生类链，每个类都可能想要执行由基类定义的操作，但同时也添加自己的功能。作为另一个例子，想象一个类型的层次结构。图 9-4 显示了这种层次结构的图。层次结构中的每个低级类进一步指定了书籍的类型，一个获取书籍描述的方法实际上需要处理层次结构中的所有级别。可以通过以下方式实现：

| Book | | |
| :--- | :--- | :--- |
| Paperback | Technical | |

（注：此处原文似乎包含一些乱码或不完整的文本片段，已根据上下文逻辑推断并翻译了核心含义）

之前的示例应该写成如下：

```cpp
void lessPresumptuous(Super* inSuper)
{
    Sub* mySub = dynamic_cast<Sub*>(inSuper);
    if (mySub != nullptr) {
        // 继续访问 mySub 上的 Sub 方法。
    }
}
```
