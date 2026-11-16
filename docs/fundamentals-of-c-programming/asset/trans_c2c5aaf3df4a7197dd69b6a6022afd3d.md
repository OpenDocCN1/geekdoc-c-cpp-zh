

## 18.6. 智能指针

```cpp
struct Widget {
    unsigned id;
    Widget():id(id_source++) {
        std::cout << "Creating a widget #" << id << " ("
        << reinterpret_cast<uintptr_t>(this)
        << ")\n";
    }
    ~Widget() {
        std::cout << "Destroying a widget #" << id << " ("
        << reinterpret_cast<uintptr_t>(this)
        << ")\n";
    }
};

unsigned Widget::id_source = 0;

// Global shared pointer
auto global_ptr = std::make_shared<Widget>();

std::shared_ptr<Widget> make_widget() {
    std::cout << "------ Entering make_widget ----\n";
    std::cout << "------ Leaving make_widget ----\n";
    return std::make_shared<Widget>();
}

void test1() {
    std::cout << "---- Entering Test 1 ----\n";
    // Make p point to a dynamically created widget object
    auto p = std::make_shared<Widget>();
    std::cout << p->id << " \n";
    p->id = 25;
    std::cout << p->id << " \n";
    std::cout << "---- Leaving Test 1 ----\n";
}

void test2() {
    std::cout << "---- Entering Test 2 ----\n";
    // Make q point to a dynamically created widget object
    auto q = std::make_shared<Widget>();
    std::cout << q->id << " \n";
    q = nullptr; // Make q point to nothing
    std::cout << "---- Leaving Test 2 ----\n";
}

void test3() {
    std::cout << "---- Entering Test 3 ----\n";
    // Make p point to a dynamically created integer
    auto p = std::make_shared<int>(55);
    std::cout << *p << " \n"; // Prints 55
    *p = -4; // Reassign
    std::cout << *p << " \n"; // Prints -4
    std::cout << "---- Leaving Test 3 ----\n";
}

void test4() {
    std::cout << "---- Entering Test 4 ----\n";
    static auto p = make_widget();
    std::cout << p->id << " \n";
    std::cout << "--- Leaving Test 4 ---\n";
}

void test5() {
    std::cout << "--- Entering Test 5 ---\n";
    auto p = make_widget();
    std::cout << p->id << " \n";
    std::cout << "--- Leaving Test 5 ---\n";
}

void test6() {
    std::cout << "--- Entering Test 6 ---\n";
    // Aliasing
    auto q = std::make_shared<Widget>();
    auto r = q; // r aliases q, no new memory allocated
    auto s = q; // s aliases q, no new memory allocated
    std::cout << q->id << " \n";
    std::cout << r->id << " \n";
    std::cout << s->id << " \n";
    q = nullptr;
    std::cout << r->id << " \n";
    std::cout << s->id << " \n";
    r = nullptr;
    std::cout << s->id << " \n";
    s = nullptr; // Deallocates the widget object
    std::cout << "--- Leaving Test 6 ---\n";
}

int main() {
    std::cout << "--- Entering main ---\n";
    test1();
    test2();
    test3();
    test4();
    test5();
    test6();
    std::cout << "--- Leaving main ---\n";
}
```

清单 18.21 (simplesharedptrtest.cpp) 的输出按时间顺序显示了程序何时创建和销毁 Widget 对象：

```
Creating a widget #0 (18566044)
--- Entering main ---
--- Entering Test 1 ---
Creating a widget #1 (18566092)
1
25
--- Leaving Test 1 ---
Destroying a widget #25 (18566092)
--- Entering Test 2 ---
Creating a widget #2 (18566380)
2
Destroying a widget #2 (18566380)
--- Leaving Test 2 ---
--- Entering Test 3 ---
55
-4
--- Leaving Test 3 ---
--- Entering Test 4 ---
--- Entering make_widget ---
Leaving make_widget
Creating a widget #3 (18566404)
3
--- Leaving Test 4 ---
--- Entering Test 5 ---
--- Entering make_widget ---
Leaving make_widget
Creating a widget #4 (18566092)
4
--- Leaving Test 5 ---
Destroying a widget #4 (18566092)
--- Entering Test 6 ---
Creating a widget #5 (18566092)
5 5 5
5
5
Destroying a widget #5 (18566092)
--- Leaving Test 6 ---
--- Leaving main ---
Destroying a widget #3 (18566404)
Destroying a widget #0 (18566044)
```

清单 18.21 (simplesharedptrtest.cpp) 中的 Widget 构造函数确保其创建的每个 widget 对象都有一个唯一的 id 编号。第一个 widget 的 id 为 0，第二个为 1，以此类推。

执行中的程序在调用 main 函数之前会先初始化全局对象。程序输出的前两行：

```
Creating a widget #0 (18566044)
--- Entering main ---
```

显示了全局对象 global_ptr 的创建。接下来的几行：

```
--- Entering Test 1 ---
Creating a widget #1 (18566092)
1
25
--- Leaving Test 1 ---
Destroying a widget #25 (18566092)
```

显示了 test1 函数中局部 widget #1 的创建。test1 中的代码修改了 Widget 对象的 id 值。（请回顾，客户端可以自由修改结构体的字段。）在函数执行结束时，std::shared_ptr 对象会自动销毁 widget #1，现在它被称为 widget #25，正如我们从析构函数的输出中所见。

需要注意的是，p 是 test1 中的局部变量，因此 std::shared_ptr p 本身的空间位于栈上。对 std::make_shared 的调用通过 new 在堆上创建一个 widget 对象。当 p 在 test1 执行结束时超出作用域，p 的析构函数会自动调用 delete 从堆上释放该 widget。通常的函数返回机制会自动将 p 从栈上移除。

输出的接下来几行：

```
--- Entering Test 2 ---
Creating a widget #2 (18566380)
2
Destroying a widget #2 (18566380)
--- Leaving Test 2 ---
```

这表明，当先前分配给 widget 的 std::shared_ptr 被重新赋值（在此例中为 nullptr）时，原始 widget 对象的空间会立即被释放（其析构函数被调用）；对象在函数结束前即被清理。

在输出的接下来几行中：

```
--- Entering Test 3 ---
55
-4
--- Leaving Test 3 ---
```

test3 函数并未揭示 std::shared_ptr 自动内存管理的任何线索，因为 int 类型没有构造函数或析构函数来指示动态分配的 int 值的生命周期。程序中包含 test3 函数仅是为了演示 std::shared_ptr 对象可以像管理复杂类型一样妥善管理简单类型的动态内存。简单的 int 类型在其内存被释放时不会报告其销毁，但请放心，std::shared_ptr 对象会正确释放其内存。

在输出的接下来几行中：

```
--- Entering Test 4 ---
--- Entering make_widget ---
Leaving make_widget
Creating a widget #3 (18566404)
3
--- Leaving Test 4 ---
```

我们看到了 widget #3 的创建，但未看到其销毁。这是因为这是 test4 的第一次调用。第一次调用初始化静态局部变量 p，从而构造了一个 std::shared_ptr 及其关联的 Widget 对象。由于 p 是静态局部变量，它必须在 test4 的调用之间保持存活；因此，p 无法在程序执行完毕之前被释放（见下文）。

在输出的接下来几行中：

```
--- Entering Test 5 ---
--- Entering make_widget ---
Leaving make_widget
Creating a widget #4 (18566092)
4
--- Leaving Test 5 ---
Destroying a widget #4 (18566092)
```

我们看到与 test4 完全相同的情况，只不过 p 不是静态的。这意味着 p 会在函数返回时销毁其 widget 对象。

在最后一个测试函数 test6 的输出中，我们看到

```
--- Entering Test 6 ---
Creating a widget #5 (18566092)
5 5 5
5
5
Destroying a widget #5 (18566092)
--- Leaving Test 6 ---
```

test6 函数仅分配一个 Widget 对象。它将三个 std::shared_ptr 对象分配给同一个 widget 对象。这清楚地证明了 shared_ptr 这一名称的合理性——所有三个指针共享对同一对象的访问权。如果 p 和 q 是相同类型的 std::shared_ptr，则语句

```
q = p;
```

使 p 和 q 成为同一对象的别名。无论是否存在别名，test6 中的代码都恰好分配一个 Widget 对象，并在函数执行完成时释放该同一个 Widget 对象。

程序输出的最后几行：

```
--- Leaving main ---
Destroying a widget #3 (18566404)
Destroying a widget #0 (18566044)
```

显示了 test4 的静态局部 std::shared_ptr（widget #3）和 global_ptr（widget #0）的销毁。

如果你仔细分析清单 18.21 (simplesharedptrtest.cpp) 的输出，你会发现每个构造函数调用都有针对同一对象的相应析构函数调用（请记住 test1 将 widget #1 重命名为 #25，因此请比较 widget #1 的创建地址与 widget #25 的销毁地址，你会发现它们匹配）。清单 18.21 (simplesharedptrtest.cpp) 中的所有 Widget 对象都在堆上分配空间，然而代码中既看不到 new 也看不到 delete。

正是这种在适当时候释放其引用内存的能力，使得 std::shared_ptr 对象成为智能指针。

请回顾演示手动管理动态内存困难的清单 18.1 (howtodelete.cpp)。清单 18.22 (smartdelete.cpp) 将清单 18.1 (howtodelete.cpp) 中 get_widget 函数返回值的原始指针转换为 std::shared_ptr。结果如何？我们不再需要担心谁“拥有”堆上分配对象的内存；std::shared_ptr 对象管理所有这些细节。不需要 delete。

## 清单 18.22: smartdelete.cpp

```cpp
#include <iostream>
#include <memory>

struct Widget {
    int value;
    Widget(int value): value(value) {
        std::cout << "Creating widget " << value << '\n';
```

