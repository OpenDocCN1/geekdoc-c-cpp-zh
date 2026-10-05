

```cpp
vector<Number> allNumbers;
vector<Number*> primes;
// _
for(Number &z : allNumbers)
    if(isPrime(z, primes))
        primes.push_back(&z); // store address
return primes; // Pointers to function-local objects
}
```

**Listing 20.9** 不要返回函数局部对象的地址。

## 20.7 C 数组 (C-Arrays)

通过 `vector` 和 `array`，你已经有了非常好的选项来顺序存储多个相似的元素。但有时你需要回到基础，在这种情况下，这意味着要使用 C 数组。

从原则上说，C 数组等同于带有额外大小信息的原始指针。指针指向单个值，而 C 数组则指向若干个连续值的起始位置：

```cpp
int value = 42;
int* pointer = &value; // 指向单一个 int
int array[10] = {1,2,3,4,5,6,7,8,9,10}; // 包含 10 个 int 值的 C 数组
```

现在 `array` 的类型为 `int[10]`，你可以使用基于范围的 for 循环遍历所有元素：

```cpp
for(int val : carray)
  cout << val;
```

你也可以读取第五个元素或向第八个元素写入。需要注意的是，和 `vector` 以及 `array` 一样，元素的索引从零开始：

```cpp
int x = carray[4]; // 获取第 5 个元素
carray[7] = 12; // 写入第 8 个元素
```

C 数组如何与原始指针工作要稍微复杂一些。例如，你可以隐式地将任何 C 数组转换为相同类型的简单指针。这为你提供了一个 `int*`：

```cpp
int* ptr = carray;
```

此 `ptr` 指向 `carray[0]`。因此，通过 `*ptr = 99`，你设置了 `carray[0] = 99`。

### 20.7.1 使用指针进行计算

当原始指针指向 C 数组时，你可以对该指针进行算术运算。例如，像处理整数一样使用 `++`、`--` 以及 `+` 和 `-` 操作。

```cpp
// https://godbolt.org/z/a5b6gMo9h
#include <iostream>
int main() {
    int carry[10] = { 1, 1 }; // 初始化为 {1,1,0,0,0,0,0,0,0,0};
    int* end = carry+10; // 指向最后一个元素之后的指针
    for(int* p = carry+2; p != end; ++p) {
        *p = *(p-1) + *(p-2); // 加上前两个值
    }
    for(int const* p=carry; p != end; ++p) {
        std::cout << *p << " ";
        std::cout << "\n";
    }
}
```

**Listing 20.10** 使用指向 C 数组的原始指针，你可以进行算术运算。

该程序输出 1 1 2 3 5 8 13 21 34 55。这是如何运作的？首先，程序用两个 1 初始化数组，随后是根据需要填充的零。**警告：** 如果你不指定初始化，C 数组将包含随机值——例如：

```cpp
int carray[10]; // C 数组保持未初始化
```

通过 `carray+10`，你初始化了 `end`，使其指向 C 数组最后一个元素**之后**的指针。在 C 和 C++ 中，有一种常见的惯例是记住范围的末尾，而不是指向最后一个元素本身。副作用是 `carray` 指针和 `end` 指针之间的差恰好是它们之间的元素数量：((end-carray)=10) 为真。

然后，用 `carray+2` 初始化循环的 `int* p`，从而指向 `carray` 中两个 1 之后的第一个元素。这正应该是你想要写入的第一个位置。在循环的每次迭代中，将 `p` 在 C 数组中移动一个位置。然而，你需要在每次增量后检查 `for` 循环，通过 `p != end` 检查 `p` 是否尚未指向 C 数组之后的元素（这标志着循环的结束）。因此，在循环期间，`p` 指向 `carray+2`、`carray+3`、`carray+4`…… 直到 `carray+9`，以执行循环体。最后的增量将 `p` 推进到 `carray+10`，这代表循环的终止条件。

在循环体内，你向 `*p` 写入，这意味着 `carray+2` 到 `carray+9` 顺序指向的内容。你写入了什么？嗯，使用 `*(p-1) + *(p-2)` 作为前两个元素的和——对于第一次迭代，实际上是：

```cpp
*p = *(p-1) + *(p-2); // 在第一次循环迭代中，p = carray+2，所以：
*(carray+2) = *(carray+2-1) + *(carray+2-2); // 相当于：
```

```cpp
(carray+2) = *(carray+1) + *(carray+0); // 相当于：
carray[2] = carray[1] + carray[0]; // 所以：
carray[2] = 1 + 1;
```

你已经学习了不同的表示法。*(carray+x)` 等同于 `carray[x]`。在第二次循环迭代中，当 `p = carray+3` 时，最终结果是：

```cpp
carray[3] = carray[2] + carray[1]; // 即
carray[3] = 2 + 1;
```

以此类推，直到整个 `carray` 被覆盖为 {1, 1, 2, 3, 5, 8, 13, 21, 34, 55}。你看到可以使用基于范围的 for 循环遍历 C 数组。你可以这样做是因为与原始指针 `int*` 不同，C 数组携带它的大小。不幸的是，一旦你将 C 数组传递给函数，它的大小就会丢失——它退化为相同类型的简单指针。

20.7.2 C 数组的退化 (Decay)

```cpp
// https://godbolt.org/z/a5b6gMo9h
#include <iostream>
int main() {
    int carry[10] = { 1, 1 }; // 初始化为 {1,1,0,0,0,0,0,0,0,0};
    int* end = carry+10; // 指向最后一个元素之后的指针
    for(int* p = carry+2; p != end; ++p) {
        *p = *(p-1) + *(p-2); // 加上前两个
    }
    for(int const* p=carry; p != end; ++p) {
        std::cout << *p << " ";
        std::cout << "\n";
    }
}
```

**Listing 20.10** 使用指向 C 数组的原始指针，你可以进行算术运算。

通过 `carray+10`，你初始化 `end`，使其指向 C 数组最后一个元素**之后**。在 C 和 C++ 中，有一种常见的惯例是记住范围的末尾，而不是指向最后一个元素本身。副作用是 `carray` 指针和 `end` 指针之间的差恰好是它们之间的元素数量：((end-carray)=10) 为真。

然后，用 `carray+2` 初始化循环的 `int* p`，从而指向 `carray` 中两个 1 之后的第一个元素。这应该是你想要写入的第一个位置。在循环的每次迭代中，将 `p` 在 C 数组中移动一个位置。然而，你需要在每次增量后检查 `for` 循环，通过 `p != end` 检查 `p` 是否尚未指向 C 数组之后的元素（这标志着循环的结束）。因此，在循环期间，`p` 指向 `carray+2`、`carray+3`、`carray+4`…… 直到 `carray+9`，以执行循环体。最后的增量将 `p` 推进到 `carray+10`，这代表循环的终止条件。

在循环体内，你向 `*p` 写入，这意味着 `carray+2` 到 `carray+9` 顺序指向的内容。你写入了什么？嗯，使用 `*(p-1) + *(p-2)` 作为前两个元素的和——对于第一次迭代，实际上是：

```cpp
*p = *(p-1) + *(p-2); // 在第一次循环迭代中，p = carray+2，所以：
*(carray+2) = *(carray+2-1) + *(carray+2-2); // 相当于：
```

```cpp
(carray+2) = *(carray+1) + *(carray+0); // 相当于：
carray[2] = carray[1] + carray[0]; // 所以：
carray[2] = 1 + 1;
```

你已经学习了不同的表示法。*(carray+x)* 等同于 `carray[x]`。

在第二次循环迭代中，当 `p = carray+3` 时，最终结果是：

```cpp
carray[3] = carray[2] + carray[1]; // 即
carray[3] = 2 + 1;
```

以此类推，直到整个 `carray` 被覆盖为 {1, 1, 2, 3, 5, 8, 13, 21, 34, 55}。你看到可以使用基于范围的 for 循环遍历 C 数组。你可以这样做是因为与原始指针 `int*` 不同，C 数组携带它的大小。不幸的是，一旦你将 C 数组传递给函数，它的大小就会丢失——它退化为相同类型的简单指针。

### 20.7.3 动态 C 数组

当你需要一个大小在运行时确定的 C 数组，你可以使用 `new[]` 运算符。它返回一个指向堆上动态分配数组第一个元素的指针。你还必须使用 `delete[]` 来释放内存。

```cpp
int size;
cin >> size;
int* dynamicArray = new int[size];
// ... 使用 dynamicArray
delete[] dynamicArray;
```

和静态 C 数组一样，动态 C 数组并不携带它的大小。你必须自己跟踪大小。

