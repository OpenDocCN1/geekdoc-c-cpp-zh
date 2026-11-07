

实际上并没有违背面向对象编程的精神。相反，它们为公共接口提供了更大的灵活性。

## 友元类

什么时候会希望让一个类成为另一个类的友元呢？来看一个例子。假设你必须编写一个简单的模拟程序，模拟电视和遥控器。你决定定义一个表示电视的 `Tv` 类和一个表示遥控器的 `Remote` 类。显然，这两个类之间应该存在某种关系，但究竟是哪种呢？遥控器不是电视，电视也不是遥控器，因此公有继承的“is-a”关系并不适用。它们之间也不是彼此的组成部分，因此包含关系或私有/保护继承的“has-a”关系也不适用。实际情况是，遥控器可以修改电视的状态，这提示我们可以将 `Remote` 类设为 `Tv` 类的友元。

下面来定义 `Tv` 类。你可以用一组状态成员（即描述电视各个方面的变量）来表示一台电视。以下是可能的一些状态：

- 开/关
- 频道设置
- 音量设置
- 有线或天线调谐模式
- 电视调谐器或 A/V 输入

调谐模式反映了这样一个事实：在美国，14 频道及以上的频道间隔，有线接收与 UHF 广播接收是不同的。输入选择在电视（可以是有线电视或广播电视）和 DVD 之间进行选择。有些电视可能提供更多选择，例如多个 DVD/蓝光输入，但就本例而言，这个列表已经足够了。

此外，电视还有一些不属于状态变量的参数。例如，不同电视能接收的频道数量可能不同，你可以添加一个成员来记录该值。

接下来，你必须为类提供用于更改设置的方法。如今许多电视都把控制按钮隐藏在面板后面，但大多数电视即使没有遥控器，也仍然可以更换频道等。不过，通常只能一次向上或向下切换一个频道，而不能随机选择频道。同样，通常有一个增大音量的按钮和一个减小音量的按钮。

遥控器应复刻电视内置的控制功能。它的许多方法可以通过使用 `Tv` 的方法来实现。此外，遥控器通常提供随机频道选择功能。也就是说，你可以直接从频道 2 跳到频道 20，而无需经过所有中间频道。许多遥控器还可以工作在两种或多种模式下，例如作为电视控制器和 DVD 控制器。

这些考虑因素提示了如程序清单 15.1 所示的定义。该定义中包含几个用枚举定义的常量。下面的语句使 `Remote` 成为友元类：

```cpp
friend class Remote;
```

友元声明可以出现在公有、私有或保护部分；位置没有区别。因为 `Remote` 类提到了 `Tv` 类，所以编译器在处理 `Remote` 类之前必须知道 `Tv` 类。最简单的方法是先定义 `Tv` 类。另一种方法是使用前置声明；我们很快会讨论这个选项。

### 程序清单 15.1 tv.h

```cpp
// tv.h -- Tv and Remote classes
#ifndef TV_H_
#define TV_H_

class Tv
{
public:
    friend class Remote;   // Remote can access Tv private parts
    enum {Off, On};
    enum {MinVal,MaxVal = 20};
    enum {Antenna, Cable};
    enum {TV, DVD};

    Tv(int s = Off, int mc = 125) : state(s), volume(5),
        maxchannel(mc), channel(2), mode(Cable), input(TV) {}
    void onoff() {state = (state == On)? Off : On;}
    bool ison() const {return state == On;}
    bool volup();
    bool voldown();
    void chanup();
    void chandown();
    void set_mode() {mode = (mode == Antenna)? Cable : Antenna;}
    void set_input() {input = (input == TV)? DVD : TV;}
    void settings() const; // display all settings
private:
    int state;             // on or off
    int volume;            // assumed to be digitized
    int maxchannel;        // maximum number of channels
    int channel;           // current channel setting
    int mode;              // broadcast or cable
    int input;             // TV or DVD
};

class Remote
{
private:
    int mode;             // controls TV or DVD
public:
    Remote(int m = Tv::TV) : mode(m) {}
    bool volup(Tv & t) { return t.volup(); }
    bool voldown(Tv & t) { return t.voldown(); }
    void onoff(Tv & t) { t.onoff(); }
    void chanup(Tv & t) { t.chanup(); }
    void chandown(Tv & t) { t.chandown(); }
    void set_chan(Tv & t, int c) { t.channel = c; }
    void set_mode(Tv & t) { t.set_mode(); }
    void set_input(Tv & t) { t.set_input(); }
};
#endif
```

程序清单 15.1 中的大多数类方法都是内联定义的。注意，除了构造函数之外，每个 `Remote` 方法都将一个 `Tv` 对象的引用作为参数。这反映了遥控器必须指向特定的电视。程序清单 15.2 显示了其余的定义。音量设置函数将 `volume` 成员改变一个单位，除非声音已经达到最小或最大设置。频道选择函数使用环绕方式，最低频道设置视为 1，紧跟在最高频道设置 `maxchannel` 之后。

许多方法使用条件运算符在两种设置之间切换状态：

```cpp
void onoff() {state = (state == On) ? Off : On;}
```

如果两个状态值为真和假，或者等价地，0 和 1，则可以更紧凑地使用按位异或和赋值组合运算符（^=）来完成，如附录 E“其他运算符”所讨论的：

```cpp
void onoff() { state ^= 1; }
```

实际上，你可以将多达 8 个二值状态设置存储在一个 `unsigned char` 变量中，并单独切换它们，但这是另一个话题了，一个由附录 E 中讨论的位运算符实现的话题。

### 程序清单 15.2 tv.cpp

```cpp
// tv.cpp -- methods for the Tv class (Remote methods are inline)
#include <iostream>
#include "tv.h"

bool Tv::volup()
{
    if (volume < MaxVal)
    {
        volume++;
        return true;
    }
    else
        return false;
}
bool Tv::voldown()
{
    if (volume > MinVal)
    {
        volume--;
        return true;
    }
    else
        return false;
}
void Tv::chanup()
{
    if (channel < maxchannel)
        channel++;
    else
        channel = 1;
}
void Tv::chandown()
{
    if (channel > 1)
        channel--;
    else
        channel = maxchannel;
}
void Tv::settings() const
{
    using std::cout;
    using std::endl;
    cout << "TV is " << (state == Off? "Off" : "On") << endl;
    if (state == On)
    {
        cout << "Volume setting = " << volume << endl;
        cout << "Channel setting = " << channel << endl;
        cout << "Mode = "
            << (mode == Antenna? "antenna" : "cable") << endl;
        cout << "Input = "
             << (input == TV? "TV" : "DVD") << endl;
    }
}
```

程序清单 15.3 是一个简短的程序，测试到目前为止程序的一些特性。同一个遥控器被用来控制两台不同的电视。

### 程序清单 15.3 use_tv.cpp

```cpp
//use_tv.cpp -- using the Tv and Remote classes
#include <iostream>
#include "tv.h"

int main()
{
    using std::cout;
    Tv s42;
    cout << "Initial settings for 42\" TV:\n";
    s42.settings();
    s42.onoff();
    s42.chanup();
    cout << "\nAdjusted settings for 42\" TV:\n";
    s42.settings();

    Remote grey;

    grey.set_chan(s42, 10);
    grey.volup(s42);
    grey.volup(s42);
    cout << "\n42\" settings after using remote:\n";
    s42.settings();

    Tv s58(Tv::On);
    s58.set_mode();
    grey.set_chan(s58, 28);
    cout << "\n58\" settings:\n";
    s58.settings();
    return 0;
}
```

以下是程序清单 15.1、15.2 和 15.3 的程序输出：

```text
Initial settings for 42" TV:
TV is Off
```

