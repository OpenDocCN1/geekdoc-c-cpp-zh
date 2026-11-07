
在这种情况下，你会陷入麻烦，因为默认生成的移动操作可能会创建无效的 Tasks 状态。考虑以下示例：

`basics/tasksbug.cpp`

```cpp
#include "tasksbug.hpp"
#include <iostream>
#include <chrono>
#include <exception>

int main()
{
    try {
        Tasks ts;
        ts.start([]{
            std::this_thread::sleep_for(std::chrono::seconds{2});
            std::cout << "\nt1 done" << std::endl;
        });
        ts.start([]{
            std::cout << "\nt2 done" << std::endl;
        });

        // OOPS: move tasks:
        Tasks other{std::move(ts)};
    }
    catch (const std::exception& e) {
        std::cerr << "EXCEPTION: " << e.what() << std::endl;
    }
}
```

一开始，我们通过将两个任务传递给 Tasks 对象 ts 来启动它们。因此，在 ts 中，threads 数组有两个条目，且 numThreads 为 2。不幸的是，容器的移动操作会移动元素，因此在 std::move() 之后，ts 不再包含任何表示正在运行线程的线程对象。因此，numThreads 只是被复制了，这意味着我们创建了一个不一致/无效的状态。析构函数最终会遍历前两个元素并调用 join()，这会抛出异常（这在析构函数中是致命错误）。

一般问题在于，两个成员共同定义了一个有效状态，而默认生成的移动语义会造成不一致，以至于连析构函数都会失败。你无法总是避免这个问题，因为当对象被销毁时，你可能总是必须显式地对对象所含元素的某个子集做一些处理。在所有这些情况下，默认生成的移动操作可能无法正常工作，你应当禁用或修复它们。

一种修复方式可能是：

-   修复析构函数以处理被移动后的状态（例如，在这种情况下，我们可以只在 thread 对象 `joinable()` 时才调用 `join()`）
-   自己实现移动操作

考虑一个用于纸牌游戏卡牌的类。⁴ 假设每个对象都是一张有效卡牌，例如红桃八或方块 K。还假设无论出于何种原因，值是一个字符串，并且该类的不变式是每个对象都具有表示有效卡牌的状态。这意味着我们可能没有默认构造函数，并且初始化构造函数会断言该值是有效的。例如：

```cpp
class Card {
private:
    std::string value;              // rank + "-of-" + suit
public:
    Card(const std::string& v)
      : value{v} {
        assertValidCard(value);     // ensure the value is always valid
    }

    std::string getValue() const {
        return value;
    }
};
```

在这个类中，生成的特殊移动成员函数会创建一个无效状态，破坏“值始终是点数后跟 "-of-" 再后跟花色”的类不变式（例如 "queen-of-hearts"）。

只要我们不使用 std::move() 或其他移动操作，这就不是问题（该类型的析构函数对被移动后的字符串工作正常），但当我们调用 std::move() 时，就可能陷入麻烦。赋一个新值工作正常：

```cpp
std::vector<Card> deck;                  // initialize deck
...
Card c{std::move(deck[0])};              // deck[0] has its valid state
deck[0] = Card{"ace-of-hearts"};          // deck[0] is valid again
```

然而，打印被移动后卡牌的值可能会失败：

```cpp
std::vector<Card> deck;                  // initialize deck
...
Card c{std::move(deck[0])};              // deck[0] has invalid state
print(deck[0]);                          // passing an object with broken invariant
```

如果 print 函数假定不变式没有被破坏，我们可能会得到核心转储：

```cpp
void print(const Card& c) {
    std::string val{c.getValue()};
    auto pos = val.find("-of-");              // find position of substring (no check)
    std::cout << val.substr(0, pos) << ' '
              << val.substr(pos+4) << '\n';  // OOPS: possible core dump
}
```

⁴ 感谢 Tony Van Eerd 提供此示例。

这段代码可能在运行时失败，因为对于被移动后的卡牌，不再保证值中包含 "-of-"。在这种情况下，`find()` 会用 `std::string::npos` 初始化 `pos`，当 `pos+4` 被用作 `substr()` 的第一个参数时，会抛出 `std::out_of_range` 类型的异常。

完整示例参见 *basics/card.hpp* 和 *basics/card.cpp*。

修复这个类的选项如下：

-   禁用移动语义：

    ```cpp
    class Card {
        ...
        Card(const Card&) = default;              // disable move semantics
        Card& operator=(const Card&) = default;   // disable move semantics
    };
    ```

    然而，这会使移动操作（例如由 `std::sort()` 调用）开销更大。

-   完全禁用复制和移动：

    ```cpp
    class Card {
        ...
        Card(const Card&) = delete;              // disable copy/move semantics
        Card& operator=(const Card&) = delete;   // disable copy/move semantics
    };
    ```

    然而，此后你就不能再洗牌或排序卡牌了。

-   修复有问题的特殊移动成员函数。

    然而，什么才是有效的修复（总是赋一个诸如 "ace-of-clubs" 的“默认值”可以吗）？并且你如何确保带有默认值的对象在不分配内存的情况下表现良好？

-   在内部允许新状态，但禁止调用 `getValue()` 或其他成员函数。

    你可以记录这一点（“对于被移动后的对象，只允许为其赋新值。所有其他成员函数都有前提条件：对象不处于被移动后的状态。”），甚至可以在成员函数内部检查这一点，并触发断言或抛出异常。

-   通过引入 `Card` 可能没有值的新状态来扩展不变式。

    这意味着你必须实现移动特殊成员函数，因为必须确保对于被移动后的对象，成员 value 处于此状态。

    通常，被移动后的状态等同于默认构造状态。因此，这也是提供默认构造函数的机会。理想情况下，你还可以提供一个成员函数来检查此状态。

    进行此更改后，该类的用户必须考虑到字符串的值可能为空，并相应地更新其代码。例如：

    ```cpp
    void print(const Card& c) {
        std::string val{c.getValue()};
        auto pos = val.find("-of-");                 // find position of substring
        if (pos != std::string::npos) {              // check whether it exists
            std::cout << val.substr(0, pos) << ' '
                      << val.substr(pos+4) << '\n';
        }
        else {
            std::cout << "no value\n";
        }
    }
    ```

或者，`getValue()` 可以返回 `std::optional<std::string>`（自 C++17 起可用）。似乎没有明显完美的解决方案。你必须思考这些方案对程序更大范围的不变式分别意味着什么（例如，只有一个梅花 A，或者所有卡牌都是有效卡牌等），并决定使用哪一种。

注意，这个类在 C++11 之前工作正常，那时不支持移动语义（这可能意味着第一个选项是最好的）。因此，C++11 可能为类引入一些在该类实现时不可能存在的状态。这是罕见情况，但它确实意味着移动语义的引入可能会破坏现有代码。

参见 class final 或另一个类的示例，其中我们在内部标记被移动后的状态以单独处理它，并在“移除”算法使元素处于被移动后状态之后使该状态可见。

### 6.3.2 由于移动一致的值成员而破坏不变式

移动操作破坏不变式的第二个原因与这样的对象有关：其中两个成员必须保持一致，但可能被移动特殊成员函数破坏。正如线程数组示例中所见，这甚至可能造成破坏析构函数的不一致。然而，更常见的情况是析构函数工作正常，但被移动后的状态破坏了不变式。

考虑一个类，其中我们有一个值的两种不同表示：一个整数表示和一个字符串表示：

*basics/integrating.hpp*

```cpp
#include <iostream>
#include <string>

class IntString
{
  private:
    int val;          // value
    std::string sval; // cached string representation of the value
  public:
    IntString(int i = 0)
      : val{i}, sval{std::to_string(i)} {
    }
    void setValue(int i) {
      val = i;
      sval = std::to_string(i);
    }
    ...
    void dump() const {
      std::cout << "[ " << val << " / " << sval << "]\n";
```
