
# 迭代器与索引

既然你可以编写一个使用简单变量和 `size()` 方法的循环来遍历 `vector` 的元素，为什么要费力使用迭代器呢？这是一个有效的问题，有三个答案：

- 迭代器允许你在容器的任何位置插入和删除元素。请参见下方的“添加和删除元素”章节。
- 迭代器允许你使用 STL 算法，算法将在第 17 章讨论。
- 使用迭代器顺序访问每个元素比通过索引访问每个元素更高效。这种结论对于 `vector` 不成立，但适用于 `list`、`map` 和 `set`。

# 添加和删除元素

正如你已经读过的，可以使用 `push_back()` 方法向 `vector` 末尾添加元素。`vector` 提供了一个对应的方法 `pop_back()`。

> 警告：`pop_back()` 不返回它移除的元素。如果你需要该元素，必须先通过 `back()` 获取它。

你还可以使用 `insert()` 方法在 `vector` 的任何位置插入元素，它会在迭代器指定的位置添加一个或多个元素，并将所有后续元素向下移动以为新元素腾出空间。`insert()` 有五种不同的重载形式，可以：

- 插入单个元素。
- 插入 `n` 个单个元素的拷贝。
- 从迭代器范围插入元素。记住，迭代器范围是半开的，即它包含起始迭代器所指向的元素，但不包含结束迭代器所指向的元素。
- 使用移动语义（move semantics）将给定元素移动到 `vector` 中插入单个元素。
- 将元素列表插入 `vector` 中，其中元素列表以 `initializer_list` 的形式给出。

> 注意：`push_back()` 和 `insert()` 有某些版本接受左值（lvalue）或右值（rvalue）作为参数。左值版本根据需要分配内存来存储新元素，并存储元素参数的拷贝。右值版本则使用移动语义将对象的所有权移动到 `vector`，而不是拷贝对象。

你可以使用 `erase()` 移除 `vector` 中的任意位置，并使用 `clear()` 所有元素。`erase()` 有两种形式：一种接受单个迭代器以删除单个元素，另一种则接受两个迭代器以指定要删除的元素范围。

如果你想删除满足特定条件的元素，一种解决方案是编写一个循环遍历所有元素，并删除每个符合条件的元素。然而，这种二次复杂度可以通过使用“删除-擦惯式”（remove-erase-idiom）来避免，该惯式具有线性复杂度。删除-擦惯式将在第 17 章中讨论。

- `insert(const_iterator pos, const T& x)`: 属性 `x` 将被插入到位置 `pos` 处。
- `insert(const_iterator pos, size_type n, const T& x)`: 值 `x` 将在位置 `pos` 处插入 `n` 次。
- `insert(const_iterator pos, InputIterator first, InputIterator last)`: 范围 `first last` 内的元素将被插入到位置 `pos` 处。

```cpp
vector<int> vectorOne = { 1, 2, 3, 5 };

vector<int> vectorTwo;

// 哎，我们忘记添加 4 了。将其插入到正确的位置

vectorOne.insert(cbegin(vectorOne) + 3, 4);

// 将元素 6 到 10 添加到 vectorTwo

for (int i = 6; i <= 10; i++) {
    vectorTwo.push_back(i);
}

printVector(vectorOne);
printVector(vectorTwo);

// 将 vectorTwo 的所有元素添加到 vectorOne 的末尾

vectorOne.insert(cend(vectorOne), cbegin(vectorTwo), cend(vectorTwo));

printVector(vectorOne);

// 删除 vectorOne 中的数字 2 到 5
```

```cpp
vectorOne.erase(cbegin(vectorOne) + 1, cbegin(vectorOne) + 5);

printVector(vectorOne);

// 完全清空 vectorTwo

vectorTwo.clear();

// 添加 10 个值 100 的拷贝

vectorTwo.insert(cbegin(vectorTwo), 10, 100);

// 决定我们只需要 9 个元素

vectorTwo.pop_back();

printVector(vectorTwo);
```

程序的输出如下：

+ 1 2 3 4 5
6 7 8 9 10
1 2 3 4 5 6 7 8 9 10
1 6 7 8 9 10
100 100 100 100 100 100 100 100 100

记住，迭代器表示半开范围，且 `insert()` 在迭代器位置所指向的元素之前添加元素。因此，你可以将 `vectorTwo` 的全部内容插入 `vectorOne` 的末尾，如下：

```cpp
vectorOne.insert(cend(vectorOne), cbegin(vectorTwo), cend(vectorTwo));
```

> 警告：接受 `vector` 范围作为参数的方法（如 `insert()` 和 `erase()`）假设起始和结束迭代器指向同一个容器中的元素，且结束迭代器指向起始器之后的元素。如果不满足这些条件，这些方法将无法正常工作！

## 移动语义

所有 STL 容器都通过包含移动构造函数和移动赋值运算符来实现移动语义。这些使用了第 10 章描述的右值引用。这的一个巨大优势是，你可以从函数返回 STL 容器而不会产生性能下降。看以下示例：

```cpp
vector<int> createVectorOfSize(size_t size)
{
  vector<int> vec(size);
  int contents = 0;
  for (auto& i : vec) {
    i = contents++;
  }
  return vec;
}

...
vector<int> myVector;
myVector = createVectorOfSize(123);
```

没有移动语义的情况下，`createVectorOfSize` 会创建一个局部 `vector`。返回语句会拷贝 `vec`，将其从函数返回，并赋值给 `myVector`。在 STL 容器语义支持下，避免了 `vector` 的拷贝。相反，返回语句移动了 `vector`。在这种情况下，移动是可能的，因为 `vec` 将超出范围。

同样，`push` 操作也可以使用移动语义在某些情况下提高性能。例如，假设你有一个 `Element` 类型元素的 `vector`，如下：

```cpp
class Element {
public:
    Element(int i, const string& str) : mI(i), mStr(str) {}
private:
    int mI;
    string mStr;
};

vector<Element> vec;
```

## 大小与容量

`vector` 提供了两种获取其大小信息的方法：`size()` 和 `capacity()`。`size()` 方法返回 `vector` 中的元素数量，而 `capacity()` 返回它在不重新分配内存的情况下可以容纳的元素数量。因此，你可以在不引起重新分配的情况下插入的元素数量为 `capacity() - size()`。

> 注意 你可以使用 `empty()` 方法查询 `vector` 是否为空。`vector` 可以为空，但具有非零的容量。

## 预留容量

如果你不在乎效率或迭代器失效问题，那么完全没有需要控制 `vector` 的内存分配。但是，如果你想让程序运行尽可能高效，或者保证迭代器不会失效，你可以强制 `vector` 预分配足够的空间来容纳所有所有元素。当然，你需要知道它将包含多少个元素，而这有时是无法预测的。

预留空间的一种方法是调用 `reserve()`，它会分配足够的内存来容纳指定数量的元素。下一节将展示 `reserve()` 方法的用法示例。

> 警告 为元素预留空间会改变容量，但不会改变大小。也就是说，它并不会实际创建元素。不要访问超过 `vector` 大小的范围。

预留空间的另一种方法是在构造函数或使用 `resize()` 方法中指定你希望 `vector` 存储的元素数量。这种方法实际上会创建一个具有该大小（以及可能具有该容量）的 `vector`。

## vector 示例：轮询类

计算机科学中的一个常见问题是在有限资源列表之间分配请求。例如，一个简单的操作系统可以维护一个进程列表，并为每个进程分配一个时间片（例如 100ms）来执行其某些任务。时间片结束后，操作系统会挂起当前进程，并给队列中的下一个进程分配时间片来执行它的某些任务。解决这个问题最简单的算法之一是轮询调度（round-robin scheduling）。当最后一个进程的时间结束时，调度器将从第一个进程重新开始。例如，在有三个进程的情况下，第一个时间片分配给第一个进程，第二个分配给第三个，第四个又回到第一个进程。这种循环将这样无限持续下去。

假设我们决定编写一个通用的轮询调度类，它可以用于任何类型的资源。该类应该支持添加和删除资源，并应该支持顺序循环遍历资源以获取下一个。你可以直接使用 `vector`，但编写一个包装器通常会有帮助，它可以更直接地提供你特定应用程序所需的功能。以下示例展示了一个带有代码注释的 `RoundRobin` 类模板。这里是该类的定义：

```cpp
// 类模板 RoundRobin
// 为元素列表提供简单的轮询语义。

template <typename T>
class RoundRobin {
public:
    // 客户端提供预期元素数量的提示，
    // 以提高效率。
    RoundRobin(size_t numExpected = 0);
    virtual ~RoundRobin();
    // 防止赋值和值传递
    RoundRobin(const RoundRobin& rhs) = delete;
    RoundRobin& operator=(const RoundRobin& rhs) = delete;
    // 将元素附加到列表末尾。可以在调用
    // getNext() 之间调用。
    void add(const T& elem);
    // 从列表中删除与 elem 等（operator==）
    // 的第一个元素。
    // 可以在调用 getNext() 之间调用。
    void remove(const T& elem);
    // 返回列表中的元素，从第一个元素开始，
    // 当到达列表末尾时循环回到第一个，
    // 同时考虑已添加或删除的元素。
    T& getNext();
private:
    std::vector<T> mElems;
    std::vector<T>::iterator mCurElem;
};
```

如你所见，接口非常直接：三个参数和析构函数。资源存储在 `vector` `mElems` 中。迭代器 `mCurElem` 始终指向上一次调用 `getNext()` 返回的元素。如果还没有调用过 `getNext()`，`mCurElem` 等于 `end(mElems)`。在声明 `mCurElem` 的行之前使用了 `typename` 关键字。所以，你只见过将 `typename` 关键字用于指定模板参数，但在一个或多个模板参数上。在这种情况下，每当你访问基于模板参数 `T` 的类型（即访问迭代器类型），必须指定 `typename`。因此，你必须指定 `typename`。这是 C++ 语法的另一个例子。

该类还防止 `mElems` 数据的赋值和值传递。要实现赋值和值传递，你需要实现赋值运算符和构造函数，并确保 `mElems` 在目标对象是有效的。此示例中省略了这一点。

接下来是 `RoundRobin` 类的实现，并带有代码注释。

在构造函数中使用了 `reserve()`，以及在 `add()`、`remove()` 和 `getNext()` 中大量使用了迭代器。最复杂的方面是在 `add()` 和 `remove()` 方法中处理 `mCurElem`。

```cpp
template <typename T> RoundRobin<T>::RoundRobin(size_t numExpected)
{
    // 如果客户端提供了指导建议，则预留该空间。
    mElems.reserve(numExpected);
    // 初始化 mCurElem，尽管它在至少有一个
    // 元素时才被使用。
    mCurElem = end(mElems);
}

template <typename T> RoundRobin<T>::~RoundRobin()
{
    // 无需操作
}

// 重置迭代器以确保它是有效的。
template <typename T> void RoundRobin<T>::add(const T& elem)
{
    // 如果 vector 为空，将迭代器设置为起始。
    if (mElems.empty()) {
        mCurElem = mElems.begin();
    } else {
        // 如果迭代器在末尾，回到开头。
        if (mCurElem == mElems.end()) {
            mCurElem = mElems.begin();
        }
    }
    mElems.push_back(elem);
    // 如果我们刚刚在末尾添加了元素，且
    // 迭代器位于末尾，则将其循环。
    if (mCurElem == mElems.end()) {
        mCurElem = mElems.begin();
    }
}

template <typename T> T& RoundRobin<T>::getNext()
{
    // 首先确保有元素。
    if (mElems.empty()) {
        throw std::out_of_range("列表中没有元素");
    }
    // 如果还没有调用过 Next()，mCurElem 等于 end(mElems)
    //（构造函数）。在这种情况下回到开头。
    if (mCurElem == mElems.end()) {
        mCurElem = mElems.begin();
    } else {
        // 之前调用过 Next()。
        // 对元素数量递增迭代器。
        ++mCurElem;
        if (mCurElem == mElems.end()) {
            mCurElem = mElems.begin();
        }
    }
    // 返回元素的引用。
    return *mCurElem;
}

template <typename T> void RoundRobin<T>::remove(const T& elem)
{
    // 在列表中搜索要删除的元素。
    for (auto i = mElems.begin(); i != mElems.end(); ++i) {
        if (*i == elem) {
            // 如果我们正在移除当前元素，
            // 将迭代器移动到下一个元素。
            if (i == mCurElem) {
                ++mCurElem;
                if (mCurElem == mElems.end()) {
                    mCurElem = mElems.begin();
                }
            }
            // 除元素。
            mElems.erase(i);
            // 如果迭代器现在位于末尾，
            // 将其回到开头。
            if (mCurElem == mElems.end() && !mElems.empty()) {
                mCurElem = mElems.begin();
            }
            return;
        }
    }
}
```

# 第 16 章 深入容器与迭代器

```cpp
Scheduler::Scheduler(const vector<Process>& processes)
{
  // 添加进程
  for (auto& process : processes) {
    rr.add(process);
  }
}

void Scheduler::scheduleTimeSlice() {
  try {
    rr.getNext().doWorkDuringTimeSlice();
  } catch (const out_of_range&) {
    cerr << "No more processes to schedule." << endl;
  }
}
```
