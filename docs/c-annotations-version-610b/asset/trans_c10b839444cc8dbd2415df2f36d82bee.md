

## 12.3 关联容器

这意味着要确定 multimap 中具有相同键的所有元素。本节末尾给出了一个示例，说明这些成员函数的使用。

- `multimap::iterator find(key)`：该成员返回一个迭代器，指向第一个键为 `key` 的值。如果该元素不存在，则返回指向末尾的迭代器。可以递增该迭代器以访问所有具有相同键的元素，直到它到达末尾，或者迭代器的 `first` 成员不再等于 `key`。
- `multimap::iterator insert()`：该成员函数通常会成功，因此返回的是 `multimap::iterator`，而不是像 map 容器那样返回 `pair<multimap::iterator, bool>`。返回的迭代器指向新添加的元素。

虽然 lower_bound 和 upper_bound 函数在 map 和 multimap 容器中行为相同，但它们在 multimap 中的操作值得额外注意。下一个示例说明了将 lower_bound、upper_bound 和 equal_range 应用于 multimap 的情况。

```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    pair<string, int> pa[] =
    {
        pair<string,int>("alpha", 1),
        pair<string,int>("bravo", 2),
        pair<string,int>("charley", 3),
        pair<string,int>("bravo", 7),  // unordered 'bravo' values
        pair<string,int>("delta", 5),
        pair<string,int>("bravo", 4),
    };
    multimap<string, int> object(&pa[0], &pa[6]);

    typedef multimap<string, int>::iterator msiIterator;

    msiIterator it = object.lower_bound("brava");

    cout << "Lower bound for 'brava': " <<
        it->first << ", " << it->second << '\n';

    it = object.upper_bound("bravu");

    cout << "Upper bound for 'bravu': " <<
        it->first << ", " << it->second << '\n';

    pair<msiIterator, msiIterator>
        itPair = object.equal_range("bravo");

    cout << "Equal range for 'bravo':\n";
    for (it = itPair.first; it != itPair.second; ++it)
        cout << it->first << ", " << it->second << '\n';
    cout << "Upper bound: " << it->first << ", " << it->second << '\n';

    cout << "Equal range for 'brav':\n";
    itPair = object.equal_range("brav");
    for (it = itPair.first; it != itPair.second; ++it)
        cout << it->first << ", " << it->second << '\n';
    cout << "Upper bound: " << it->first << ", " << it->second << '\n';
}
/*
    Generated output:

    Lower bound for 'brava': bravo, 2
    Upper bound for 'bravu': charley, 3
    Equal range for 'bravo':
    bravo, 2
    bravo, 7
    bravo, 4
    Upper bound: charley, 3
    Equal range for 'brav':
    Upper bound: bravo, 2
*/
```

特别注意以下特性：

- 对于不存在的键，`lower_bound` 和 `upper_bound` 产生相同的结果：它们都返回第一个键大于给定键的元素。
- 虽然 `multimap` 中的键是有序的，但相同键的值是无序的：它们按照输入的顺序被检索。

### 12.3.8 `set`容器

`set` 类实现了一个排序的值集合。在使用 `set` 容器之前，必须包含 `<set>` 头文件。

`set` 包含唯一的值（容器可接受的类型）。每个值只存储一次。

可以显式创建特定的值：每个 `set` 都定义了 `value_type`，可用于创建可以存储在集合中的值。例如，可以如下构造 `set<string>` 的值：

```cpp
set<string>::value_type setValue("Hello");
```

`value_type` 与 `set<string>` 相关联。也经常使用匿名 `value_type` 对象。例如，

```cpp
set<string>::value_type("Hello");
```

与其反复使用 `set<string>::value_type(...)`，通常使用 `typedef` 来减少输入并提高可读性：

```cpp
typedef set<string>::value_type StringSetValue;
```

使用这个 `typedef`，可以如下构造 `set<string>` 的值：

```cpp
StringSetValue("Hello");
```

或者，可以直接使用 `set` 类型的值。在这种情况下，类型 `Type` 的值会被隐式转换为 `set<Type>::value_type`。

`set` 容器提供以下构造函数、运算符和成员函数：

- 构造函数：
  - 可以构造一个空的集合：
    ```cpp
    set<int> object;
    ```
  - 可以使用两个迭代器初始化集合。例如：
    ```cpp
    int intarr[] = {1, 2, 3, 4, 5};
    set<int> object(&intarr[0], &intarr[5]);
    ```

    请注意，集合中的所有值必须不同：构造集合时不能重复存储相同的值。如果相同值重复出现，只有该值的第一个实例被放入集合中，其余值被静默忽略。

    和 map 一样，set 拥有它包含的数据的自己的副本。
- 可以使用复制构造函数初始化集合：
  ```cpp
  extern set<string> container;
  set<string> object(container);
  ```
- set 容器只支持容器可用的标准运算符集。
- set 类具有以下成员函数：
  - `set::iterator begin()`：该成员返回一个迭代器，指向集合的第一个元素。如果集合为空，则返回 `end`。
  - `void clear()`：该成员从集合中删除所有元素。
  - `size_t count(key)`：如果集合中存在给定的键，该成员返回 1，否则返回 0。
  - `bool empty()`：如果集合中没有元素，该成员返回 `true`。
  - `set::iterator end()`：该成员返回一个迭代器，指向集合最后一个元素之后的位置。
  - `pair<set::iterator, set::iterator> equal_range(key)`：该成员返回一对迭代器，分别是下面介绍的成员函数 `lower_bound` 和 `upper_bound` 的返回值。
  - `... erase()`：该成员可用于从集合中删除特定元素或元素范围：
    - `bool erase(value)` 从集合中删除具有给定值的元素。如果该值被移除，则返回 `true`；如果集合不包含元素 `value`，则返回 `false`。
    - `void erase(pos)` 删除迭代器 `pos` 指向的元素。
    - `void erase(first, beyond)` 删除迭代器范围 `[first, beyond)` 指示的所有元素。
  - `set::iterator find(value)`：该成员返回一个迭代器，指向具有给定值的元素。如果元素不存在，则返回 `end`。
  - `... insert()`：该成员可用于将元素插入集合。如果元素已存在，则现有元素保持不变，并忽略要插入的元素。返回值取决于调用的 insert 版本：
    - `pair<set::iterator, bool> insert (keyvalue)` 将新的 `set::value_type` 插入集合。返回值是 `pair<set::iterator, bool>`。如果返回的 `bool` 字段为 `true`，则 value 已插入集合。值 `false` 表示指定的值已存在于集合中，因此提供的值未插入集合。在这两种情况下，`set::iterator` 字段都指向集合中具有指定值的数据元素。
    - `set::iterator insert (pos, keyvalue)`。这样也可以将 `set::value_type` 插入集合。`pos` 被忽略，并返回指向已插入元素的迭代器。
    - `void insert(first, beyond)` 将迭代器范围 `[first, beyond)` 指向的 `(set::value_type)` 元素插入集合。
  - `set::iterator lower_bound(key)`：该成员返回一个迭代器，指向第一个键至少等于指定键的键值元素。如果不存在这样的元素，则函数返回 `end`。
  - `set::reverse_iterator rbegin()`：该成员返回一个迭代器，指向集合的最后一个元素。
  - `set::reverse_iterator rend()`：该成员返回一个迭代器，指向集合第一个元素之前的位置。
  - `size_t size()`：该成员返回集合中元素的数量。
  - `void swap(argument)`：该成员可用于交换两个使用相同数据类型的集合（argument 是第二个集合）。
  - `set::iterator upper_bound(key)`：该成员返回一个迭代器，指向第一个键大于指定键的键值元素。如果不存在这样的元素，则函数返回 `end`。

### 12.3.9 `multiset`容器

与 `set` 一样，`multiset` 类实现了排序的值集合。在使用 `multiset` 容器之前，必须包含 `<set>` 头文件。

`set` 和 `multiset` 之间的主要区别在于，`multiset` 支持相同值的多个条目，而 `set` 包含唯一的值。

`set` 和 `multiset` 具有相同的成员函数集。有关 `multiset` 成员函数的概述，请参阅第 12.3.8 节。但是，有些成员函数的行为与 `set` 容器中的对应函数略有不同。这里介绍这些成员。

- `size_t count (value)`：该成员返回与给定值关联的 multiset 中条目的数量。
- `... erase()`：该成员可用于从 multiset 中删除元素：
  - `size_t erase(value)` 删除所有具有给定值的元素。返回被删除元素的数量。

