

## 图 18.1 内存泄漏

- 1. 在调用 calc 之前，变量 p 不存在

- 2. 在 calc 执行期间，变量 p 是活跃的，并指向动态分配的内存

![](img/e84ad11adb18201d71595b31ce6c9eff_556_0.png)

- 3. calc 返回后，变量 p 消失，但代表其分配的内存仍然存在

![](img/e84ad11adb18201d71595b31ce6c9eff_556_1.png)

```
// Do some stuff
// ...
int *p = new int[n];
// ...
// Do some stuff with p
// ...
// Exit function without deleting p's memory
}
```

如果程序足够多次地调用函数 calc，程序最终将耗尽内存。图 18.1 显示了当局部指针在函数执行结束时超出作用域时，内存是如何被搁置的。

在 calc 函数中，p 是一个局部变量。因此，p 位于栈上。当某次对 calc 的调用完成时，函数的清理代码会自动释放变量 p 所占用的空间。这是因为所有函数都会自动管理其参数和局部变量的内存。问题是，p 是通过 new 赋值的，指向从堆中分配的内存，而不是栈。函数执行只管理栈内存。当函数执行完成时，p 消失了，p 所指向的内存不会自动释放。更糟糕的是，局部变量 p 曾经引用的堆内存现在无法访问，因为没有其他仍然有效的变量知道它。

编写正确的 calc 函数在这种情况下有两种选择：

- 1. 在返回之前使用 delete 释放 p 分配的内存，

- 2. 将 p 返回给调用函数的调用者，并让调用者在使用完 calc 创建的对象时调用 delete。

选项 1 是最简单的解决方案。`calc` 函数需要一个动态分配的数组，创建它，使用它，然后在返回之前释放它。在这个单个函数定义中，我们可以看到一个 `new` 和后来对应的 `delete`——一个完美的匹配对。不幸的是，这并不是常见的情况。

选项 2 是更常见的情况。来自堆的动态内存分配使得正在执行的程序可以在运行时添加额外数据，这些数据在函数调用之间持续存在。理论上，这个过程很简单：

- 1. 需要 `calc` 函数所能提供的东西的代码将调用 `calc` 以获取一个动态分配的对象，并且

- 2. 在使用完它时 `delete` 该对象。

这里的问题是，我们看不到与 `delete` 配对的 `new`。`new` 隐藏在 `calc` 中，调用者必须执行 `delete`。调用代码的程序员必须自律，并记住适当地使用 `delete`。

- `delete` 运算符绝不应该用于释放之前通过 `new` 调用分配的内存。此代码片段说明了一个这样的示例：

```
int list[10], *p = list; // p points to list
// ...
// Do some stuff
// ...
delete [] p; // Logic error, attempt to deallocate p's memory
```

指针 `p` 引用的空间不是由 `new` 分配的，因此不应使用 `delete` 来尝试释放其内存。

尝试 `delete` 未使用 `new` 分配的内存会导致未定义行为，并代表一个逻辑错误。

- `delete` 不得用于多次释放同一内存。当两个指针引用同一内存时，可能会发生这种情况。这样的指针称为 *别名*。以下代码片段说明了这种情况：

```
int *p = new int[10], *q = p; // q aliases p
// ...
// Do some stuff with p and/or q
// ...
delete [] p; // Free up p's memory
// ...
// Do some other stuff
// ...
delete [] q; // Logic error, q's memory already freed!
```

由于指针 `p` 和指针 `q` 指向同一内存，它们互为别名。释放其中一个引用的内存，另一个的内存也会被释放，因为是同一内存。

对同一内存多次 `delete` 会导致未定义行为，并代表一个逻辑错误。

- 绝不要尝试访问之前通过 `delete` 释放的内存。尝试访问已删除的内存会导致未定义行为，并代表一个逻辑错误。代码片段

```
int *list = new int[10];
// ...
// Use list, then
// ...
delete [] list; // Deallocate list's memory
// ...
// Sometime later
// ...
int x = list[2]; // Logic error, but sometimes works!
```

说明了如何发生这种情况。出于效率原因，许多实现中的 delete 运算符将堆空间标记为“可用”，而不修改该内存的内容。粗心的程序员可能会无意中使用已删除指针的内存，仿佛它仍然有效。当释放的内存最终通过对 new 的调用在其他地方重新分配时，问题就会显现出来。结果是程序似乎“工作”一段时间，然后在不可预测的时间神秘失败。调试这种情况可能非常困难。问题通常是因为别名造成的：

```
int *list = new int[10];
// ...
int *arr = list; // arr aliases list
// ...
delete [] list; // Deallocate list's memory
// ...
// Sometime later
// ...
int x = arr[2]; // Same problem!
```

我们声明了 list 的内存，而不是 arr 的内存，不是吗？不，因为 arr 是 list 的别名，arr 引用了之前用 delete 释放的内存。

别名是一个问题，因为我们对变量的概念。当我们有两个名称不同的变量时，自然会认为它们代表两个不同的对象。这被称为值语义。指针和引用引入了别名的可能性：它们使用引用语义。引用语义使得诸如按引用调用和遍历动态数据结构（如链表）等有用技术成为可能，但使用引用语义推理对象的身份需要额外的谨慎。

确保每个 new 都有且只有一个对应的 delete 似乎很简单，但在实践中，确定确切何时使用 delete 可能非常困难。例如，假设你从函数调用中获得一个动态分配的对象，如下所示：

```
Widget *p = get_widget();
```

很有可能 get_widget 函数通过 new 分配一个 Widget 对象，并简单地返回指向该对象的指针。在这种情况下，我们可以使用

```
delete p;
```

在我们使用完 p 指向的对象时。但是，如果 get_widget 函数正在管理在其他地方创建的某个资源；也就是说，get_widget 返回指向它不创建的对象的指针，会怎样？清单 18.1 (howtodelete.cpp) 提供了一个初步示例。

## 清单 18.1: howtodelete.cpp

```
#include <iostream>

struct Widget {
    int value;
    Widget(int value): value(value) {
        std::cout << "Creating widget " << value << '\n';
    }
    ~Widget() {
        std::cout << "Destroying widget " << value << '\n';
    }
};

Widget global_w(5);

Widget *get_widget1() {
    // Caller must deallocate the returned object
    Widget *w = new Widget(10); // Allocation each call
    return w;
}

Widget *get_widget2() {
    // Caller must NOT deallocate the returned object
    // as it points to a global variable not dynamically
    // allocated
    return &global_w; // No allocation
}

void process() {
    Widget *p1 = get_widget1();
    std::cout << "p1->value = " << p1->value << '\n';
    Widget *p2 = get_widget2();
    std::cout << "p2->value = " << p2->value << '\n';
    delete p1; // Must delete p1
    delete p2; // But do not delete p2!
}

int main() {
    std::cout << "Entering main\n";
    process();
    std::cout << "Leaving main\n";
}
```

清单 18.1 (howtodelete.cpp) 中 process 函数的作者正确地假设，get_widget1 函数返回一个动态分配的对象，调用者（在此例中为 process）最终必须释放它。语句

```
delete p1;
```

正确地释放了 get_widget1 创建的对象。process 函数的作者还错误地假设，get_widget2 函数返回一个动态分配的对象，调用者最终必须释放它。不想冒内存泄漏的风险，process 作者添加了语句

```
delete p2;
```

