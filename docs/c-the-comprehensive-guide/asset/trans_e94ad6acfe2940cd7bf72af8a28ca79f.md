
因此，你只应在有限程度上将此类初始化工作转移到翻译期。

### 13.10.9 “if consteval”

从 C++23 起，还有 *if consteval*。此特性的工作方式与普通 if 略有不同，因为它括号中不包含条件。相反，仅当调用上下文为 constexpr（通常意味着可在编译期求值）时，才会执行 *if consteval* 后面的块。

```cpp
// https://godbolt.org/z/7KWqTpoK
#include <iostream> // cout
constexpr int get_value() {
    if consteval {
        return 42;
    } else {
        return 668;
    }
}
int main() {
    auto a = get_value();
    std::cout << a << '\n';       // Output: 668
    constexpr auto b = get_value();
    std::cout << b << '\n';       // Output: 42
}
```

清单 13.19 编译器判断在给定上下文中该调用是否可在编译期求值。

尽管 a 不在 constexpr 上下文中求值，但 *if consteval* 会检测到调用方不是常量，并在编译时于此处插入 else 分支。然而对于 b，会使用 if 分支，因为 b 是 constexpr，可在编译期求值。

这只是以下写法的另一种形式：

```cpp
constexpr int get_value() {
    if(std::is_constant_evaluated()) {
        return 42;
    } else {
        return 668;
    }
}
```

由于这种写法常与 if constexpr 混淆，因此引入了新语法。

### 13.10.10 用“mutable”解除“const”限制

嘘！告诉你一个秘密，你绝不能告诉任何人。而且不要用它，好吗？你可以让类中的字段成为 mutable，即使你当前处于 const 方法中。

这样做，你就绕过了编译器为你提供的保证。但有时你必须破例。例如，如果你想为了分析目的统计某个方法的调用次数，而该方法实际上是 const 的。

```cpp
// https://godbolt.org/z/sPorknEbd
#include <iostream>
class Data {
    int value_;
    mutable size_t getCount_{0};
public:
    explicit Data(int v) : value_{v} { }
    ~Data() {
        std::cout << "get was used " << getCount_ << " times\n";
    }
    int get() const {
        ++getCount_;
        return value_;
    }
};
int main() {
    Data d{42};
    for (int i=0; i<10; ++i) { d.get(); }
} // Output: get was used 10 times
```

**清单 13.20** “mutable”使 const 方法中的数据字段可变。

如果省略 `mutable`，`get()` 中的 `++getCount_` 表达式将报错。在标记为 `const` 的方法中，不能修改实例数据字段。使用 `mutable`，你可以为单个字段破例。

你应当把 mutable 视为例外：仅将其用于分析。如果你因其他原因需要它，请重新考虑你的设计。

你也可以给 lambda 附加 mutable。我在第 23 章第 23.3.6 节的“可变 Lambda”部分对此作了更详细的描述。

### 13.10.11 const 正确性

从长远来看，一个相关且非常有帮助的方面是习惯于正确使用 const。如果你来自 C（或 Java），这很可能意味着要更多使用它。一旦进入 C++ 世界，只要在正确的位置使用 `const`，编译器就已经能发现代码中的许多*逻辑*错误——即某些本不打算被修改的内容被修改了。

第二个方面是文档说明。`const` 会告诉后续程序员（往往就是你自己）这个值的用途。该变量是用于计算，还是仅用于临时存储？它是输入参数还是输出参数？

### 用于常量的迭代器

此外，还有其他地方可以表明值的不可变性。我将在第 20 章更详细地讨论迭代器，但由于它们具有某种常量性，我应该在这里解释一下。

`Container::const_iterator` 是指向标准库容器内部的引用，它不会修改其中的元素。应将其视为类似于 `int const*`：值不能改变，但引用可以改变。因此，它不同于 `const Container::iterator`，后者相当于 `int *const`。迭代器本身保持固定。

```cpp
// https://godbolt.org/z/GE5v6Ea8x
#include <map>
#include <string>
using std::map; using std::string;
struct MyClass {
  bool isFound(const map<int,string>& dict,   // immutable input parameter.
              const int key,                  // likewise
              string &result                  // output parameter: not const
              ) const                      // instance of MyClass const
  {
    const map<int,string>::const_iterator where  // reference and value fixed
      = dict.find(key);
    if(where == end(dict)) {
      return false;
    } else {
      result = where->second;
      return true;
    }
  }
};
```

**清单 13.21** “const”与容器。

find 方法返回一个迭代器。然而，它可以隐式转换为 `const_iterator`。反过来则无法隐式转换。

### 13.10.12 总结

如果你从一开始就为程序配备尽可能多——或必要数量——的 const，那么编译器可以在开发过程中检测出许多拼写错误、逻辑错误，有时甚至设计错误。[^1]

类和函数的接口通过 const 得到初步描述，但并没有显式文档。在程序代码中，你未来的读者会感谢你，因为 `const` 帮助他们理解哪些内容本应被修改、哪些不应被修改。

从一开始就让项目*符合 const 正确性*，比之后为了调试而不得不这样做要省力得多。

正确使用 `const` 是一种强大且不可低估的工具。最好从“许多”const 开始，并在某些时候考虑是否可以省略它们，而不是考虑是否应该添加更多。

正确使用 const 是类型安全编程的一部分。C++ 拥有强大的类型系统来防止错误。利用 C++ 的能力在编译期操作类型并对其进行计算。

## 13.11 用“volatile”表示易变

const 和 volatile 关键字经常被一起提及。原因有两个：第一，它们在标准中构成常见的*cv 限定符*组；第二，volatile 在某种程度上与 const 相反。使用 volatile，你标记的是那些特别容易改变的东西。这里指的是对编译器的控制：使用 volatile，你标记那些从处理器和编译器的角度看，无需它们干预就能通过某些其他外部机制随时改变的变量和字段。

> **C++20：更少的“volatile”**
>
> 在 C++20 中，volatile 被大幅删减。正如 J. F. Bastien 在一次演讲中所说，“可疑且有缺陷的部分”被移除，而“有用的部分保留了下来”。[^2]
>
> 历史上，volatile 可以出现在 const 能出现的任何地方。这毫无意义，并且同样会令程序员和编译器构建者困惑。仅仅因为参数可以是 const，也允许其为 volatile，这相当无意义，或者至少令人困惑：
>
> ```
> int func(volatile int x);  // volatile is pointless here
> ```
>
> 自 C++20 起，volatile 已与 const 解耦，并被赋予更清晰的语义。总的来说，volatile 变量仍用于与外部世界交互，但棘手的情况已被移除。

例如，一个 volatile 变量可以是一个反映所连接设备状态的变量。本质上，并且极其简化地说，它可能如下面的清单所示。

```cpp
#include <iostream>
#include <chrono> // milliseconds
#include <thread> // this_thread::sleep

struct Pos {
    volatile int x;
    volatile int y;
};
Pos pos{};

// defined somewhere else:
int installMouseDriver(Pos *p);

constexpr auto DELAY = std::chrono::milliseconds(100);
constexpr auto LOOPS = 30; // 30*100ms = 3s
int main() {
    installMouseDriver(&pos); // MouseDriver updates x and y
    for(int i=0; i<LOOPS; ++i) {
        std::cout << "mouse at (" << pos.x << ", " << pos.y << ")\n";
        std::this_thread::sleep_for(DELAY);
    }
}
```

**清单 13.22** x 和 y 可以以某种方式从外部改变。

Pos 的 x 和 y 字段已用 volatile 限定。这告诉编译器，这些字段中的值可能随时改变。例如，编译器既不应应用优化，也不应将这些变量复制到寄存器中进行计算。所有计算都必须直接在这些易变变量的内存中进行。

正如我在这个例子中所暗示的，volatile 在底层编程中特别常见。例如，如果你想通过*通用输入/输出*（GPIO）接口读取树莓派上的温度传感器，一种方法是通过 volatile 变量访问 GPIO 引脚。[^3]

[^1]: “第 43 条：const 正确性”，Herb Sutter，*Exceptional C++*，Addison-Wesley 2000

[^2]: “弃用 volatile”，J. F. Bastien，*CppCon 2019*，https://www.youtube.com/watch?v=KJW_DLaVXIV

[^3]: https://www.raspberrypi.org/forums/viewtopic.php?t=130798&p=875156, [2024-02-25]

