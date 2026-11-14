

void start_solve(const VectorB& b, VectorX& x,
             Iteration& iter) const
{
    my_iter.set_iter(iter);
    my_thread = std::thread(
        [this, &b, &x]() {
            my_solver.solve(b, x, my_iter);
        }
    );
}
int wait() {
    my_thread.join();
    return my_iter.error_code();
}
int interrupt() {
    my_iter.interrupt();
    return wait();
}
bool finished() const { return my_iter.iter.finished(); }
private:
    Solver my_solver;
    mutable interruptible_iteration my_iter;
    mutable std::thread my_thread;
};

启动求解器使用 `async_executor` 后，我们可以去做其他事情，并不时检查求解器是否 `finished()`。如果意识到结果已变得无关紧要，可以 `interrupt()` 执行。无论是完整求解还是中断执行，都必须 `wait()`，直到 `thread` 通过 `join` 正常结束。

以下伪代码展示了科学家如何使用这种异步执行：

点击此处查看代码图片

```
while (happy(science_foundation)) {
    discretize_model();
    auto my_solver = itl::make_cg_solver(A, PC);
    itl::async_executor async_exec(my_solver);
    async_exec.start_solve(b, x, iter);

    play_with_model();
    if (found_better_model) {
        async_exec.interrupt();
    }
    else
        async_exec.wait();
}
```

工程版本中，将 `science_foundation` 替换为 `client`。

我们也可以将异步求解器用于数值上具有挑战性的系统，且事先不知道哪个求解器可能会收敛。为此，我们会并行启动所有有望成功的求解器，等待其中一个完成，并中断其他求解器。为清晰起见，我们应将执行器存储在容器中。特别是当执行器既不可复制也不可移动时，可以使用第 4.1.3.2 节中的容器。

## 4.6.7 可变参数互斥锁

在多线程应用中，当许多线程等待被锁定的互斥量时，性能会显著下降。当我们为大型数据结构提供多个互斥量（每个互斥量负责一部分数据）时，可以减少这种拥堵。这样，线程只有在另一个线程访问同一部分数据时才需要等待。

我们不会展示这样的实现，而是探讨另一个挑战。除了仅局部访问数据的操作外，可能还有考虑整个数据结构的操作，例如以复杂方式重组数据时。此时我们必须 `lock` 所有互斥量。如果按顺序进行，我们可能会陷入 _死锁_，即程序永久停滞的状态，因为多个线程在等待永远不会再次可用的资源（这些资源被其他也在等待的线程占据，形成某种循环依赖）。这是一门独立的学科，我们不会深入探讨。有巧妙的约定可以防止死锁，但这也不是我们的主题。

我们的解决方法是同时锁定所有互斥量——或者等待直到它们可以一次性全部锁定。我们假设大型数据结构的所有锁都存储在一个 `array` 中。当这些数组始终具有相同大小（例如 4）时，可以直接用所有元素调用可变参数 `lock` 函数：

```
lock(m[0], m[1], m[2], m[3]);
```

但我们希望更通用地思考，并能够处理任意大小的数组。我们的实现也应遵循 RAII 原则，

即，类似于 `lock_guard`，但针对数组：

```cpp
template <std::size_t N>
class array_lock_guard
{
public:
    array_lock_guard(std::array<std::mutex, N>& mutexes)
        : mutexes(mutexes)
    {
        // lock them all
    }

    ~array_lock_guard()
    {
        for (auto& m : mutexes)
            m.unlock();
    }

private:
    std::array<std::mutex, N>& mutexes;
};
```

我们的类必须在构造函数中锁定所有互斥量，在析构函数中解锁。后者并不关键：我们可以按顺序进行。锁定必须在一次调用中完成：

```cpp
template <std::size_t... I>
void lock_all(std::index_sequence<I...>)
{
    std::lock(mutexes[I]...);
}

array_lock_guard(std::array<std::mutex, N>& mutexes)
    : mutexes(mutexes)
{
    lock_all(std::make_index_sequence<N>());
}
```

我们在此使用了 `index_sequence` 并将其传递给第二个函数，该函数用它实例化了可变模板参数，其在可变表达式中的展开最终锁定了所有互斥量。为完整起见，我们应提到 C++17 引入了 `scoped_lock`，另一种 RAII 风格的互斥量管理器，允许锁定和解锁任意数量的互斥量（甚至不同类型的互斥量）。

## 4.6.8 协程

[C++20] 协程是可以被挂起并稍后恢复执行的函数，仿佛从未中断过。这为并发编程提供了新机遇：由于缺少资源而无法继续的函数不再有义务等待该资源；相反，它可以挂起，即将控制权返回给调用者，由调用者在资源可用时恢复该函数。许多事件驱动的异步系统正是以这种方式实现的。

=> c++20/coroutine-generator.cpp

协程的另一种不一定是并发的应用是生成：一个执行某些计算或遍历数据结构的函数，每当有新值可供调用者使用时，函数就会挂起并提供该值。调用者对该值执行操作，然后恢复生成器。假设我们有一个存储 int 值的树，希望按中序打印：

点击此处查看代码图片

```
tree t;
fill_tree(t);

for (auto i : traverse(t, inorder))
    cout << i << endl;
```

我们的生成器函数 traverse 应递归下降到子树，并按正确顺序提供所有值。为此，节点的值应在从左子树返回后、在下降到右子树之前提供：

点击此处查看代码图片

```
struct preorder_t {} const preorder;
struct inorder_t {} const inorder;
struct postorder_t {} const postorder; // extra traversal

template <typename Order>
```

```cpp
generator<int> traverse(const tree& t, Order)
{
    stack<tree_entry*> s;
    tree_entry* current = t.head.get();

    while (current != nullptr || !s.empty()) {
        while (current != nullptr) {
            if constexpr (is_same_v<Order, preorder_t>)
                co_yield current->value;
            s.push(current);
            current = current->left.get();
        }

        current = s.top(); s.pop();
        if constexpr (is_same_v<Order, inorder_t>)
            co_yield current->value;
        current = current->right.get();
    }
}
```

在下降到两个子树之前/之后返回值称为先序/后序。后者的实现相当不同，因此我们将其放在单独的函数中，你可以在源代码中找到。

C++ 中的协程是 *无栈* 的，即它们在挂起时不存储栈的状态。因此，它们不能递归使用，我们需要通过为数据实现栈来手动处理递归。协程在挂起时存储的是局部变量、寄存器和函数参数；实际上是恢复执行所需的一切内容。

协程可以使用 `co_await` 和 `co_yield` 挂起。前者仅挂起，而后者还返回一个值。要在返回值的同时终止协程，可以使用 `co_return`。这些是 C++20 中的三个新关键字。

协程的返回类型必须是所谓的 *Promise*，不应与类模板 `std::promise` 混淆。Promise 处理协程的恢复。我们的 `generator` 类型取自 Kenny Kerr 的教程 [42]，超过 100 行长。虽然协程专家肯定会拥抱其自身 Promise 实现中的精细控制粒度，但该领域的新手程序员可能更偏好简单。幸运的是，标准的 `generator` 实现即将推出，并希望在 C++23 中可用。

