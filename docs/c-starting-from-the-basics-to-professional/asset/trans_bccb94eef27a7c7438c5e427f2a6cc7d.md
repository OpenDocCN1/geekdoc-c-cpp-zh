
## 综合运用

在 truckload 模块及其实现文件就位后，可以使用以下代码试用 Truckload 类：

```cpp
// Ex12_17.cpp
// Using a linked list
import box.random;
import truckload;

int main()
{
    Truckload load1;  // Create an empty list

    // Add 12 random Box objects to the list
    const size_t boxCount {12};
    for (size_t i {}; i < boxCount; ++i)
        load1.addBox(randomSharedBox());

    std::cout << "The first list:\n";
    load1.listBoxes();

    // Copy the truckload
    Truckload copy{load1};
    std::cout << "The copied truckload:\n";
    copy.listBoxes();

    // Find the largest Box in the list
    SharedBox largestBox{load1.getFirstBox()};

    SharedBox nextBox{load1.getNextBox()};
    while (nextBox)
    {
        if (nextBox->compare(*largestBox) > 0)
            largestBox = nextBox;
        nextBox = load1.getNextBox();
    }

    std::cout << "\nThe largest box in the first list is ";
    largestBox->listBox();
    std::cout << std::endl;
    load1.removeBox(largestBox);
    std::cout << "\nAfter deleting the largest box, the list contains:\n";
    load1.listBoxes();

    const size_t nBoxes {20};              // Number of vector elements
    std::vector<SharedBox> boxes;          // Array of Box objects

    for (size_t i {}; i < nBoxes ; ++i)
        boxes.push_back(randomSharedBox());
}
```

## 嵌套类

Package 类被设计为专门在 Truckload 类内部使用。确保 Package 对象只能由 Truckload 类的成员函数创建是合理的。诚然，由于 Package 类未从模块中导出，外部代码本来也无法使用它。但一般来说，你可能想更进一步，采用一种机制，使 Package 对象仅对 Truckload 类的成员私有，而不对模块其余部分可用。可以通过使用嵌套类来实现。嵌套类是在另一个类定义内部定义其定义的类。嵌套类的名称位于外围类的作用域内，并受外围类中成员访问规范的约束。我们可以将 Package 类的定义放在 Truckload 类的定义内部，如下所示：

```cpp
export module truckload;
import box;
import <memory>;
import <vector>;

// We no longer need the truckload:shared_box partition (or any other partition file)
export using SharedBox = std::shared_ptr<Box>;

export class Truckload
{
public:
    // Exact same public member functions as before...

private:
    class Package
    {
    public:
        SharedBox m_box;        // Pointer to the Box object contained in this Package
        Package* m_next;        // Pointer to the next Package in the list

        Package(SharedBox box) : m_box{box}, m_next{nullptr} {} // Constructor
        ~Package() { delete m_next; }                          // Destructor
    };

    Package* m_head {};      // First in the list
    Package* m_tail {};      // Last in the list
    Package* m_current {};   // Last retrieved from the list
};
```

现在，Package 类型局部于 Truckload 类定义的作用域。由于 Package 类的定义位于 Truckload 类的私有部分，因此无法从 Truckload 类外部创建或使用 Package 对象。由于 Package 类完全私有于 Truckload 类，将其所有成员设为 public 也无妨。因此，Truckload 对象的成员函数可以直接访问它们。原 Package 类的 getBox()、getNext() 和 setNext() 成员不再需要。所有 Package 成员都可以从 Truckload 对象直接访问，但在类外部不可访问。

Truckload 类的成员函数定义需要修改，以便直接访问 Package 类的成员变量。这很简单。只需将 Truckload.cpp 中所有出现的 getBox()、getNext() 和 setNext() 替换为直接访问相应成员变量的代码。将 Package 作为嵌套类后得到的 Truckload 类定义可与 Ex12_17.cpp 源文件配合使用。可运行的示例可在代码下载中的 Ex12_18 中找到。

> **注意** 将 Package 类嵌套在 Truckload 类内部，只是在外围类 Truckload 的上下文中定义了 Package 类型。Truckload 类型的对象不会受到任何影响——它们将拥有与之前相同的成员。

嵌套类的成员函数可以直接引用外围类的静态成员，以及外围类中定义的任何其他类型或枚举项。嵌套类可以通过常规方式访问外围类的其他成员：通过类对象，或通过指向类对象的指针或引用。在访问外围类的成员时，嵌套类的成员函数具有与外围类的成员函数相同的访问权限；也就是说，嵌套类的成员函数可以访问外围类对象的私有成员。

### 具有公有访问权限的嵌套类

当然，你也可以将 Package 类定义放在 Truckload 类的公有部分。这意味着 Package 类定义将成为公有接口的一部分，因此*确实*可以在外部创建 Package 对象。由于 Package 类名位于 Truckload 类的作用域内，不能单独使用它。必须用嵌套它的类名来限定 Package 类名。下面是一个示例：

```cpp
Truckload::Package myPackage{ myBox };    // Define a Package object
```

当然，在示例中将 Package 类型设为公有，会否定一开始将其设为嵌套类的理由！话虽如此，在其他情况下，公有嵌套类也可能有意义。我们将在下一小节中看到一个这样的例子。

### 遍历 Truckload 的更好机制：迭代器

getFirstBox() 和 getNextBox() 成员允许你遍历 Truckload 中存储的所有 Box。给类添加类似成员并非闻所未闻——我们在实际代码中至少遇到过两次——但这种模式有一些严重缺陷。也许你已经能想到一个了？

假设你发现——确实如此——Ex12_17 的 main() 函数太长、太拥挤，并决定将其部分功能拆分到可复用的函数中。那么，一个很好的首选候选就是用于查找 Truckload 中最大 Box 的辅助函数。一种自然的写法如下：

```cpp
SharedBox findLargestBox(const Truckload& truckload)
{
    SharedBox largestBox{ truckload.getFirstBox() };

    SharedBox nextBox{ truckload.getNextBox() };
    while (nextBox)
    {
        if (nextBox->compare(*largestBox) > 0)
            largestBox = nextBox;
        nextBox = truckload.getNextBox();
    }

    return largestBox;
}
```

然而不幸的是，这个函数无法编译！你能看出为什么吗？问题的根本原因是，getFirstBox() 和 getNextBox() 都必须更新 truckload 内部的 m_current 成员。这意味着它们都必须是 non-const 成员函数，进而意味着这两个函数都不能在 truckload 上调用，而 truckload 是一个常量引用参数。尽管如此，使用常量引用参数是常规做法。没有人会也不应该期望查找最大 Box 需要修改 Truckload。然而，就目前而言，无法遍历 const Truckload 的内容，这使得我们的 Truckload 对象几乎毫无用处。一个正确的 const Truckload& 引用应当允许代码遍历其中包含的 Box，但同时阻止调用 addBox() 或 removeBox()。

> **注意** 你可以尝试通过将 Truckload 类的 m_current 成员变量声明为 mutable 来绕过这个问题。这样你就可以将 getFirstBox() 和 getNextBox() 都变成 const 成员。虽然作为附加练习这可能对你很有趣，但该解决方案总体上仍有一些缺点。首先，对同一集合进行嵌套循环时你会遇到问题。其次，尽管并发性不在本讨论范围内，但你大概可以想象，使用 mutable 方案也永远无法支持多个执行线程并发遍历。在这两种情况下，每次遍历都需要一个 m_current 指针——而不是每个 Truckload 对象一个。

这个问题的正确解决方案就是所谓的迭代器模式。原理很简单。与其将 m_current 指针存储在 Truckload 对象本身内部，不如将其移到一个专门设计并创建用于遍历 Truckload 的另一个对象中。这样的对象称为迭代器。

> **注意** 在本书后面，你将了解到标准库的容器和算法也广泛使用迭代器。虽然标准库迭代器的接口与我们即将为 Truckload 定义的 Iterator 类略有不同，但基本原理相同：迭代器允许外部代码遍历容器的内容，而无需了解数据结构的内部细节。

让我们看看这对我们来说可能是什么样子。我们将从 Ex12_18 的 Truckload 类开始——也就是 Package 已经是嵌套类的版本——并添加第二个名为 Iterator 的嵌套类。为了向你展示这种可能性，我们还会在外围类的定义之外定义这两个嵌套类。

```cpp
export module truckload;
import box;
import <memory>;
import <vector>;
```
