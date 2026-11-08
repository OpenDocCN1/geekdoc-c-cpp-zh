
现在如果再次运行 `main()`，一切恢复正常。你会看到构造函数和析构函数的数量一样多：

```text
    Constructor mvalue1
    Constructor temp
(function)
    Constructor local
    Destructor local
    Destructor temp
    Copy constructor mvalue1-copy
(function)
        Constructor local
        Destructor local
        Destructor mvalue1-copy
            Constructor mvalue2
            Destructor mvalue2
        Destructor mvalue1
```

在之前看到第一个 Destructor mvalue1 的地方，你会看到实际上之前不可见的副本正在被销毁；这一点由 Destructor mvalue1-copy 中改变后的名称揭示出来。

但即使没有复制构造函数，我们的程序也运行了。如果你不定义自己的复制构造函数，编译器会再次替你接管。它生成一个复制构造函数，将所有数据字段逐元素复制到新实例中。这对你目前遇到的所有数据类型都非常有效：内置类型、标准容器以及标准库中的大多数其他类型。

然而，如果你使用某些需要在析构函数中进行特殊处理的东西，这就不起作用了。原始指针和来自清单 16.7 的 `db_` 资源不会被正确复制（只会转移指针或句柄本身），并且资源不会被请求两次。而且我们的 `cout << "Destructor "` 输出也属于这一类，因为析构函数中做了一些特殊处理。作为经验法则，请参见下面的方框。

### 何时需要复制构造函数？

如果你自己编写（或需要编写）析构函数来确保类正常工作，那么你很可能也需要自己编写的复制构造函数——反过来也一样。你在析构函数中管理的资源很可能在复制和赋值时也需要特殊处理。

如果可能，你应尽量不自己编写复制构造函数。编译器不仅会替你处理复制操作；它还会做其他重要的小事情。这包括在待复制的数据字段允许时自动标记为 `noexcept`。在某些情况下，这可以生成更快的代码。

## 16.7 赋值运算符

你现在已经熟悉 MyValue 类，也知道可以使用 MyValue(string) 构造函数创建新实例，或通过 MyValue (const MyValue&) 进行复制。你还知道用 = 进行赋值，因此应该能够准确说出以下示例中发生了什么。

```cpp
void byVal(MyValue arg) {
}

int main() {
    MyValue value1{"ABCD"};    // new instance, constructed via string
    MyValue value2{value1};     // new instance, constructed via copy
    MyValue value3 = value1;    // new instance, also via copy, despite =
    byVal(value1);         // a new instance via copy
    value1 = value2;        // not a new instance, but an assignment
}
```

**清单 16.15** 复制与赋值。

虽然前两行没有什么意外，但有时人们可能会对 `MyValue value3 = value1;` 扬起眉毛。因此，提醒一下：变量声明中的等号 `=` 绝不是赋值，而只是编写初始化的另一种方式。为了避免阅读时产生混淆，你应避免这样做——至少在处理真正的类时如此。对于像 `int` 这样的简单类型，`int val{7}` 对某些人来说可能看起来奇怪，所以这里可以放心地使用 `=` 进行初始化。

现在回到赋值。在 `value1 = value2;` 中，你现在遇到了新东西。再次简化一下，你有以下代码：

```cpp
// https://godbolt.org/z/5M8xKabjK
int main() {
    MyValue value1{"ABCD"};
    MyValue value2{"WXYZ"};
    value1 = value2;        // assignment
}
```

你现在得到这个：

```text
Constructor ABCD
  Constructor WXYZ
  Destructor WXYZ
  Destructor WXYZ
```

哎呀，这里事情又搞混了。`Destructor WXYZ` 输出出现了两次，令人费解。这里发生了什么？

在 `value1 = value2;` 中，编译器调用 `MyValue` 类的**赋值运算符**。你自己没有定义赋值运算符（因为你正在学习它），所以编译器再次替你介入并生成一个赋值运算符——所有数据字段都逐元素地从 `value2` 赋值给 `value1`。`value1` 之前包含的内容随后被覆盖。

因此，很明显，如果没有 `Destructor ABCD` 赋值，这两行 `Destructor WXYZ` 输出中的一行本来会被输出。并且 `number_` 字段中的缩进深度被覆盖了。

你可能想要不同的行为；例如，你可能想保留原对象的缩进深度。为此，实现一个具有以下签名的特殊方法：

```cpp
MyValue& MyValue::operator=(const MyValue&);
```

注意，这是一个*方法*，而不是*构造函数*。被赋值的对象已经存在；它的内容将由这个赋值运算符覆盖。因为它不是构造函数，所以你不是在初始化列表中完成数据字段的转移，而是像方法一样在函数体中进行。

```cpp
// https://godbolt.org/z/s65GVY9xj
struct MyValue {
    // ... everything else as before
    MyValue& operator=(const MyValue& right) {
        if (this != &right) { // 1. check for self-assignment
            // 2. Release previous resources; none here
            // 3. element-wise transfer by assignment or similar
            name_ = right.name_ + "-Assignment (previously " + name_ + ")";
            /* number_ remains, and thus the original indentation */
        }
        return *this; // 4. return self
    }
};
```

**清单 16.16** 实现自定义赋值运算符的架构。

如果将其插入 `struct MyValue` 的定义中，你将得到以下输出：

```text
Constructor ABCD
  Constructor WXYZ
  Destructor WXYZ
Destructor WXYZ-Assignment (previously ABCD)
```

这样世界又恢复秩序：你可以从文本和缩进中看出哪个原对象被覆盖，以及它何时被清除。

如果你为自己的类定义 `operator=` 赋值运算符，务必遵循前面展示的实现模式：

- 1. 用 `if (this != &right)` 检查 this 是否与 `&right` 具有相同地址。如果不这样做，像 `value1 = value1` 这样的自赋值可能会出现问题。
- 2. 释放待覆盖对象的所有先前资源。这在清单 16.16 的第 2 点中指出，因为这里对 `MyValue` 没有什么要做。
- 3. 按第 3 点所述将所有元素从 right 转移到左侧……这通常通过赋值或某种其他形式的复制来完成。因为在这种情况下你故意省略了 `number_` 的转移，所以添加一条关于这种不寻常做法的注释。
- 4. 然后用 `return *this` 返回对当前对象的引用。这允许像 `value1 = value2 = value3 = value4;` 这样的赋值链。

赋值运算符与复制构造函数的相似之处非常广泛：

- 通常，你不需要自定义赋值运算符；对于内置数据类型、标准容器以及标准库的大多数类型，编译器生成的赋值运算符至少一样好。
- 如果你自己定义（或需要定义）复制构造函数或析构函数，通常也需要自己的赋值运算符——反过来也一样。

除了实现赋值运算符的方式不同之外，还有另一个关键区别：如果你的类中有 `const` 数据元素，那么赋值运算符会从可用操作列表中移除——或者说被“删除”。后果是你不能再通过赋值覆盖实例。为了说明，我将 `MyValue` 类简化为一个构造函数和一个常量数据字段。

```cpp
struct MyNumber {

    const int number_;        // constant data field

    explicit MyNumber(int v)
        : number_{v}          // initialization of the constant data field
    {}
};

int main() {
    MyNumber c1{4};
    MyNumber c2{7};
    c1 = c2;                  // ✗ Error: Assignment removed by compiler
}
```

**清单 16.17** “const” 数据元素最初没有赋值运算符。
