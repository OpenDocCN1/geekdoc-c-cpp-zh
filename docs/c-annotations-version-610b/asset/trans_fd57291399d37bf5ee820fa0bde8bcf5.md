

### 13.5 重定义成员函数

派生类可以重定义基类成员。假设一个车辆分类系统还必须涵盖卡车，卡车由两部分组成：前部（牵引车）拉动后部（挂车）。牵引车和挂车各自有质量，mass 函数应返回组合质量。

`Truck` 的定义从一个类定义开始。我们最初的 `Truck` 类派生自 `Auto`，但之后进行了扩展，以多保存一个 `size_t` 字段，表示额外的质量信息。这里我们选择在 `Auto` 类中表示卡车前部的质量，并将挂车质量存储在一个额外字段中：

```cpp
class Truck: public Auto
{
    size_t d_trailer_mass;

public:
    Truck();
    Truck(size_t tractor_wt, size_t speed, char const *name,
          size_t trailer_wt);

    void setMass(size_t tractor_wt, size_t trailer_wt);
    size_t mass() const;
};

Truck::Truck(size_t tractor_wt, size_t speed, char const *name,
             size_t trailer_wt)
:
    Auto(tractor_wt, speed, name)
{
    d_trailer_mass = trailer_wt;
}
```

注意，`Truck` 类现在包含了基类 `Auto` 中已有的两个函数：`setMass` 和 `mass`。

- `setMass` 的重定义没有问题：这个函数被简单地重定义，以执行针对 `Truck` 对象的特定操作。
- 然而，重定义 `setMass` 会*隐藏* `Auto::setMass`。对于 `Truck`，只能使用具有两个 `size_t` 参数的 `setMass` 函数。
- `Vehicle` 的 `setMass` 函数对 `Truck` 仍然可用，但现在必须*显式*调用，因为 `Auto::setMass` 被隐藏了。即使 `Auto::setMass` 只有一个 `size_t` 参数，该函数仍然被隐藏。要实现 `Truck::setMass`，我们可以这样写：

    ```cpp
    void Truck::setMass(size_t tractor_wt, size_t trailer_wt)
    {
        d_trailer_mass = trailer_wt;
        Auto::setMass(tractor_wt);    // note: Auto:: is required
    }
    ```
- 在类外部，通过作用域解析运算符访问 `Auto::setMass`。因此，如果某个 `Truck` 对象需要设置其 `Auto` 部分的质量，它必须使用：

    ```cpp
    truck.Auto::setMass(x);
    ```

```cpp
cout << '\n' << "Truck weighs " <<
             lorry.Vehicle::mass() << '\n' <<
       "Truck + trailer weighs " << lorry.mass() << '\n' <<
       "Speed is " << lorry.speed() << '\n' <<
       "Name is " << lorry.name() << '\n';
}
```

`Truck` 类派生自 `Auto`。然而，有人可能会质疑这种类设计。既然卡车被构想为牵引车和挂车的组合，那么使用组合来定义它可能更好。这将我们的视角从“`Truck` 是一种 `Auto`（并且包含一些奇怪的数据成员）”转变为“`Truck` 由 `Auto`（牵引车）和 `Vehicle`（挂车）组成”。`Truck` 的接口现在非常具体，不需要用户去研究 `Auto` 和 `Vehicle` 的接口，并且为定义“公路列车”（牵引车拖挂多辆挂车）提供了可能。下面是这种另一种类设置的一个示例：

```cpp
class Truck
{
    Auto d_lorry;
    Vehicle d_trailer;        // use vector<Vehicle> for road trains

public:
    Truck();
    Truck(size_t tractor_wt, size_t speed, char const *name,
          size_t trailer_wt);

    void setMass(size_t tractor_wt, size_t trailer_wt);
    void setTractorMass(size_t tractor_wt);
    void setTrailerMass(size_t trailer_wt);
    size_t mass() const;
    size_t tractorMass() const;
    size_t trailerMass() const;
    // consider:
    Auto const &tractor() const;
    Vehicle const &trailer() const;
};
```

### 13.6 iostream::init

考虑从 `std::istream` 或 `std::ostream` 派生的类。这样的类可以如下设计：

```cpp
class XIstream: public std::istream
{
public:
    ...
};
```

假设 `XIstream` 要关联的 `streambuf` 在构造时还不可用，那么 `XIstream` 只提供默认构造函数。但是，该类可以提供成员函数 `void switchStream(std::streambuf *sb)`，以便为 `XIstream` 对象换用一个新的 `streambuf` 接口。如何实现 `switchStream`？

`std::istream` 和 `std::ostream` 类提供了一个受保护成员 `void init(std::streambuf *sb)` 来实现此功能。init 成员期望一个指向 streambuf 的指针，该 streambuf 将与 istream 或 ostream 对象关联。init 成员会先妥善结束任何现有的关联，再切换到其地址被提供给 init 的 streambuf。

假设 `switchStream` 的 `sb` 所指向的 `streambuf` 持续存在，那么 `switchStream` 可以简单地实现如下：

```cpp
void switchStream(streambuf *sb)
{
    init(sb);
}
```

### 13.7 多重继承

到目前为止，一个类总是从单个基类派生而来。除了单一继承，C++ 还支持*多重继承*。在多重继承中，一个类从多个基类派生，因此同时继承多个父类的功能。

使用多重继承时，将新派生类视为两个基类的实例化应当是合理的。否则，组合更合适。通常，线性派生（只使用一个基类）的使用频率远高于多重派生。良好的类设计原则要求一个类应该具有单一且描述清晰的责任，而这一原则常常与多重继承相冲突，因为在多重继承中，我们可以说 `Derived` 类的对象*既是* `Base1` 对象*又是* `Base2` 对象。

但话又说回来，考虑一下多重继承被用到极致的*原型*对象：*瑞士军刀*！这个物体是一把刀，是一把剪刀，是一个开罐器，是一个开瓶器，它是……

“瑞士军刀”是多重继承的一个极端例子。在 C++ 中，确实*有*一些很好的理由，可以不违反下一章将要讨论的“一个类，一个责任”原则。本节讨论使用多重继承构造类的技术细节。

如何在 C++ 中构造一把“瑞士军刀”？首先我们需要（至少）两个基类。例如，假设我们在设计一个工具包，用于构建飞机驾驶舱的仪表板。我们设计各种仪器，如人工地平仪和高度表。飞机上常见的组件之一是*导航通信一体机*（nav-com set）：导航信标接收机（“nav”部分）和无线电通信单元（“com”部分）的组合。要定义 nav-com set，我们首先设计 `NavSet` 类（假设存在 `Intercom`、`VHF_Dial` 和 `Message` 类）：

```cpp
class NavSet
{
    public:
        NavSet(Intercom &intercom, VHF_Dial &dial);

        size_t activeFrequency() const;
        size_t standByFrequency() const;

        void setStandByFrequency(size_t freq);
        size_t toggleActiveStandby();
        void setVolume(size_t level);
        void identEmphasis(bool on_off);
};
```

接下来我们设计 `ComSet` 类：

```cpp
class ComSet
{
    public:
        ComSet(Intercom &intercom);

    size_t frequency() const;
    size_t passiveFrequency() const;

    void setPassiveFrequency(size_t freq);
    size_t toggleFrequencies();

    void setAudioLevel(size_t level);
    void powerOn(bool on_off);
    void testState(bool on_off);
    void transmit(Message &message);
};
```

使用这个类的对象，我们可以接收通过 Intercom 传输的消息，但也可以通过 Message 对象*发送*消息，该 Message 对象是通过其 transmit 成员函数传递给 ComSet 对象的。

现在我们可以构建我们的 NavCom 一体机了：

```cpp
class NavComSet: public ComSet, public NavSet
{
    public:
        NavComSet(Intercom &intercom, VHF_Dial &dial);
};
```

完成。现在我们已经定义了一个 NavComSet，它*既*是 NavSet*又*是 ComSet：通过多重继承，两个基类的功能现在都可以在派生类中使用。

请注意以下几点：

- 关键字 public 出现在两个基类名称（NavSet 和 ComSet）之前。默认情况下，继承使用*私有派生*，并且关键字 public 必须在每个基类说明之前重复。基类不要求使用相同的派生类型。一个基类可以使用公有派生，另一个基类可以使用私有派生。
- 多重派生类 NavComSet 没有引入自身的新功能，而只是将两个现有类组合成一个新的聚合类。因此，C++ 提供了将多个简单类合并成一个更复杂类的可能性。
- 以下是 NavComSet 构造函数的实现：

    ```cpp
    NavComSet::NavComSet(Intercom &intercom, VHF_Dial &dial)
    :
        ComSet(intercom),
        NavSet(intercom, dial)
    {}
    ```

    构造函数不需要额外代码：其目的是激活其基类的构造函数。基类初始化器的调用顺序*不是*由它们在构造函数代码中的调用顺序决定的，而是由基类在类接口中的顺序决定的。

- NavComSet 类定义不需要额外的数据成员或成员函数：在这里（而且通常也是如此）继承的接口为多重派生类的正常运行提供了所有必需的功能和数据。

当然，在定义基类时，我们特意严格使用了不同的成员函数名，从而让自己轻松不少。因此，NavSet 类中有 setVolume 函数，ComSet 类中有 setAudioLevel 函数。这有点取巧，因为我们可以预期这两个单元实际上都有一个组合对象 Amplifier 来处理音量设置。一个经过修订的类可能会提供一个 Amplifier

