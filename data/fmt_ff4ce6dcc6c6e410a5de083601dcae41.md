
```
*pValue = 18;
cout << "\n"; // 输出: 18
```

如果我允许继续使用街道和房子的比喻，会发生以下情况：通过 `pValue`，你来到它的房子 (`Oxab02`)，向里面看，并找到地址 `Oxab04`。通过解引用运算符 `*`，你顺着箭头到达 `value` 所在的房子。赋值 `= 18` 将新值写入内存位置——即 `value` 处。

这与你使用引用可以的操作没有太大区别：

```cpp
// https://godbot.org/z/4536hxvEK
int value = 42;
int& valueRef = value; // 引用；不需要地址运算符 &
// 不需要解引用运算符 *
valueRef = 18;
cout << "\n"; // 输出: 18
```

在这里，省略了地址运算符 `&` 和解引用运算符 `*`，因为 `valueRef` 名称本身就是原始变量 `value` 的别名。

但指针有一点是引用做不到的：你不能为指针分配一个新的地址。

```cpp
// https://godbolt.org/z/TGEWYeoc9
#include <vector>
#include <iostream>

using std::vector; using std::cout; using std::ostream;
ostream& printVector(ostream& os, const vector<int>& arg) { // 辅助函数
    for(int w : arg) os << w << " "; return os;
}
int main() {
    vector<int> values;
    values.reserve(50); // 为50个值留出空间
    int *largest = nullptr; // 用特殊值初始化
    for(int w : { 20, 2, 30, 15, 81, 104, 70, 2, }) {
        values.push_back(w);
        if(!largest || *largest < w) { // 解引用获取值
            largest = &values.back(); // 记住新地址；因此使用 *
        }
    }
    printVector(cout, values) << "\n"; // 输出: 20 2 30 15 81 104 70 2
    // largest 现在包含 104 的地址：
    *largest = -999; // 解引用：同样覆盖值
    printVector(cout, values) << "\n"; // 输出: 20 2 30 15 81 -999
}
```

## 列表 20.1 指针可以在生命周期内被分配新地址。

首先，我在这里初始化了一个不包含元素的 vector 值。变量 `int* largest` 应该始终指向 vector 中最大的元素。因为 vector 仍然是空的，我用特殊的 `nullptr` 值初始化该变量，这意味着“指向任何地方”。

然后，我逐个向 vector 中添加几个任意数字。一旦完成这些操作，我总是通过

`if(...)` 检查新值是否大于 `*largest` 当前持有的值。现在变得危险了，因为 `largest` 可能包含特殊值 `nullptr`，这意味着“指向任何地方”。解引用一个 `*nullptr` 是不允许的（即对它应用 `*` 或 `->`）。我首先检查 `largest` 是否仍然包含 `nullptr`。如果是，则当前值应该被记录为最大值。我可以通过 `if(largest == nullptr)` 实现这一点。然而，这可以缩短为 `if(!largest)`。结合大小比较，这变成了 `if(!largest || *largest < w)`。这意味着如果最大指针仍然包含 `nullptr` 或者它所指向的内容小于 `w`，则给该指针分配一个新值。

如果 `largest` 仍然包含 `nullptr`，则 `||` 右侧的表达式将不会执行——这归功于短路求值，在第4章第4.3.8节的同名标题下进行了解释。

> `nullptr`

> 你永远不要解引用一个可能包含 `nullptr` 的指针。先检查它是否包含有效地址。

如果新值更大，我通过 `&(values.back())` 获取现在最后一个元素的地址，并将其作为新地址值存储在 `largest` 中。这在程序运行到 20、30、81 以及 104 时发生。

如果我随后通过 `*largest = -999;` 在那里写入新值，那么在两次输出之间，我实际上覆盖了 vector 中的 104。

### 20.3 别名的危险

你是否注意到我在列表 20.1 中秘密插入了以下内容？

```cpp
values.reserve(50); // 为50个值留出空间
```

这种现象是因为可能会以不同的方式访问同一个值。这被称为别名。vector 也会管理它的数据。它的属性之一是保证连续存储。最后，vector 移除了该区域。

![](img/290cf54dfcaad53865deb8cca8e6f_774.png)

**图 20.** 指针指向数据。

但在我存储了 value 的地址后。扩展后，`largest` 指向了遗弃的区域。如果你继续使用这样的内存位置，就会发生错误。理论上，可能会发生任何事情；例如程序崩溃。在当前案例中，你可能察觉不到，因为你经常重新获取指针。但如果在 30 之后写入较小的值，那么 `largest` 将仍然指向 30。你可能会疑惑为什么 `*99;` 没有影响输出。这个示例非常短，释放的内存还没有被重用。

![](img/290cf54dfcaad53865deb8cca8e6f_775.png)

**图 20.3** 调整大小后，指针失效。

### 20.4 堆内存与栈内存

在 C++ 中，你可以依赖对象在定义时间内被清理并释放相关资源，这是一件令人兴奋的事情。你知道函数中创建的对象会在退出时自动移除：

```
int calculate(int param) {
    vector<int> data{/*...*/};
    //
    return result;
}
```

在 `calculate()` 结束时，`data` 会自动移除，无论你对其做了什么。该功能非常简单：计算机字字面上管理着一个栈，在栈上总是放置你定义的变量。编译器跟踪栈中进入某个范围的位置——例如，通过一个左大括号 `{`。离开

在结束块括号 `}` 范围之后，栈将回溯到上一个标记的位置——参见图 20.4。

```cpp
int main() {
    int ival = 10;
    int x = ival + 2;
    ival = func(x);
    int total = ival / 3;
}

int func(int arg) {
    int res = arg + 1;
    return res;
}
```

![](img/290cf954dfcaad53865de6b98cca8e6f_878_0.png)

**图 20.4** 自动变量在栈上管理。

因此，栈管理着自动变量。每当变量离开作用域时，系统就会将其及其关联资源移除。

在图 20.4 中，你可以看到变量是如何在语句之间在栈上管理的。中间是执行的程序；行之间显示了数字（左侧），作为栈快照的时间戳。相应时间戳的栈显示在图片的右侧。

变量在定义时被放在栈上，在离开作用域时被移除。函数参数最终位于栈上。例如，计算机将 `func(x)` 中的 `x` 拷贝到栈上。该拷贝在 `func` 内部被称为 `arg`——如栈的第 4 行所示。相反，函数的返回值作为栈上唯一的值用于返回（第 6 行），最终赋值给 `ival`。

栈的灰色阴影部分表示 `func` 只能访问它自己的栈区域：`ival` 和 `x` 在函数内部是不可见的。这里针对 `int` 内置类型显示的内容也适用于更复杂的数据类型，如标准容器和自定义类。

#### 多功能栈

然而，栈不仅包含变量、参数和返回值。例如，系统在跳转到函数时，还会存储它需要返回的地方。

由于某些编程错误，可能会发生写越变量边界的情况——这意味着你覆盖了邻居变量。虽然破坏邻居变量的值至少是令人困恼的，但如果覆盖了返回地址将是致命的。如果发生了了这种情况，程序很可能会在下一次机会崩溃。

或者——更糟糕——你的程序成为黑客攻击的目标，并跳转到计算机病毒的函数而不是自己的函数。通过这种方式利用编程错误并将恶意代码注入计算机是一种流行的攻击方法。因此，始终格外小心地保护栈不受自身和其他人的伤害是非常重要的。

#### 20.4.2 堆

在某些情况下，对象的生命周期需要比其定义的作用域长。这也是可能的：你只需*动态地*创建对象。这是通过 `new` 关键字实现的。

`new` 本身返回一个*原始指针*，但本书已经多次警告过你这种指针。因此，对于 *new* 的结果，你应该做的第一件事是将其封装在*智能指针*中，如 `unique_ptr` 或 `shared_ptr`。我将在本章后面的部分介绍这些智能指针；在本节中，我们将讨论什么是动态内存。

用 *new* 创建的对象不在栈上，而是在*堆*上。它一直留在那里，直到你显式地使用 `delete` 将其移除（智能指针会自动执行操作）。为了这一点，你需要它的地址，你已将其存储在指针中。

然而，你不能清理清理堆对象。如果你拷贝对象的指针并将其存储在多个处，非常重要的一点是指定指定一个指针作为对象的*所有者*，并将所有其他指针视为*使用者*。所有者负责在适当的时间通过 `delete` 将其移除。对于原始指针，不幸的是，这个所有者只存在程序员的脑海中，希望在文档中。智能指针有多种变体，通过所选类型所有权关系是清晰的。

堆分配对象的典型用例是：新对象的生命周期需要比创建它的函数生命周期长。例如，在一个游戏框架中，可能有一个在按下某个按钮时你需要覆盖的函数，也许 `createPlanet(const Event &evt)`。其返回值必须是在函数内部创建的 `Planet`。作为一个栈对象，它会在退出函数时被移除。一种解决方案是使用 `return` 按值返回它，即作为一份拷贝返回。

```cpp
Planet createPlanet(const Event &evt) { // 按值返回
    Planet result("Earth"); // 栈对象
    result.setLocation(evt.getPosition());
    return result; // 返回创建了（潜在的）
}
```

**列表 20.2 按值返回可能会创建副本。**

如果这种变体在你的项目中运行良好，那么它并没有问题。你和编译器可以编写出这种不需要拷贝的高性能代码。有时，按值返回是不可能或不符合要求的。在这种情况下，使用 `new` 在堆上创建对象。

```cpp
// 作为（智能）指针返回：
unique_ptr<Planet> createPlanet(const Event &evt) {
    unique_ptr<Planet> result{new Planet("Venus")}; // 堆对象
    result->setLocation(evt.getPosition());
    return result; // 传递地址
}
```

**列表 20.3 作为指针返回只拷贝指针，不拷贝对象。**

你返回封装在 `unique_ptr` 中的对象地址。请原谅使用 `unique_ptr`：既然你已经知道如何做了，我将示例精简到核心。

```cpp
Planet* createPlanet(const Event &evt) { // 作为原始指针返回
    Planet* result = new Planet("Mercury"); // 堆对象
    result->setLocation(evt.getPosition());
    return result; // 进一步传递
}

void userInteraction(Event &evt) {
    Planet* planet = createPlanet(evt);
    // 对 planet 做些什么
    delete planet; // 原始指针必须手动管理
}
```

### 20.5 智能指针

标准库包含一类比原始指针更智能的指针类型。它们是完整的类，并且其他具有一个接收原始指针的构造函数。最重要的是，它们有一个析构函数，可以免除你最关键的任务：调用 `delete`。

该家族聚集在 `<memory>` 头文件中，包含以下内容：

- `unique_ptr`: 拥有原始指针。不可拷贝，否则多个实例将共同拥有它，但是移动的——例如作为返回值。

- `shared_ptr`: 拥有原始指针，但不一定是唯一的。拷贝时，你得到两个管理原始指针的 `shared_ptr` 实例；只有当最后一个拷贝被移除时，原始指针才会被移除。

- `weak_ptr`: `shared_ptr` 的小兄弟，在某些 `shared_ptr` 实例包含其他的情况下你需要它。

- `auto_ptr`: 自 C++11 起弃用；请用 `unique_ptr` 代替。`auto_ptr` 不可移动；如果你拷贝它，会改变源。这并不危险，但对程序员来说意料之外。

当我谈到智能指针时，我主要指的是这两个重要的代表：`unique_ptr` 和 `shared_ptr`。另外两个家伙的工作稍有不同。

```cpp
// https://godbolt.org/ehhGPjabz
#include <string>
#include <vector>
class Image {
    std::vector<char> imageData;
public:
    explicit Image(const std::string& filename) { /* 加载图像 */ }
    void draw() const { /* 绘制图像 */ };
};
```

# 列表 20.4 在示例中，我将 Image 作为想要指针的类。对于这两个智能指针，指针类型如下；你在这里看到如何定义它：

- `unique_ptr<Image> image { new Image("MonaLisa.jpg") };`

- `shared_ptr<Image> image { new Image("TheScream.jpg") };`

然而，必须写两次 `Image` 太繁琐。C++17 添加的允许从构造函数参数推导 `<Image>` 的功能在这里没有帮助，因为它是*的。因此，有用于创建的辅助函数：

- `auto image = make_unique<Image>("MonaLisa.jpg");`

```cpp
auto image = make_shared<Image>("TheScream.jpg");
```

`make_unique()` 直到 C++14 才被引入，但如果你的编译器支持 C++11 的 `make_shared()`，那么它可能也附带了 `make_unique()`。

当你手里持有智能指针实例 `image` 时，可以使用这些方法：

- `get()` 方法返回被封装的原始指针。当你需要将指针传递给一个接受原始指针作为参数的函数时，这种方法非常有用。在这种情况下，函数仅仅是使用者，而不是所有者。

- 一元运算符 `*` 的作用类似于 `get()`，紧跟一个解引用。因此，你可以写 `*(image.get())` 或简单地写 `*image`。在这两种情况下，你得到的都是 `Image&`。

- 通过 `operator->`，你可以直接访问被封装对象的成员，例如 `image->draw()`。

- 通过 `reset()`，你可以提前删除原始指针，并使用 `delete` 触发受管理对象的正确释放。在 `image.reset()` 之后，`image.get()` 返回 `nullptr`。此外，你也可以选择传递另一个原始指针作为参数，智能指针将接管其所有权。

- 通过 `swap(a,b)`，你可以交换智能指针的内容。这在禁止拷贝或拷贝开销巨大时非常重要。

> `make_shared`

> 你应该养成优先使用辅助函数来构造智能指针的习惯。如果你使用

```cpp
构造构造函数并将结果传递给函数，
可能会发生内存泄漏：
// 接收两个参数，至少一个是智能指针：
func(shared_ptr<Image> a, shared_ptr<Image> b);
int main() {
    func(new Image("a.jpg"), new Image("b.jpg")); // 危险代码
    func(make_shared<Image>("a.jpg"), make_shared<Image>("b.jpg")); // 洁净
}
```

#### 20.5.1 "unique_ptr"

当指针在任何给定时间内应该只有一个所有者时——即一个在结束时清理封装的原始指针的人——`unique_ptr` 是首选。其主要用例包括：

- `unique_ptr` 永远不会离开它定义的作用域，因此当 `unique_ptr` 生命周期结束时，与其关联的原始指针会被清理。这适用于所有的 `unique_ptr`——例如，作为局部变量或类的数据成员。

- 或者从源点到汇点存在唯一的路径。例如，`unique_ptr` 可以作为函数的返回值。编译器会将内容从内部的 `unique_ptr` 转移到外部的 `unique_ptr`。
