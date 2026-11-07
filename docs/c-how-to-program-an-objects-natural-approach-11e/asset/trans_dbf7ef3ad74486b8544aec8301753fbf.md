

## noexcept 说明符

如果函数不抛出任何异常，也不调用任何会抛出异常的函数，则应明确说明该函数不抛出异常。<sup>21</sup> 只需在原型和定义的函数签名后添加 `noexcept`。对于常量成员函数，`noexcept` 必须放在 `const` 之后。如果 `noexcept` 函数调用了另一个会抛出异常的函数，而该 `noexcept` 函数没有处理该异常，则程序会立即终止。

`noexcept` 说明符后面可以选择性地跟一对括号，其中包含一个求值为 `true` 或 `false` 的 `bool` 表达式。单独的 `noexcept` 等价于 `noexcept(true)`。在函数签名后跟 `noexcept(false)` 表示类的设计者已经考虑过该函数是否可能抛出异常，并决定它可能会抛出异常。在这种情况下，客户端代码程序员可以决定是否将对该函数的调用包装在 `try` 语句中。

## MyArray 类的移动构造函数

**移动构造函数**（第52–56行）声明一个*右值引用*（`&&`）参数，表示其 `MyArray` 实参必须是临时对象。成员初始化列表将成员 `m_size` 和 `m_ptr` 从实参移动到正在构造的对象中。

```cpp
// move constructor: must receive an rvalue reference to a MyArray
MyArray::MyArray(MyArray&& original) noexcept
    : m_size{std::exchange(original.m_size, 0)},
      m_ptr{std::move(original.m_ptr)} { // move original.m_ptr into m_ptr
    std::cout << "MyArray move constructor\n";
}
```

回顾第11.6.2节，对被移动对象唯一有效的操作是给它赋另一个对象或销毁它。**从对象移动资源时，应使该对象处于能够被正确析构的状态。此外，它不应再引用已移动到新对象的资源。<sup>22</sup>** 为了对 `m_size` 成员做到这一点，第53行：

- 调用标准库 `exchange` 函数（头文件 `<utility>`），该函数将其第一个参数（`original.m_size`）设置为第二个参数的值（`0`），并返回其第一个参数的原值，然后
- 用 `exchange` 返回的值初始化新对象的 `m_size`。

当 `unique_ptr` 被**移动构造**时，如第54行所示，其**移动构造函数**将源 `unique_ptr` 的动态内存所有权转移给目标 `unique_ptr`，并将源 `unique_ptr` 设置为 `nullptr`。<sup>23</sup> 如果你的类管理原始指针，则必须显式将源指针设置为 `nullptr`——或者类似第53行使用 `exchange`。

21. C++ Core Guidelines，“F.6：如果你的函数可能不抛出异常，就将其声明为 `noexcept`。”访问日期：2023年4月18日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rf-noexcept。
22. C++ Core Guidelines，“C.64：移动操作应移动其源对象并使其保持有效状态。”访问日期：2023年4月18日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-move-semantics。
23. “`std::unique_ptr<T,Deleter>::unique_ptr`。”访问日期：2023年4月18日。https://en.cppreference.com/w/cpp/memory/unique_ptr/unique_ptr。

### 移动并不移动任何东西

尽管我们说移动构造函数将 `m_size` 和 `m_ptr` 成员从实参对象“移动”到正在构造的对象中，但它实际上并没有移动任何东西。<sup>24</sup>

- 对于像 `size_t` 这样的基础类型（它只是一个无符号整数），值从源对象的成员复制到新对象的成员。
- 对于原始指针，源对象指针中存储的地址被复制到新对象的指针中。
- 对于对象，调用该对象的移动构造函数。`unique_ptr` 的移动构造函数通过将动态分配内存的地址从源 `unique_ptr` 的底层原始指针复制到新对象的底层原始指针，然后将 `nullptr` 赋给源 `unique_ptr` 以表示它不再管理任何数据，从而**转移动态内存的所有权**。

下图展示了将带有原始指针成员的源对象 x 移动到名为 y 的新对象的概念。注意移动后 x 的两个成员都为 0——指针成员中的 0 表示空指针。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_682_0.png)

## MyArray 类的移动赋值运算符（=）

移动赋值运算符（=）（第59–69行）定义一个*右值引用*（`&&`）参数，表示其 MyArray 实参的资源应被移动（而非复制）。第62行测试自赋值，即一个 MyArray 对象被赋值给自身。<sup>25</sup> 当 `this` 等于右操作数的地址时，赋值两侧是同一个对象，因此无需移动任何内容。

```cpp
// move assignment operator
MyArray& MyArray::operator=(MyArray&& right) noexcept {
    std::cout << "MyArray move assignment operator\n";

    if (this != &right) { // avoid self-assignment
        // move right's data into this MyArray
        m_size = std::exchange(right.m_size, 0); // indicate right is empty
        m_ptr = std::move(right.m_ptr);
    }

    return *this; // enables x = y = z, for example
}
```

如果不是自赋值，第64–65行：

- 通过调用 `exchange` 将 `right.m_size` 移动到目标 MyArray 的 `m_size` 中——这会将 `right.m_size` 设置为 0 并返回其原值，我们用该值设置目标 MyArray 的 `m_size` 成员，并且
- 将 `right.m_ptr` 移动到目标 MyArray 的 `m_ptr` 中。

与移动构造函数中一样，当 `unique_ptr` 被移动赋值时，其动态内存的所有权转移到新的 `unique_ptr`，移动赋值运算符将原 `unique_ptr` 设置为 `nullptr`。无论这是否为自赋值，成员函数都返回当前对象（`*this`），从而支持级联的 MyArray 赋值，例如 `x = y = z`。

## 移动操作应为 noexcept

移动构造函数和移动赋值运算符绝不应抛出异常。它们不获取任何新资源——只是移动现有资源。因此，C++ Core Guidelines 建议将移动构造函数和移动赋值运算符声明为 `noexcept`。<sup>26</sup> 这也是能够将类的移动能力与标准库容器（如 vector）一起使用的要求。

26. C++ Core Guidelines，“C.66：使移动操作 noexcept。”访问日期：2023年4月18日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#rc-move-noexcept。

## 检查点

1. **（填空）** 一个声明为 ________ 的函数不抛出任何异常，也不调用任何会抛出异常的函数。一个声明为 ________ 的函数表示程序员已经考虑过该函数是否可能抛出异常，并决定它可能会。

   **答案：** `noexcept`、`noexcept(false)`。

2. **（填空）** `unique_ptr` 的移动构造函数将源 `unique_ptr` 的动态内存所有权转移给目标 `unique_ptr`，并将源 `unique_ptr` 设置为 ________。

   **答案：** `nullptr`。

3. *(代码)* 如何为名为 `value` 的函数参数声明类型为 `std::string` 的**右值**引用？

   **答案：** `std::string&& value`。

## 11.6.8 析构函数

图11.4第27行

```cpp
~MyArray(); // destructor
```

声明类的析构函数（定义在第73–75行），当 MyArray 对象超出作用域时调用。这将自动调用 `m_ptr` 的析构函数，释放 MyArray 对象构造时创建的动态分配 int 数组。C++ Core Guidelines 指出，析构函数抛出异常是糟糕的设计。因此，建议将析构函数声明为 `noexcept`。<sup>27</sup> 然而，除非你的类派生自析构函数声明为 `noexcept(false)` 的基类，否则编译器默认隐式将析构函数声明为 `noexcept`。

27. C++ Core Guidelines，“C.37：使析构函数 noexcept。”访问日期：2023年4月18日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-dtor-noexcept。

```cpp
// destructor: This could be compiler-generated. We included it here so
// we could output when each MyArray is destroyed.
MyArray::~MyArray() {
    std::cout << "MyArray destructor\n";
}
```

## 11.6.9 toString 和 size 函数

图11.4第29行

```cpp
size_t size() const noexcept { return m_size; } // return size
```

定义一个内联 `size` 成员函数，返回 MyArray 的元素个数。

图11.4第30行

```cpp
std::string toString() const; // create string representation
```

声明一个 `toString` 成员函数（定义在第78–91行），返回 MyArray 内容的字符串表示。函数 `toString` 使用 `ostringstream`（第8.17节介绍）构建一个字符串，其中包含用花括号（{}）括起来的 MyArray 元素值，并用逗号和空格分隔每个项。

