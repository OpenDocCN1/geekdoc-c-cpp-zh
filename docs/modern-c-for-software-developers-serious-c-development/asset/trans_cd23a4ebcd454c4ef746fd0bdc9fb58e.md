

增强我们的智能指针类，使其能够转换为 `bool` 类型。这样我们就可以像原始指针一样在 `if` 语句中使用它：

```
if (sp) {
    statements
}
```

`sp` 用于测试底层原始指针是否为空。

对于上面的示例，请考虑以下关于两个智能指针类的程序片段：

```
smart_pointer<int> sp1(p)
smart_pointer<int> sp2(q)
sp1 = sp2
```

这会导致未定义行为，因为赋值操作将调用 `sp1` 的默认拷贝赋值运算符，导致我们得到两个都使用相同内存位置的对象。我们还可能会两次删除分配的内存。此外，这次赋值将导致 `sp1` 初始分配的内存丢失。这表明我们的智能指针类需要进一步完善，以处理拷贝初始化、拷贝赋值以及其他原始指针特性。

## 智能指针类型

回到之前的示例，必须对智能指针如何被拷贝做出决定。否则，将使用默认拷贝构造函数，从而产生未定义行为。

标准库为该问题提供了解决方案，这引向了不同智能指针类的规范。每个指针类都反映了一个设计决策。

## std::unique_ptr

`std::unique_ptr` 类语义表示它是所封装内存的唯一所有者。`std::unique_ptr` 对象持有一个原始指针，并在析构函数中删除它。

考虑一个 `makeASandwich()` 函数：

```
#include <memory>

Sandwich* ptr = makeASandwich()
std::unique_ptr<Sandwich> sp(makeASandwich());
```

`makeASandwich` 为 `Sandwich` 分配内存并返回指向分配内存的指针。`sp` 是一个智能指针对象，它封装了一个名为 `sp` 的 `std::unique_ptr` 对象于原始的 Sandwich 指针。我们拥有该智能指针的所有权，除了我们之外没人可以删除或使用该对象。我们拥有智能指针的所有权，可以安全地修改指向的 `Sandwich` 对象，而不必担心其他人可能持有该指针或修改了对象。

`std::unique_ptr` 指针是多态的，可以指向派生对象。

`unique_ptr` 对象有两种类型：一种用于标量，另一种用于数组：

- `unique_ptr<Foo>` 封装指向类型 `Foo` 对象的指针。
- `unique_ptr<Foo[]>` 封装指向 `Foo` 对象数组的指针。

以下示例显示了如何创建 `std::unique_ptr` 对象。在这些示例中，`sp1`、`sp2` 和 `sp3` 是智能指针对象：

- `std::unique_ptr<double> sp1(new double(3.14));`
- `std::unique_ptr<double[]> sp2(new double[50]);`
- `std::unique_ptr<Foo> sp3(new Foo)`

第二个声明创建 `std::unique_ptr` 对象，它封装了一个指向包含五十个 double 的数组的原始指针。

这是一个用法示例：

```
#include <iostream>
#include <memory>
int main() {
    std::unique_ptr<double[]> sp(new double[5] {1,2,3,4,5});
    int i = 1;

    // 获取原始指针
    auto ptr = sp.get();
    for (int ctr = 0; ctr < 4; ctr++) {
        *ptr = 2 * i;
        i++;
        ptr++;
    }

    ptr = sp.get();
    for (int ctr = 0; ctr < 4; ctr++) {
        std::cout << *ptr << " ";
        ptr++;
    }

    // 输出
2 4 6 8 10
```

注意 `sp.get()` 返回了智能指针对象封装的原始指针。

`std::unique_ptr` 对象是其封装的分配内存的所有者。如果智能指针对象在未传递所有权的情况下超出作用域，则该对象会被删除，其指向的内会在析构函数中释放。

`std::unique_ptr` 在任何时候只有一个所有者。我们不能简单地拷贝 `std::unique_ptr`：

```
std::unique_ptr<int> p(new int(5));
std::unique_ptr<int> q;

q = p; // 编译错误
```

这是另一个示例：

```cpp
#include <iostream>
#include <memory>
void borrower1(std::unique_ptr<double[]> sp)
{
  std::cout << "in borrower1. memory address of pointer to " << sp;
  std::cout << std::endl;
}
void borrower2(std::unique_ptr<double[]> &sp)
{
  std::cout << "in borrower2. memory address of reference to " << sp;
  std::cout << std::endl;
}
void memory_address()
{
  // sp 被创建并拥有包含 42 个 double 的内存
  std::unique_ptr<double[]> sp(new double[42]);

  std::cout << "address of created sp = " << &sp << std::endl;

  borrower1(sp);
  borrower2(sp);
}
```

```cpp
int main()
{
    memory_address();
}

// 输出
address of created sp = [address]
in borrower1. memory address of pointer to [address]
in borrower2. memory address of reference to [address]
```

## 移动 unique_ptr

如果所有者想要将其所有权交给另一个变量，必须使用 `std::move`。

```cpp
#include <iostream>
#include <memory>
#include <utility>

void calc(std::unique_ptr<double[]>&& x)
{
    std::cout << "in calc: " << x << std::endl;
}

int main()
{
    // sp 被创建并拥有包含 42 个 double 的内存
    std::unique_ptr<double[]> sp(new double[42]);

    std::cout << "address of created sp = " << &sp << std::endl;

    // 将所有权移动到 q
    std::unique_ptr<double[]> q = std::move(sp);

    // 将 q 传递给 calc
    calc(std::move(q));

    return 0;
}

// 输出
address of created sp = [address]
in calc: [address]
```

## 删除 unique_ptr

当 `unique_ptr` 对象超出作用域时，它的析构函数会自动删除它封装的内存。

```cpp
#include <iostream>
#include <memory>

int main()
{
    std::unique_ptr<int> p(new int(10));
    // p 在此处被删除
    return 0;
}
```

## 释放为原始指针

`unique_ptr` 也可以 `release()` 方法释放原始指针。

```cpp
#include <iostream>
#include <memory>

int main()
{
    std::unique_ptr<int[]> sp(new int[10]);
    int* ptr = sp.release();
    // sp 不再拥有内存，我们必须手动删除
    delete[] ptr;
    return 0;
}
```

## std::shared_ptr

单个内存资源可以被多个 `shared_ptr` 对象共享。应用程序维护一个资源使用次数的内部计数。

当创建一个新的 `shared_ptr` 对象时，它的构造函数会将与共享数据相关的引用计数加 1。当 `shared_ptr` 超出作用域时，它的析构函数会将共享资源的引用计数减 1。如果引用计数变为 0，意味着没有 `shared_ptr` 对象在使用该内存，内存会被删除。

## 共享内存指针

以下是 `shared_ptr` 的用法示例：

```cpp
#include <iostream>
#include <string>
#include <memory>

void shared_user(std::string s, std::shared_ptr<double[]>& x) {
    std::cout << "share taken by: " << s;
    std::cout << " reference count: " << x.use_count() << std::endl;
}

void share_memory() {
    // 创建共享指针，它指向
    // 包含 42 个数字的连续内存块
    // 引用计数自动分配内存

    std::shared_ptr<double[]> sp(new double[42]);

    // 共享 sp
    shared_user("user 1", sp);

    std::shared_ptr<double[]> q = sp;
    shared_user("user 2", q);

    // 再次共享 sp
    std::shared_ptr<double[]> r = sp;
    shared_user("user 3", r);
}

int main()
{
    share_memory();
}

// 输出
share taken by: user 1 reference count: 1
share taken by: user 2 reference count: 2
share taken by: user 3 reference count: 3
```

## 创建共享内存指针

以下示例通过构造函数创建共享内存指针：

```cpp
#include <memory>
#include <utility>

std::shared_ptr<double> p1(new double(1.5));
```

以下示例调用拷贝构造函数来创建一个新的共享内存指针对象：

