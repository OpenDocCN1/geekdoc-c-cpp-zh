
## 11.10. 函数对象

函数对象是定义了 `operator()` 的对象。函数对象不仅与泛型算法结合使用，还作为函数指针的一种（首选的）替代方案。

函数对象经常用于实现*谓词*函数。谓词函数返回布尔值。谓词函数和谓词函数对象通常称为“谓词”。谓词经常被泛型算法使用，例如第19章介绍的 `count_if` 泛型算法，它返回其函数对象返回 `true` 的次数。在*标准模板库*中使用了两种谓词：*一元谓词*接收一个参数，*二元谓词*接收两个参数。

假设我们有一个类 `Person` 和一个 `Person` 对象数组。进一步假设该数组未排序。在数组中查找特定 `Person` 对象的一种众所周知的方法是使用函数 `lsearch`，它在数组中执行*线性搜索*。示例：

```cpp
Person &target = targetPerson();    // determine the person to find
Person *pArray;
size_t n = fillPerson(&pArray);

cout << "The target person is";

if (!lsearch(&target, pArray, &n, sizeof(Person), compareFunction))
    cout << " not";
cout << "found\n";
```

函数 `targetPerson` 确定我们要找的人，并调用 `fillPerson` 填充数组。然后使用 `lsearch` 定位目标人员。

比较函数必须可用，因为它的地址是 `lsearch` 的参数之一。它必须是一个具有地址的实际函数。如果将其定义为内联，那么编译器别无选择，只能忽略该请求，因为内联函数没有地址。`compareFunction` 可以这样实现：

```cpp
int compareFunction(void const *p1, void const *p2)
{
    return *reinterpret_cast<Person const *>(p1)   // lsearch wants 0
           !=                                       // for equal objects
           *reinterpret_cast<Person const *>(p2);
}
```

当然，这假设 `operator!=` 已在类 `Person` 中重载。但重载 `operator!=` 没什么大不了的，所以假设该运算符确实可用。

平均而言，以下操作*至少*会发生 `n / 2` 次：

- 1. 比较函数的两个参数被压入栈；
- 2. 确定 `lsearch` 最后一个参数的值，生成 `compareFunction` 的地址；
- 3. 调用比较函数；
- 4. 然后，在比较函数内部，`Person::operator!=` 的右操作数的地址被压入栈；
- 5. 对 `Person::operator!=` 求值；
- 6. `Person::operator!=` 函数的参数从栈中弹出；
- 7. 比较函数的两个参数从栈中弹出。

使用函数对象会得到不同的情形。假设我们构造了一个函数 `PersonSearch`，其原型如下（然而，这并不是首选方法。通常，泛型算法优于自制函数。但现在我们关注 `PersonSearch`，以说明函数对象的使用和实现）：

```cpp
Person const *PersonSearch(Person *base, size_t nmemb,
                           Person const &target);
```

该函数可以如下使用：

```cpp
Person &target = targetPerson();
Person *pArray;
size_t n = fillPerson(&pArray);

cout << "The target person is";

if (!PersonSearch(pArray, n, target))
    cout << " not";

cout << "found\n";
```

到目前为止，变化不大。我们将对 `lsearch` 的调用替换为对另一个函数的调用：`PersonSearch`。现在看看 `PersonSearch` 本身：

```cpp
Person const *PersonSearch(Person *base, size_t nmemb,
                           Person const &target)
{
    for (int idx = 0; idx < nmemb; ++idx)
        if (target(base[idx]))
            return base + idx;
    return 0;
}
```

`PersonSearch` 实现了一个简单的线性搜索。然而，在 for 循环中我们看到 `target(base[idx])`。这里 `target` 被用作*函数对象*。其实现很简单：

```cpp
bool Person::operator()(Person const &other) const
{
    return *this == other;
}
```

注意有点奇特的语法：`operator()`。第一组圆括号定义被重载的运算符：函数调用运算符。第二组圆括号定义该重载运算符所需的参数。在类头文件中，该重载运算符声明为：

```cpp
bool operator()(Person const &other) const;
```

显然，`Person::operator()` 是一个简单的函数。它只包含一条语句，我们可以考虑将其定义为内联。假设我们这样做，那么调用 `operator()` 时会发生以下情况：

- 1. `Person::operator==` 的右操作数的地址被压入栈；
- 2. `operator==` 函数被求值（当寻找与指定目标对象*相等*的对象时，这相对于调用 `operator!=` 可能也是一种*语义*上的改进）；
- 3. `Person::operator==` 的参数从栈中弹出。

由于 `operator()` 是内联函数，它实际上不会被调用。相反，会立即调用 `operator==`。此外，所需的栈操作相当有限。

函数对象确实可以定义为内联。间接调用的函数（即通过函数指针调用）永远不能定义为内联，因为必须知道其地址。因此，即使函数对象需要做的工作很少，如果将通过指针调用它，也要将其定义为普通函数。执行间接调用的开销可能会抵消间接调用函数所带来的灵活性优势。在这些情况下，使用内联函数对象可以提高程序效率。

函数对象的另一个好处是，它们可以访问其所属对象的私有数据。在使用比较函数的搜索算法中（如 `lsearch`），目标和数组元素通过指针传递给比较函数，这会涉及额外的栈处理。使用函数对象时，目标人员在单次搜索任务中不会变化。因此，目标人员可以传递给函数对象所属类的构造函数。事实上，在表达式 `target(base[idx])` 中就是如此：它把要搜索数组的后续元素作为其唯一参数接收。

### 11.10.1 构造操纵器

在第6章中，我们见过类似 `cout << hex << 13` 的写法，以十六进制格式显示值 13。人们可能会好奇 `hex` 操纵器是如何神奇地做到这一点的。本节介绍像 `hex` 这样的操纵器的构造。

实际上，操纵器的构造相当简单。首先，需要给出操纵器的定义。假设我们要创建一个操纵器 `w10`，它将 ostream 对象要写入的下一个字段的字段宽度设置为 10。该操纵器被构造为一个函数。`w10` 函数需要知道要在哪个 ostream 对象中设置宽度。通过为该函数提供一个 `ostream &` 参数，它便获得了这一信息。既然该函数知道了我们所指的 ostream 对象，它就可以在该对象中设置宽度。

接下来，必须能够在插入序列中使用该操纵器。这意味着操纵器的返回值也必须是对 `ostream` 对象的引用。

基于上述考虑，现在我们可以构造 `w10` 函数：

```cpp
#include <ostream>
#include <iomanip>

std::ostream &w10(std::ostream &str)
{
    return str << std::setw(10);
}
```

当然，`w10` 函数可以在“独立”模式下使用，但也可以用作操纵器。例如：

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

extern ostream &w10(ostream &str);

int main()
{
    w10(cout) << 3 << " ships sailed to America\n";
    cout << "And " << w10 << 3 << " more ships sailed too.\n";
}
```
