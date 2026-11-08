
这个示例将使用任何包含 operator<<() 的 Box 类，这使得将 Box 输出到 std::cout 更容易。我们也可以移除 Truckload 的 listBoxes() 成员，并为 << 运算符添加一个重载，以便将 Truckload 对象输出到流，类似于 Box 类。如果你使用为练习12-6创建的 Truckload 类（即包含嵌套 Iterator 类的那个），你可以实现这个运算符函数而无需 friend 声明。它的定义如下：

```cpp
std::ostream& operator<<(std::ostream& stream, const Truckload& load)
{
    size_t count {};
    auto iterator = load.getIterator();
    for (auto box = iterator.getFirstBox(); box; box = iterator.getNextBox())
    {
        std::cout << *box << ' ';
        if (!(++count % 4)) std::cout << std::endl;
    }
    if (count % 4) std::cout << std::endl;
    return stream;
}
```

你可以用它替换旧 Truckload 类的 listBoxes() 成员函数。代码与 listBoxes() 代码类似，只是现在只使用公有函数，而不是直接处理列表中的 Packages。该函数使用 Box 类的 operator<<() 函数。现在输出 Truckload 对象将非常简单——你只需使用 << 将其写入 cout。

如果你同时向 Truckload 类添加数组下标运算符和流输出运算符，可以使用以下程序来练习这些新运算符：

```cpp
// Ex13_10.cpp
// Using the subscript operator
import <iostream>;
import <memory>;
import <random>;     // For random number generation
import <functional>;  // For std::bind()
import truckload;

// Add the createUniformPseudoRandomNumberGenerator() function from Ex13_05 here.

int main()
{
    const double limit {99.0};      // Upper limit on Box dimensions
    auto random = createUniformPseudoRandomNumberGenerator(limit);

    Truckload load;
    const size_t boxCount {16};     // Number of Box object to be created

    // Create boxCount Box objects
    for (size_t i {}; i < boxCount; ++i)
        load.addBox(std::make_shared<Box>(random(), random(), random()));

    std::cout << "The boxes in the Truckload are:\n";
    std::cout << load;

    // Find the largest Box in the Truckload
    double maxVolume {};
    size_t maxIndex {};
    size_t i {};
    while (load[i])
    {
        if (load[i]->volume() > maxVolume)
        {
            maxIndex = i;
            maxVolume = load[i]->volume();
        }
        i++;
    }

    std::cout << "\nThe largest box is: ";
    std::cout << *load[maxIndex] << std::endl;

    load.removeBox(load[maxIndex]);
    std::cout << "\nAfter deleting the largest box, the Truckload contains:\n";
    std::cout << load;
}
```

当我们运行这个示例时，它产生了以下输出：

```text
The boxes in the Truckload are:
Box(47.7,20.3,38.5) Box(68.3,35.4,63.3) Box(10.1,81.2,4.1) Box(32.2,71.6,88.4)
Box(44.6,87.2,10.0) Box(73.3,78.2,18.7) Box(25.9,70.0,51.6) Box(42.7,49.8,71.9)
Box(35.0,82.5,74.9) Box(46.3,46.3,89.9) Box(77.0,88.5,82.1) Box(77.7,59.3,96.8)
Box(26.2,32.2,18.0) Box(58.5,75.0,21.5) Box(42.3,13.6,71.6) Box(31.3,13.6,94.4)

The largest box is: Box(77.0,88.5,82.1)
After deleting the largest box, the Truckload contains:
Box(47.7,20.3,38.5) Box(68.3,35.4,63.3) Box(10.1,81.2,4.1) Box(32.2,71.6,88.4)
Box(44.6,87.2,10.0) Box(73.3,78.2,18.7) Box(25.9,70.0,51.6) Box(42.7,49.8,71.9)
Box(35.0,82.5,74.9) Box(46.3,46.3,89.9) Box(77.7,59.3,96.8) Box(26.2,32.2,18.0)
Box(58.5,75.0,21.5) Box(42.3,13.6,71.6) Box(31.3,13.6,94.4)
```

`main()` 函数现在使用下标运算符从 Truckload 对象访问指向 Box 对象的指针。你可以从输出中看到下标运算符正常工作，并且查找和删除最大 Box 对象的结果正确。现在将 Truckload 和 Box 对象输出到标准输出流的工作方式与基本类型相同。

> **注意** 对于 Truckload 对象，下标运算符掩盖了一个特别低效的过程。因为很容易忘记每次使用下标运算符都涉及从开头遍历列表的至少一部分，所以在生产代码中添加此运算符之前应三思。特别是如果 Truckload 对象包含大量盒子，使用此运算符可能会对性能造成灾难性影响。

正因如此，标准库的作者决定不为他们的链表类模板 `std::list<>` 和 `std::forward_list<>` 提供任何下标运算符。重载下标运算符最好保留给那些可以由高效元素检索机制支持的情况。

为了解决 Truckload 数组下标运算符的这个性能问题，你应该要么省略它，要么将 Truckload::Packages 的链表替换为 `std::vector<SharedBox>`。我们最初使用链表的唯一原因是教学目的。在现实生活中，你很可能永远不应使用链表。`std::vector<>` 几乎总是更好的选择。我们将把此版本 Truckload 的实现推迟到第20章的练习。

## 修改重载下标运算符的结果

你可能会遇到这样的情况：你想重载下标运算符并使用它返回的对象，例如，在赋值左侧或对其调用函数。使用当前 Truckload 类中 `operator[]()` 的实现，如果编写以下任一语句，程序可以编译但不会正确工作：

```cpp
load[0] = load[1];
load[2].reset();
```

这会编译并执行，但不会影响列表中的项。你想要的是列表中的第一个指针被第二个替换，并且第三个被重置为 null，但这不会发生。问题在于 `operator[]()` 的返回值。该函数返回一个智能指针对象的临时副本，它指向与列表中原始指针相同的 Box 对象，但却是不同的指针。每次你在赋值左侧使用 `load[0]` 时，你得到的是列表中第一个指针的不同副本。两条语句都会执行，但只是修改列表中指针的副本，而这些副本不会存在很久。

这就是为什么下标运算符通常返回对数据结构内部值的引用，而不是该值的副本。然而，对 Truckload 类这样做带来了一个重大挑战。你不能再从 Truckload 类的 `operator[]()` 返回 `nullptr`，因为你不能返回对 `nullptr` 的引用。显然，在这种情况下你也绝不能返回对局部对象的引用。你需要设计另一种方式来处理无效索引。最简单的解决方案是返回一个不指向任何对象且永久存储在全局内存某处的 SharedBox 对象。

你可以通过将以下声明添加到类的私有部分，将 SharedBox 对象定义为 Truckload 类的静态成员：

```cpp
static SharedBox nullBox {};  // Pointer to nullptr
```

现在我们可以将下标运算符的定义改为：

```cpp
SharedBox& Truckload::operator[](size_t index)
{
    size_t count {};              // Package count
    for (Package* package{m_head}; package; package = package->m_next)
    {
        if (count++ == index)      // Up to index yet?
            return package->m_box;  // If so return the pointer to Box
    }
    return nullBox;
}
```

现在它返回对指针的引用，并且该成员函数不再是 const。下面是 Ex13_10 的扩展，用于尝试在赋值左侧使用下标运算符。我们只是扩展了 Ex13_10 中的 main()，以表明遍历 Truckload 列表中的元素仍然有效：

```cpp
int main()
{
    // All the code from main() in Ex13_10 here...

    load[0] = load[1];          // Copy 2nd element to the 1st
    std::cout << "\nAfter copying the 2nd element to the 1st, the list contains:\n";
    std::cout << load;

    load[1] = std::make_shared<Box>(*load[2] + *load[3]);
    std::cout << "\nAfter making the 2nd element a pointer to the 3rd plus 4th,"
              << " the list contains:\n";

    std::cout << load;
}
```

你可以在 Ex13_11.cpp 中找到完整程序。输出的第一部分与上一个示例类似，之后的输出如下：

```text
After copying the 2nd element to the 1st, the list contains:
Box(85.5,33.0,56.9) Box(85.5,33.0,56.9) Box(78.3,54.1,43.9) Box(69.1,31.6,78.1)
Box(41.6,30.0,14.8) Box(23.8,22.1,97.8) Box(97.8,33.4,74.0) Box(88.4,83.6,65.7)
Box(19.8,13.7,14.6) Box(77.6,72.1,35.0) Box(87.7,51.6,15.4) Box(95.0,53.5,83.9)
Box(65.6,29.6,91.7) Box(88.8,16.5,73.7) Box(64.3,2.7,30.7) Box(69.9,51.5,85.9)
Box(29.0,20.5,76.4) Box(72.8,19.2,49.1) Box(59.9,56.3,8.9)

After making the 2nd element a pointer to the 3rd plus 4th, the list contains:
Box(85.5,33.0,56.9) Box(78.3,31.6,92.0) Box(78.3,54.1,43.9) Box(69.1,31.6,78.1)
Box(41.6,30.0,14.8) Box(23.8,22.1,97.8) Box(87.8,33.4,74.0) Box(88.4,83.6,65.7)
Box(19.8,13.7,14.6) Box(77.6,72.1,35.0) Box(87.7,51.6,15.4) Box(95.0,53.5,83.9)
Box(65.6,29.6,91.7) Box(88.8,16.5,73.7) Box(64.3,2.7,30.7) Box(69.9,51.5,85.9)
Box(29.0,20.5,76.4) Box(72.8,19.2,49.1) Box(59.9,56.3,8.9)
```

第一块新输出表明前两个元素指向同一个 Box 对象，因此赋值按预期工作。第二块输出来自为 Truckload 对象中的第二个元素赋新值；新值是指向由第三个和第四个 Box 对象相加得到的 Box 对象的指针。输出表明第二个元素指向一个新对象，该对象是接下来两个对象之和。为了清楚说明发生了什么，执行此操作的语句等价于以下内容：

```cpp
load.operator[](1).operator=
    std::make_shared<Box>(load.operator[](2)->operator+(*load.operator[](3)));
```

清楚多了，不是吗？
