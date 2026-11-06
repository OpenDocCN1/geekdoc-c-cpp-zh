

## 解决智能指针实验中的问题

使用新的指针类型时，如果你不断看到错误而不是结果，可能会令人沮丧。当你使用 Code::Blocks 处理新指针类型遇到问题时，请确保安装了正确的版本并配置了正确的设置。如果仍有问题，可以考虑尝试 https://wandbox.org/ 上的技术，由于指针方法较新，它有时能提供更好的结果。在某些情况下，你可能会发现旧习惯妨碍了新流程，因此还必须确认你的代码是按使用新指针类型编写的。

### 清单 8-10：使用 unique_ptr 执行常见任务

```cpp
#include <iostream>
#include <memory>

using namespace std;

int main() {
    unique_ptr<int> ptr1(new int());
    *ptr1 = 100;
    cout << "ptr1 value: " << *ptr1 << endl;

    int myValue = 42;
    unique_ptr<int> ptr2(&myValue);
    cout << "ptr2 value: " << *ptr2 << endl;

    unique_ptr<int> ptr3 = make_unique<int>(99);
    cout << "ptr3 value: " << *ptr3 << endl;
    cout << "ptr3 address: " << ptr3.get() << endl;

    unique_ptr<int> ptr4;
    ptr4 = move(ptr3);
    if (ptr3 == nullptr) {
        cout << "ptr3 is nullptr." << endl;
    }
    cout << "ptr4 value: " << *ptr4 << endl;
    cout << "ptr4 address: " << ptr4.get() << endl;

    return 0;
}
```

该示例展示了创建 unique_ptr 的三种方式：

- 使用 new 运算符。
- 创建一个变量并指向它。
- 使用 `make_unique()` 函数。

在这三种情况下，你都会得到一个包含你所指定值的 `unique_ptr`。注意，必须使用 `<int>` 指定指针类型（用于 int 值）。与其他指针一样，你实际上不能创建一个可以指向任何内容的通用指针。

![](img/128ab511de4e7360e167e3b15cdd5dd0_233_0.png)

`unique_ptr` 为你提供了许多函数。与大多数指针不同，你不能简单地指定指针名称并获取其地址，因为 `unique_ptr` 对访问地址信息实施更严格的控制。你必须改用 `get()` 函数，如代码所示。

如前所述，你不能让一个 `unique_ptr` 等于另一个 `unique_ptr`。但是，你可以使用 `move()` 函数将一个 `unique_ptr` 的地址移动到另一个 `unique_ptr`。`swap()` 函数只是交换两个指针之间的地址。

该示例还展示了 `nullptr` 的用法。如你所见，在代码中使用 `nullptr` 比使用 0 更清晰。以下是该示例的输出：

```
ptr1 value: 100
ptr2 value: 42
ptr3 value: 99
ptr3 address: 0x5daf28
ptr3 is nullptr.
ptr4 value: 99
ptr4 address: 0x5daf28
```

要真正理解 `unique_ptr` 与 `shared_ptr` 的区别，需要并排比较它们的用法。清单 8-11 所示的 SharedPtr 示例演示了在两个指针对象之间进行选择时需要考虑的一些差异。

### 清单 8-11：使用 shared_ptr 进行复制

```cpp
#include <iostream>
#include <memory>

using namespace std;

int main() {
    int myValue = 42;
    shared_ptr<int> ptr1(new int(myValue));
    cout << "ptr1 value: " << *ptr1 << endl;
    cout << "ptr1 use count: " << ptr1.use_count()
         << endl;

    shared_ptr<int> ptr2 = ptr1;
    cout << "ptr2 value: " << *ptr2 << endl;
    cout << "ptr1 address: " << ptr1 << endl;
    cout << "ptr2 address: " << ptr2 << endl;
    cout << "ptr1 use count: " << ptr1.use_count()
         << endl;

    ptr2.reset();
    cout << "ptr1 use count: " << ptr1.use_count()
         << endl;

    ptr1.reset();
    cout << "ptr1 use count: " << ptr1.use_count()
         << endl;

    return 0;
}
```

使用 shared_ptr 时，可以让一个指针等于另一个指针，如本示例所示。代码表明 ptr1 和 ptr2 都指向同一内存位置，并具有相同的值。因此，资源（而不是指针）在两个指针之间共享。

为了更容易确定资源有多少个引用，可以使用 use_count() 函数。每增加一个引用，计数就会递增，这样你就不会不知道资源有多少个引用。

当然，现在你需要某种方法在不再需要引用时移除它们。要完成此任务，可以使用 reset()。代码使用 ptr2.reset() 移除对 myValue 的第二个引用。如下面的输出所示，每次对指针调用 reset() 时，使用计数都会减少。

```
ptr1 value: 42
ptr1 use count: 1
ptr2 value: 42
ptr1 address: 0x6caf08
ptr2 address: 0x6caf08
ptr1 use count: 2
ptr1 use count: 1
ptr1 use count: 0
```

### 通过指针引用数据

![](img/128ab511de4e7360e167e3b15cdd5dd0_235_0.png)

关于复制指针，要记住的重要一点是：复制指针只复制指针地址，而不是底层引用。因此，如果你复制一个指向数组的指针，仍然只有一个数组，但现在你有了对该数组的两个引用。要创建数组的副本，你需要创建第二个大小相同的数组，并将数据从第一个数组逐个索引复制到第二个数组。

![](img/128ab511de4e7360e167e3b15cdd5dd0_235_1.png)

智能指针类的 C++17 版本和 C++20 版本之间存在一些显著差异。从编码角度看，最重要的变化之一是 C++20 依赖宇宙飞船运算符（详情参见第 1 册第 5 章的“考虑新的宇宙飞船运算符”侧栏）取代 !=、<、<=、> 和 >= 运算符。如果你尝试在 C++20 应用程序中使用这些运算符，就会看到错误消息。有关更新代码时可能导致错误的其他版本差异，请参见 https://en.cppreference.com/w/cpp/memory/unique_ptr 和 https://en.cppreference.com/w/cpp/memory/shared_ptr。

### 使用 std::optional 和 std::nullopt 定义可空值

可选值是一种可能存在也可能不存在的值。例如，调用者在调用你的函数时可以提供 int 值，也可以完全不发送任何内容。在某些情况下，发生错误时，该值可能根本不存在。C++ 开发者曾尝试针对未提供值的问题提出各种解决方案，但都不如使用 optional。如果某个值没有出现在 optional 对象中，使用 nullopt 很容易检查。

你可能会疑惑，为什么 optional 会出现在本章。毕竟，它可能应该出现在第 1 册第 6 章处理函数时。在许多方面，optional 表现得像指针，因为它支持许多与 unique_ptr 和 shared_ptr 相同的特性。例如，你可以访问 reset() 和 swap() 函数，如 https://en.cppreference.com/w/cpp/utility/optional 所述。实际上，在学到本书此处之后再理解 optional 会更容易，这就是它出现在这里的原因。

清单 8-12 所示的 Optional 示例演示了如何创建一个可以接收字符串、但也可能不接收字符串的函数。（请注意，由于 GCC 中的问题，此示例可能无法在 Code::Blocks 中运行。目前，你必须将 `#include <optional>` 改为 `#include <experimental/optional>`，因为该支持是实验性的。还有其他必要的更改，你可以在可下载源代码中的 OptionalExperimental 项目里看到。）

### 清单 8-12：使用 optional 避免出现空值情况

```cpp
#include <iostream>
#include <optional>

using namespace std;

void myFunction(optional<string> name = nullopt) {
    if (name == nullopt) {
        cout << "I wish I knew your name!" << endl;
    } else {
        cout << "Hello " << name.value() << "!" << endl;
    }
}

int main() {
    myFunction();
    myFunction("Sarah");
    return 0;
}
```

在本例中，你会看到 `myFunction()`，它不接受任何内容或接受一个字符串。如果调用者不发送任何内容，则 name 等于 `nullopt`。另一方面，如果调用者发送一个字符串，代码会使用 `name.value()` 获取该字符串并打印到屏幕上。请注意，你不能直接访问该字符串，而必须调用 `value()`。以下是该示例的输出：

```
I wish I knew your name!
Hello Sarah!
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_236_0.png)

**警告**

你可能会忍不住认为 `nullopt` 在某种程度上等于 `nullptr`。然而，事实并非如此。如果你尝试将清单 8-12 中的 `nullopt` 检查替换为 `(ptr == nullptr)`，编译器会报错，指出你使用了错误的数据类型。

