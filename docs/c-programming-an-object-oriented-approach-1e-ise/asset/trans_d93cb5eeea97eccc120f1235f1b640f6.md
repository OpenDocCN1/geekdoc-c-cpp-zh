
## 19.2.4 常量性

容器还可以定义两种类型的迭代器：*常量迭代器* 和 *const_iterator*。

### 类型：常量迭代器

类型 *常量迭代器* 定义了一种作为常量对象的迭代器类型。换句话说，它创建后就不能被改变。我们不能移动 *常量迭代器* 使其指向另一个元素。它就像数组名一样，是一个常量指针。

### 类型：const_iterator

类型 *const_iterator* 定义了一种迭代器类型，其中解引用的项是 *右值*（不能由该迭代器修改）。这类似于我们声明一个元素为常量的数组。

## 19.3 序列容器

**序列容器** 是对象的集合，程序员可以控制存储和取回元素的顺序。STL 提供三种序列容器：*vector*、*deque* 和 *list*。前两种通常实现为动态数组；第三种通常实现为双向链表。

### 19.3.1 公共接口

在讨论序列容器之前，我们在表 19.2 中给出它们的一般公共接口。当相应列被勾选时，缩写 SC 必须替换为三种序列容器（*vector*、*deque* 或 *list*）之一。这些容器中的每一个都是模板类，其中 T 定义容器中元素的类型。*typename T* 可以是任何内置类型或用户定义类型。我们用 *iter* 表示迭代器，用 *inIter* 表示输入迭代器，用 *prev* 表示返回 *true* 或 *false* 的布尔函数。缩写 V 代表 *vector*，D 代表 *deque*，L 代表 *list*。

**表 19.2 — 序列容器类的接口**

| 构造函数、赋值和析构函数 | V | D | L |
|---|:---:|:---:|:---:|
| `SC<T>::SC()` | ✓ | ✓ | ✓ |
| `SC<T>::SC(size_type n, const T& value = T())` | ✓ | ✓ | ✓ |
| `SC<T>::SC(const_iterator first, const_iterator last)` | ✓ | ✓ | ✓ |
| `SC<T>::SC(const SC<T>& other)` | ✓ | ✓ | ✓ |
| `SC<T>& SC<T>::operator=(const SC<T>& other)` | ✓ | ✓ | ✓ |
| `SC<T>::~SC()` | ✓ | ✓ | ✓ |
| **大小和容量** |  |  |  |
| `size_type SC<T>::size()` | ✓ | ✓ | ✓ |
| `size_type SC<T>::max_size()` | ✓ | ✓ | ✓ |
| `void SC<T>::resize(size_type n, T value = T())` | ✓ | ✓ | ✓ |
| `bool SC<T>::empty()` | ✓ | ✓ | ✓ |
| `size_type SC<T>::capacity()` | ✓ |  |  |
| `void SC<T>::reserve(size_type n)` | ✓ |  |  |
| **访问元素（常量版本和非常量版本）** |  |  |  |
| `T& SC<T>::front()` | ✓ | ✓ | ✓ |
| `T& SC<T>::back()` | ✓ | ✓ | ✓ |
| `T& SC<T>::operator[](size_type index)` | ✓ | ✓ |  |
| `T& SC<T>::at(size_type index)` | ✓ | ✓ |  |
| **迭代器（普通版本和常量迭代器版本）** |  |  |  |
| `iter SC<T>::begin()` | ✓ | ✓ | ✓ |
| `iter SC<T>::end()` | ✓ | ✓ | ✓ |
| `reverse_iterator SC<T>::rbegin()` | ✓ | ✓ | ✓ |
| `reverse_iterator SC<T>::rend()` | ✓ | ✓ | ✓ |
| **插入** |  |  |  |
| `void SC<T>::push_front(const T& value)` |  | ✓ | ✓ |
| `void SC<T>::push_back(const T& value)` | ✓ | ✓ | ✓ |
| `iter SC<T>::insert(iter pos, const T& value)` | ✓ | ✓ | ✓ |
| `void SC<T>::insert(iter pos, size_type n, const T& value)` | ✓ | ✓ | ✓ |
| `void SC<T>::insert(iter pos, inIter first, inIter last)` | ✓ | ✓ | ✓ |
| **删除** |  |  |  |
| `void SC<T>::pop_front()` |  | ✓ | ✓ |
| `void SC<T>::pop_back()` | ✓ | ✓ | ✓ |
| `iter SC<T>::erase(iter pos)` | ✓ | ✓ | ✓ |
| `iter SC<T>::erase(iter first, iter second)` | ✓ | ✓ | ✓ |
| `void SC<T>::clear()` | ✓ | ✓ | ✓ |
| `void SC<T>::remove(const T& value)` |  |  | ✓ |
| `void SC<T>::remove_if(pred p)` |  |  | ✓ |
| `void SC<T>::unique(pred p)` |  |  | ✓ |
| **拼接、合并和排序** |  |  |  |
| `void SC<T>::splice(iter pos, SC<T> other)` |  |  | ✓ |
| `void SC<T>::splice(iter pos, SC<T> other, iter other)` |  |  | ✓ |
| `void SC<T>::splice(iter pos, SC<T> other, iter i, iter j)` |  |  | ✓ |
| `void SC<T>::merge(SC<T> other)` |  |  | ✓ |
| `void SC<T>::sort()` |  |  | ✓ |
| **交换** |  |  |  |
| `void SC<T>::swap(SC<T>& other)` | ✓ | ✓ | ✓ |
| **全局函数**（*op* 表示 <、<=、>、>=、== 或 !=） |  |  |  |
| `bool operator *op*(const SC<T>& left, const SC<T>& right)` | ✓ | ✓ | ✓ |
| `void swap(SC<T>& left, SC<T>& right)` | ✓ | ✓ | ✓ |

注意，每个访问成员还有一个创建 *右值* 的常量版本，但为了使接口更简短，我们没有包含它们。还要注意，每个迭代器都有一个 *const_iterator* 版本，出于同样的原因我们也没有包含它。

### 19.3.2 Vector 类

**vector** 类定义在 `<vector>` 头文件中，实现了一种序列容器，可对任意元素进行快速随机访问，并可在尾部快速插入和删除。这意味着，如果我们需要一种在前端或中间进行大量插入和删除的序列容器，vector 并不是最佳选择。vector 是一个具有开放端部的元素序列，如图 19.5 所示。

vector 类实现为在堆内存中分配的数组，但具有额外特性。像数组一样，它具有访问每个元素的索引机制。与数组不同，vector 在需要更多元素时会自行调整大小。

### 操作

vector 类的成员函数语法可从一般公共接口（表 19.2）中获得。在接下来的几节中，我们讨论其中一些操作。

### 构造函数和赋值运算符

vector 类有一个默认构造函数、两个带参构造函数、一个复制构造函数和一个赋值运算符。下面展示我们如何使用这些成员函数。

```cpp
vector<T> vec;                 // Constructs an empty vector
vector<T> vec(4, value);        // Constructs a vector of 4 elements of given value
vector<T> vec(from,to);         // A vector created from another sequence
vector<T> vec(otherVec);        // Copy constructor
vector<T> vec = otherVec;       // Assignment operator
```

第一行展示如何创建一个空 vector。第二行展示如何创建一个包含四个元素的 vector，所有元素具有相同值。注意，如果缺少第二个参数，则使用默认值（例如，整数的零）。第三行展示如何从另一个结构复制元素来创建 vector。参数 *from* 和 *to* 是复制这些元素的迭代器。注意，复制的序列是一个开放端序列 (from, to)，这意味着 *from* 在序列中，但 *to* 不在。下一行是复制构造函数，它创建 *otherVec* 的副本。最后，最后一行是赋值运算符，它完成与复制构造函数相同的工作，但要求 *vec* 对象必须已经实例化。

### 析构函数

当 vector 容器超出作用域时，析构函数会被自动调用。析构函数旨在从堆中删除整个数组。

![](img/d68f6199646ca63591a6d8419e0ed4ba_876_0.png)

**图 19.5** 带索引的 vector 作为序列结构

### 大小和容量

如公共接口（表 19.2）所示，vector 类有六个与 vector 大小和容量相关的成员函数。下面展示我们如何在 vector 类的实例（我们称之为 *vec*）上使用它们。

```
vec.size();                         // Returns the current size
vec.max_size();                     // Returns the maximum size
vec.resize(n, value);               // Resizes the vector
vec.empty();                        // Returns true if vector is empty
vec.capacity();                     // Returns potential size
vec.reserve(n);                     // Reserves more memory locations
```

*size* 函数返回当前 vector 中元素的数量。*max_size* 函数定义 vector 可拥有的最大元素数量（一个在 STL 中定义的大数）。*empty* 函数在 vector 为空时返回 true。如果 *n > size*，*resize(n, value)* 函数向 vector 尾部插入元素；如果 *n < size*，它从 vector 尾部移除元素。如果未给出 *value*，则使用默认值。*capacity* 函数返回已分配位置的数量。换句话说，*capacity* 返回 vector 自行调整大小之前的潜在大小。*reserve* 函数确保容量至少为 *n*。vector 通常会估计我们必须使用多少元素，并基于该估计从堆中分配内存。如果在执行过程中需要更多内存，该函数会分配更大的存储块，将所有元素复制到该块，销毁旧对象，并释放旧块使用的内存——这是一项耗时的活动。

### 访问元素（用于读取或修改）

如公共接口（表 19.2）所示，vector 类提供以下成员函数来访问 vector 中已有的元素。

```
vec.front();                       // Access the first element
vec.back();                        // Access the last element
vec[i];                            // Access the element at index i
vec.at(i);                         // Access the element at index i
```

尽管我们可以使用 vec[i] 或 vec.at(i) 访问索引 *i* 处的元素，但我们推荐 vec.at()，因为它会检查范围，并在索引超出范围时抛出异常。

### 迭代器

vector 类定义了两个普通迭代器和两个反向迭代器。我们在表 19.2 中只展示了普通迭代器。在每个类别中，我们可以有常量迭代器和非常量迭代器。图 19.6 展示了这些迭代器。

注意，由 *begin()*、*end()*、*rbegin()* 和 *rend()* 形成的迭代器是固定迭代器，不能移动。它们被用作限定用户定义迭代器（*iter* 和 *riter*）范围的控制边界。

要在程序中使用迭代器，我们必须先实例化它们。由于每个容器都有自己的迭代器，我们必须根据需要为该特定类创建一个或两个迭代器。根据应用的不同，我们可能需要其中一个或两个。为方便起见，我们将这两个迭代器称为 *iter* 和 *riter*。

```
vector<T>::iterator iter;             // A regular iterator
vector<T>::reverse_iterator riter;    // A reverse iterator
```

在实例化用户迭代器之后，我们必须设置它们。迭代器 *iter* 必须从 *begin()* 返回的迭代器所设置的位置开始；我们必须将迭代器 *riter* 设置为 *rbegin()* 返回的迭代器所设置的位置，如下所示：
