

-   push_back(): 在序列的末尾（后部）添加一个新元素。这些元素可以这样声明：

点击此处查看代码图片

```cpp
class Vector {
public:
  Vector();                          // 默认初始化为“空”，即没有元素
  Vector(std::initializer_list<double> l); // 使用 double 列表初始化
  void push_back(double d);          // 在末尾添加元素，大小增大 1
  // ...
};
```

`push_back()` 用于输入任意数量的元素。例如：

点击此处查看代码图片

```cpp
Vector read(istream& is) {
  Vector v;
  for (double d = 0; is >> d;) { // 将浮点值读入 d
    v.push_back(d);               // 将 d 添加到 v 中
  }
  return v;
}
```

输入循环由文件结束符（EOF）或格式单元终止。在此之前，每个数字都会被添加到末尾，`v` 的大小等于读取的元素数量。我们使用 `for` 语句而不是传统的 `while` 语句，是为了将 `d` 的作用域限制在循环内。

从 `read` 返回可能的大量数据可能是昂贵的。确保返回一个 `Vector` 是廉价的方法是使用构造函数（$6.2.2）：

点击此处查看代码图片

```cpp
Vector v = read(cin); // 这里没有 Vector 元素的拷贝
```

`std::vector` 如何高效地执行 `push_back()` 以及其他改变 vector 大小的操作，见第 $12.2 节。

用于定义初始化列表的 `std::initializer_list` 是一种编译器已知的标准库类型：当我们使用 `{1,2,3,4}` 时，编译器会创建一个 `initializer_list` 类型的对象并传递给程序。我们可以这样写：

点击此处查看代码图片

```cpp
Vector v = {1, 2, 3, 4, 5};          // v 有 5 个元素
Vector v2 = {1, 2.3, 3.45, 6.7, 8};      // v2 有 4 个元素（被截断）
```

`Vector` 的初始化列表构造函数必须这样定义：

点击此处查看代码图片

```cpp
Vector::Vector(std::initializer_list<double> l) // 使用列表初始化
  :elem(new double[l.size()]), sz(static_cast<int>(l.size())) {
    copy(l.begin(), l.end(), elem); // 从列表拷贝到 elem ($13.5)
}
```

遗憾的是，标准库无无符号表示大小和下标，因此我们需要使用丑陋的 `static_cast` 来显式将列表的大小转换为 `int`。这种做法是吹毛求节的，因为手写列表中元素数量超过最大整数（16 位整数为 32,767，32 位整数为 2,147,483,647）的情况其实很少。然而，类型系统并没有常识。它只知道变量的可能值，而不是实际值，因此在没有发生实际违规时它也可能会报错。此类警告偶尔可以帮助程序员避免严重的错误。

`static_cast` 不检查它所正在转换的值；程序员被信任会正确使用它。这并不总是一个好的假设，所以如果你有怀疑，请进行检查。应避免显式转换（通常称为强制类型转换，以提醒你正在处理某些坏掉的东西）。尝试在系统的最底层使用未检查的转换，但它们很容易出错。

其他情况包括 `reinterpret_cast` 和 `bit_cast`（§16.7），用于将对象视为简单的字节序列；以及 `const_cast` 用于“去掉 `const`”。对类型系统的审慎使用和良好的库可以在高层软件中消除未检查的转换。

## 5.3 抽象类型

如 `complex` 和 `Vector` 等类型被称为*具体*类型，因为它们的表示形式是定义的一部分。在这方面，它们类似于内置类型。相比之下，*抽象类型*是一种与实现细节隔离的类型。为了实现这一点，我们将接口与表示分离，并放弃局部变量。由于我们不知道抽象类型的表示形式（甚至是其大小，$5.2.2），并且通过引用或指针（§1.7, §15.2.1）访问它们，我们必须在存储中为我们的 Vector 分配：

首先，我们定义一个 `Container` 类，将其设计为更抽象的接口。

点击此处查看代码图片

```cpp
class Container {
public:
    virtual double& operator[](int) = 0; // 纯虚函数
    virtual int size() const = 0;      // const 成员函数 (§5.2.1)
    virtual ~Container()               // 析构函数 (§5.2.2)
};
```

该类是某些数据的纯接口。`virtual` 意味着“可以在虚类中重定义”。派自 `Container` 的类提供了 `Container` 接口的实现。奇异的 `=0` 语法表示该函数是*纯虚*的，也就是说，派自 `Container` 的类必须定义该函数。那么，无法定义一个纯 `Container` 对象。例如：

点击此处查看代码图片

```cpp
Container c;
Container* p = new Vector_container(10); // 错误：没有抽象类型的对象
```

`Vector_container` 是 `Container` 的具体实现。

```cpp
class Vector_container : public Container {
public:
    Vector_container(int n) : v(n) {}
    ~Vector_container() {}
    double& operator[](int i) override { return v[i]; }
    int size() const override { return v.size(); }
private:
    vector<double> v;
};
```

