

## 文章

你被一家向各类捐赠者募集捐款的非营利组织聘用。这家非营利组织多年来一直运营缓慢。因此，该组织未能跟上技术发展，所有数据都存储在纸质文件中。最近的疫情清楚地表明这是一个大问题：没有人能去办公室访问这些文件。

你的经理要求你把所有纸质文件扫描到电脑中。文件扫描完成后，你需要设计一个系统来存储数字文件并加以整理，以便轻松搜索。在开始之前，你的经理给了你以下指示。

审查给定的数据集。看来捐赠者信息存在于多个地方。根据你的审查，识别所有潜在的数据源，并确定数据是否需要清理和/或转换。此外，考虑如何将来自不同数据源的所有数据存储在一个地方（例如数据仓库）。最后，列出几个这个统一数据可以回答的问题。

```cpp
int value = 42;
int* pointer = &value;  // points to a single int
int carray[10] = { 1,2,3,4,5,6,7,8,9,10 };  // C-array of 10 int values
```

现在 carray 的类型是 int[10]，你可以使用基于范围的 for 循环遍历所有元素：

```cpp
for(int val : carray)
    cout << val;
```

你还可以读取第五个元素或写入第八个元素。需要注意的是，与 vector 和 array 一样，元素的索引从零开始：

```cpp
int x = carray[4];  // get the 5th element
carray[7] = 12;      // write to the 8th element
```

C 数组与原始指针的配合有点棘手。例如，你可以将任何 C 数组隐式转换为相同类型的简单指针。这会得到一个 int*：

```cpp
int* ptr = carray;
```

该 ptr 现在指向 carray[0]。因此，通过 *ptr = 99;，你设置了 carray[0] = 99;。

### 20.7.1 指针运算

当原始指针指向 C 数组时，你可以对该指针进行算术运算。例如，像使用整数一样使用 + 和 - 运算，以及 ++ 和 --。

```cpp
// https://godbolt.org/z/a5b6qMq9h
#include <iostream>
int main() {
    int carray[10] = { 1,1 };                 // initialized to {1,1,0,0,0,0,0,0,0,0}
    int* end = carray+10;                     // pointer past the last element
    for(int* p = carray+2; p != end; ++p) {
        *p = *(p-1) + *(p-2);                 // adds the previous two numbers
    }
    for(int const * p=carray; p != end; ++p)
        std::cout << *p << " ";
    std::cout << "\n";
}
```

**清单 20.10** 使用指向 C 数组的原始指针，你可以执行算术运算。

该程序输出 1 1 2 3 5 8 13 21 34 55。这是如何工作的？首先，程序用两个 1 初始化 carray，后面跟所需数量的零。**警告：** 如果你不指定初始化，C 数组将包含随机值——例如：

```cpp
int carray[10]; // ⚡ C-array remains uninitialized
```

通过 carray+10，你初始化 `end`，使其成为指向 C 数组最后一个元素**之后**的指针。在 C 和 C++ 中，用这种方式记住范围的末尾是一种常见约定，而不是指向最后一个元素本身。副作用是两个数组端点指针之间的差正好是中间的元素数量：`((end-carray)==10)` 为真。

然后用 `carray+2` 初始化循环的 `int*` 指针 `p`，使其指向 carray 中两个 1 之后的第一个元素。这应该是你想要写入的第一个位置。对于循环的每次迭代，将 `p` 在 C 数组中向前移动一个位置。使用 `++p` 很容易做到。但是，你需要在每次递增后检查循环是否结束：`p != end` 检查 `p` 是否尚未指向 C 数组之后的元素，如果尚未指向，则意味着循环未结束。因此，在循环期间，`p` 指向 `carray+2`、`carray+3`、`carray+4`、... 直到 `carray+9`，以执行循环体。最后的递增将 `p` 推进到 `carray+10`，这表示循环终止条件。

在循环体中，你写入 `*p`，即依次写入 `carray+2` 到 `carray+9` 所引用的内容。你写入什么？嗯，`*(p-1) + *(p-2)` 表示前两个元素之和——对于第一次迭代，实际上是：

```cpp
    *p = *(p-1) + *(p-2); // in the first loop iteration, p = carray+2, so:
    *(carray+2) = *(carray+2-1) + *(carray+2-2); // which is:
    *(carray+2) = *(carray+1) + *(carray+0);       // which is:
    carray[2] = carray[1] + carray[0];             // so:
    carray[2] = 1 + 1;
```

在这里你已经了解了不同的表示法。`*(carray+x)` 等价于 `carray[x]`。

在第二次循环迭代中，当 `p = carray+3` 时，最终得到

```cpp
    carray[3] = carray[2] + carray[1]; // that is:
    carray[3] = 2 + 1;
```

依此类推，直到整个 carray 被覆盖为 `{1, 1, 2, 3, 5, 8, 13, 21, 34, 55}`。

### 20.7.2 C 数组的退化

你已经看到可以使用基于范围的 `for` 循环遍历 C 数组。这是因为与原始指针 `int*` 不同，C 数组 `int[10]` 携带其大小。不幸的是，这个信息非常不稳定，一旦你将 C 数组传递给函数，它就会丢失。此时 C 数组**退化**为简单的原始指针，无法记住数组大小。具体来说，`int[10]`（以及任何其他大小）变成 `int*`。

```cpp
// https://godbolt.org/z/1qX16Gr61
#include <iostream>
void fibonacci(int data[], int* end) {
    for(int* p = data+2; p != end; ++p) {
        *p = *(p-1) + *(p-2);
    }
}
std::ostream& print(std::ostream &os, int data[], int* end) {
    for(int const * p=data; p != end; ++p)
        os << *p << " ";
    return os;
}
int main() {
    int array[10] = {1,1}; // initialized to {1,1,0,0,0,0,0,0,0,0}
    fibonacci(array, array+10);
    print(std::cout, array, array+10) << "\n";
}
```

**清单 20.11** C 数组作为参数时退化为原始指针。

因此，你不能将函数参数声明为 `int[10]`，只能声明为 `int*`。不过，你可以给函数的使用者一些提示。对于 `int* p`，你可以使用替代表示法 `int[]`。这表示该参数来源于一个 int 元素的 C 数组。然而，你只能在注释中传达数组的大小。或者——这也是这类情况下的通常做法——你为函数添加一个 end 参数，它（如前面的例子所示）指向 C 数组的末尾。

作为 `end` 的替代方案，你当然也可以在调用时传递元素数量——这里是 10：

```cpp
std::ostream& print(std::ostream &os, int data[], size_t count) {
    for(int const * p=data; p != (data+count); ++p)
        os << *p << " ";
}
```

在 C 环境中，这种变体使用得更频繁，而使用 end 指针的版本在处理 C++ 标准库时更实用。你将会看到，这些关于指针的见解可以直接转移到*迭代器*的概念上。

如果你不打算更改循环变量所指向的值，最好使用 `int const * p`。如果你想更改这些值，则应使用 `int* p`。

### 20.7.3 动态 C 数组

当你将 C 数组声明为自动栈变量时，数组的大小必须是常量——准确地说，是 constexpr：

```cpp
void calc(size_t sz) {
    int  array[10];  // okay
    int  darr[sz];   // Error: sz is not a constant
}
```

如果你想编写后者，你需要一个支持栈上*动态自动 C 数组*的编译器（自 C++14 起成为标准）。在此之前，你需要使用 new[] 创建这样的*动态 C 数组*：

```cpp
void calc(size_t sz) {
    int* darr = new int[sz];
    // ...
    delete[] darr;
}
```

你可以看到，正如 new 需要 delete 一样，new[] 需要 delete[]。*警告：* 你绝不能用 delete（不带方括号）意外删除用 new[] 创建的 C 数组。

一旦创建了这样的动态 C 数组，你就可以像前面讨论的自动 C 数组一样与之交互。唯一的区别是，你需要负责使用 delete[] 进行销毁。

你是否觉得 delete[] 太繁琐？我同意你的看法。就像自管理的原始指针一样，如果你不非常小心，资源可能会在这里丢失。你应该考虑是否可以使用 vector 来代替。如果不行，那么在创建后立即将 C 数组包装在 unique_ptr 中。它能为你调用 delete[]。

```cpp
// https://godbolt.org/z/hq839x8r
#include <memory>       // unique_ptr
#include <iostream>     // cout

std::unique_ptr<int[]> createData(size_t sz) {
    return std::unique_ptr<int[]>(new int[sz]);
}

void fibonacci(int data[], int* end) {
    for(int* p = data+2; p != end; ++p) {
        *p = *(p-1) + *(p-2);
    }
}
```

