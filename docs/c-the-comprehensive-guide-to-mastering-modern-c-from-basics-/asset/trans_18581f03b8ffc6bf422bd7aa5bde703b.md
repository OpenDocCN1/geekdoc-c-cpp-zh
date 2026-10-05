

```cpp
// https://godbolt.org/z/Y4sMdzde8
struct StereoImage {
    Image* right; // raw pointer
    Image* left; // raw pointer
    StereoImage(const string& nameBase) // construct
        : right{new Image(nameBase+"right.jpg")}, // okay
          left{new Image(nameBase+"left.jpg")} // dangerous
    {}
    ~StereoImage() { // remove
        delete right; delete left;
    }
    StereoImage(const StereoImage&) = delete; // no copy
    StereoImage& operator=(const StereoImage&) = delete; // no assignment
};

int main() {
    Image* image = new Image("image.jpg"); // a raw pointer?
    StereoImage stereo("3d");
    delete image;
}
```

**Listing 20.7** 当原始指针拥有一个对象时，潜在的错误往往难以检测。

原始指针存储了 `new` 的结果。对应的 `delete` 位于 `main` 函数末尾。但如果这是你程序中的另一个函数，并且在 `delete` 之前抛出了异常会发生什么？`delete` 将永远不会执行，你将导致内存泄漏。在此处始终使用智能指针：

- auto image = make_unique<Image>("image.jpg"); // 也是 unique_ptr
- auto image = make_shared<Image>("image.jpg"); // 也是 shared_ptr

你可能会说：“那我只需要捕获异常并在之后调用 delete 即可。”是的，这可以是一个开始。但在初始化 `links_` 时，这救不了你：在初始化 `links_` 期间，Image 构造函数中的异常具有非常微妙的影响。`right_` 的 `new` 已经执行并请求了内存。初始化 `left_` 期间的异常防止了 `left_` 内存丢失，但 `right_` 无法找回地丢失。因为异常离开了构造函数，`stereo` 被认为未创建——因此带有 `delete` 语句的析构函数不会被调用。你无法访问 `right_` 来清理它。你造成了内存泄漏。[50]

我建议在此处也使用智能指针：

- unique_ptr<Image> right; unique_ptr<Image> left_; 或者
- shared_ptr<Image> right; shared_ptr<Image> left_

然后用它们初始化：`right{ new Image nameBase+"right.jpg" }, left_{ new Image nameBase+"left.jpg" }`。问题解决了。

另一个优势是，你不一定需要用 `= delete` 删除拷贝构造函数和赋值运算符：

- 使用 `unique_ptr`，这些是不可能的，编译器本身无法生成它们——所以你不需要显式地禁止它们。
- 使用 `shared_ptr`，你可以获得这两种操作，如果你使用它们，它们会执行应执行的操作且不会破坏你的程序。

你可以在第 16 章中阅读更多关于删除方法的知识。

当原始指针管理一个对象时，它们不应该拥有它。然而，为了引用属于他人的对象，它们确实非常有用。你已经在列表 20.1 中看到在容器中使用 `*` 来就地修改元素。你之前已经遇到过 `&` 引用，这是一种允许你引用容器中元素的语言元素。但这在示例中并没有起作用。因为尽管 `&` 引用既实用又安全，但它无法完成指针可以完成的两件事：

- **你不能重新赋值引用**
当你写 `int value = 42; int &ref = value;` 时，从现在起 `ref` 将始终引用 `value`。所以通过 `ref = 99;`，你始终是在给 `value` 赋值。然而，如果你有一个 `int *ptr = &value;` 指针，你可以通过 `*ptr = 66;` 实现相同的操作，与引用不同，你可以指向一个完全新的变量。以下内容对于引用将不起作用：

```cpp
int value = 42;
int &ref = value;
ref = 99; // value 变为 99
int *ptr = &value; // ptr 指向 value
*ptr = 66; // value 变为 66，但 ptr 可以指向完全新变量
int new_value = 73; // value 变为 73
ptr = &new_value; // ptr 指向 new_value
```

- **你不能在容器中存储引用**
不存在 `vector<int>&` 之类的结构。引用是只存在于编译器的抽象概念。在编译后的程序和运行时，你不再看到它的踪迹。然而，每个容器都需要为其元素提供物理存在的内存。因此在这里你需要某种形式的指针——智能指针、原始指针，甚至是迭代器，正如你之后会看到的。

在这里，原始指针确实有应用领域。如果容器中的对象不被指针拥有，`unique_ptr` 根本无法考虑。`shared_ptr` 是可行的，但在不需要共享所有权时为什么要管理它呢？原始指针是恰恰的选择。

