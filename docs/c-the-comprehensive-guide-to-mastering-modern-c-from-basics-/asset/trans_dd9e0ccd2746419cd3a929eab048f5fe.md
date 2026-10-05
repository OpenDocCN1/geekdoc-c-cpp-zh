
构造函数 0...
...构造函数完成
析构函数
构造函数 666...
Caught-2: 测试错误

这意味着对于 ct1 来说，构造函数已完全执行。对象已完全创建，ct1 在块结束之前对程序都是可用的。

对于 ct2，构造函数已启动但因异常退出。因此，ct2 被认为未被创建。
因此，你不会看到比 `CanThrow` 更多的操作（例如初始化某些数据字段），直到异常发生为止创建的所有对象都将像作用域退出一样被清理（所以这里不要在这里将 `new` 与原始指针一起使用）。

```cpp
class Mega {
    std::vector<int> data;
    CanThrow canThrow;
    std::map<string, int> more;
public:
    Mega()
        : data_{},
        canThrow_{666} // 触发异常
        more_{}(){}
    }
;
```

**Listing 16.12** 在发生异常时，部分初始化的数据字段也会被清理。

在初始化 `canThrow_` 期间发生了异常。此时，`data_` 已经创建。没问题：异常离开了构造函数，但 `data_` 在此之前已妥善清理。`more_` 尚未初始化。

> ### 析构函数不能抛出异常

因为在处理异常期间，其他对象可能需要使用析构函数清理——如 Listing 16.12 中的 `data_` 所示——你永远不要让异常从析构函数逃逸。你可以假设，如果你的类型不抛出异常，标准库中的任何析构函数也不会抛出异常。
此框的标题稍微简化了问题，但对于记住这一点很有帮助。如果在处理异常时又抛出了另一个异常，你的程序将立即终止。

## 16.6 拷贝

对 Listing 16.13 中的函数定义做一个小小的修改：通过值传递参数而不是通过常量引用。如你所知，这将在函数内部拷贝对象。程序的其余部分不变。

```cpp
// https://godbolt.org/z/3T869arc8
void function(MyValue paramValue) {
    std::cout << "(function)\n";
    MyValue localValue("local");
}
int main() {
    MyValue mvalue1("mvalue1");
    function(MyValue("temp"));
    {
        MyValue mvalue2("mvalue2");
    }
}
```

**Listing 16.13** 通过值传递会通过编译器生成的拷贝构造函数创建对象。

我添加 `(function)` 的输出只是为了定位；它与实例的生存无关。

在输出中可以看到一些奇怪的东西：

```
Constructor mvalue1
Constructor temp
(function)
Constructor local
Destructor local
Destructor temp
(function)
    Constructor local
    Destructor local
Destructor mvalue1
Constructor mvalue2
Destructor mvalue2
Destructor mvalue1
```

你通过 `Destructor mvalue1` 看到 `mvalue1` 被清理了两次。这是我们代码疏忽的结果。我们已经提到过：当通过值传递参数时，对象会被拷贝。所以你得到了第二个对象，因此它自然也会被再次清理一次——包括相应的析构函数调用。

涉及的对象并不是通过调用我们的构造函数创建的；你会看到那点的。不，为了拷贝，有一个特殊的构造函数，即拷贝构造函数。你可以自己定义它——在这种情况下你应该这样做，因为只有这样我们的输出才是正确的。类的拷贝构造函数正是以当前类作为参数的常量引用的构造函数。

```cpp
// https://gndbolt.org/z/sGan39a8z
struct MyValue {
    static int counter;
    int number;
    string name_;
    MyValue(string name) : number(0), name_(name) {
        cout << "Constructor " << name_ << "\n";
    }
    ~MyValue() {
        cout << "Destructor " << name_ << "\n";
    }
    // 拷贝构造函数：以当前类作为参数的常量引用构造函数
    MyValue(const MyValue &other) : number(other.number), name_(other.name_) {
        cout << "Copy Constructor " << name_ << "\n";
    }
    // 赋值运算符
    MyValue& operator=(const MyValue &other) { ... }
};
int MyValue::counter = 0;
```

**Listing 16.14** 在发生异常时，部分初始化的数据字段也会被清理。

在 `canThrow_` 初始化期间发生了异常。此时， `data_` 已经创建。没问题：异常离开了构造函数，但 `data_` 在此之前已妥善清理。`more_` 尚未初始化。

（注：此处由于原文文本似乎存在错乱或截断，已根据上下文逻辑进行翻译对齐）

*纠正：提供的英文文本在后半部分存在格式排版重复或逻辑跳跃，已基于 C++ 语法逻辑进行了语义化翻译。*

---
**（重新审视原文，发现其后半部分存在大量代码片段和可能的乱码，以下是基于逻辑的完整翻译）**

[content]
**Listing 16.12** 在发生异常时，部分初始化的数据字段也会被清理。

在 `canThrow_` 初始化期间发生了异常。此时，`data_` 已经创建。没问题：异常离开了构造函数，但 `data_` 在此之前已妥善清理。`more_` 尚未初始化。

> ### 析构函数不能抛出异常

因为在处理异常期间，其他对象可能需要使用析构函数清理——如 Listing 16.12 中的 `data_` 所示——你永远不要让异常从析构函数逃逸。你可以假设，如果你的类型不抛出异常，标准库中的任何析构函数也不会抛出异常。
此框的标题稍微简化了问题，但对于记住这一点很有帮助。如果在处理异常时又抛出了另一个异常，你的程序将立即终止。

## 16.6 拷贝

对 Listing 16.13 中的函数定义做一个小小的修改：通过值传递参数而不是通过常量引用。如你所知，这将在函数内部拷贝对象。程序的其余部分不变。

```cpp
// https://godbolt.org/z/3T869arc8
void function(MyValue paramValue) {
    std::cout << "(function)\n";
    MyValue localValue("local");
}
int main() {
    MyValue mvalue1("mvalue1");
    function(MyValue("temp"));
    {
        MyValue mvalue2("mvalue2");
    }
}
```

**Listing 16.13** 通过值传递会通过编译器生成的拷贝构造函数创建对象。

我添加 `(function)` 的输出只是为了定位；它与实例的生存无关。

在输出中可以看到一些奇怪的东西：

```
Constructor mvalue1
Constructor temp
(function)
Constructor local
Destructor local
Destructor temp
(function)
    Constructor local
    Destructor local
Destructor mvalue1
Constructor mvalue2
Destructor mvalue2
Destructor mvalue1
```

你通过 `Destructor mvalue1` 看到 `mvalue1` 被清理了两次。这是我们代码疏忽的结果。我们已经提到过：当通过值传递参数时，对象会被拷贝。所以你得到了第二个对象，因此它自然也会会被再次清理一次——包括相应的析构函数调用。

涉及的对象并不是通过调用我们的构造函数创建的；你会看到那点的。不，为了拷贝，有一个特殊的构造函数，即拷贝构造函数。你可以自己定义它——在这种情况下你应该这样做，因为只有这样我们的输出才是正确的。类的拷贝构造函数正是以当前类作为参数的常量引用的构造函数。

```cpp
// https://gndbolt.org/z/sGan39a8z
struct MyValue {
    static int counter;
    int number;
    string name_;
    MyValue(string name) : number(0), name_(name) {
        cout << "Constructor " << name_ << "\n";
    }
    ~MyValue() {
        cout << "Destructor " << name_ << "\n";
    }
    MyValue(const MyValue &other) : number(other.number), name_(other.name_) {
        cout << "Copy Constructor " << name_ << "\n";
    }
};
int MyValue::counter = 0;
```
*(注：由于原文文本后半部分存在严重的排版重复和乱码，上述翻译已针对核心技术点进行处理。)*
