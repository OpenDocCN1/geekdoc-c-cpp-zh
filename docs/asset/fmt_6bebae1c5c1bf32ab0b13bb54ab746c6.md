
`erase(first, beyond)` 删除迭代器范围 `[first, beyond)` 所示的元素，返回 `beyond`。

`Type &front()`：返回 `vector` 中第一个元素的引用。程序有责任在 `vector` 不为空时才使用该成员。

`allocator_type get_allocator() const`：返回 `vector` 对象使用的分配器的拷贝。

`insert()`：在特定位置插入元素。其返回值取决于所调用的 `insert()` 版本：

- `iterator insert (pos)` 在 `pos` 处插入 `Type` 的默认值，返回 `pos`。
- `iterator insert (pos, value)` 在 `pos` 处插入值，`pos` 迭代器范围 `[first, beyond)` 的元素。
- `void insert (pos, n, value)` 在位置 `pos` 插入 `n` 个具有值 `value` 的元素。

`size_max()`：返回 `vector` 可能包含的最大元素个数。

`pop_back()`：从 `vector` 中删除最后一个元素。避免在空 `vector` 上调用此成员：虽然没有返回值，但其内部维护的可用元素计数会减少，导致 `vector` 的 `size()` 成员返回的值（转换为 `int` 后）为 `value-1`，然后是 `-2` 等。

`void push_back(value)`：将 `value` 添加到 `vector` 的末尾。

`reverse_iterator rbegin()`：此成员返回一个指向 `vector` 中最后一个元素的反向迭代器。

`reverse_iterator rend()`：返回一个指向 `vector` 第一个元素之前的反向迭代器。

## 12.4 可用容器

`void reserve(size_t request)`：如果 `request` 小于或等于 `capacity`，则没有影响。否则，这是一个分配额外内存的请求。如果调用成功，`capacity` 返回的值至少为 `request`。否则，`capacity` 保持不变。在何种情况下，`size` 的返回值都不会改变，直到调用 `resize` 函数，这才会实际改变元素的数量。

`void resize()`：可用于更改 `vector` 中当前存储的元素数量：

- `resize(n, value)` 可将 `vector` 的大小调整为 `n`。`value` 是可选的。如果扩充了 `vector` 并且提供了 `value`，则额外的元素将初始化为所用数据类型的默认值；否则，使用 `value` 初始化额外的元素。

`void shrink_to_fit()`：可选地将 `vector` 分配的内存量减少到其当前大小。实现者可以忽略或优化此请求。为了保证“收缩”适应操作，可以使用：

```
vector<Type>(vectorObject).swap(vectorObject)
```

这种用法。

`size_t size()`：返回 `vector` 中的元素数量。

`void swap(vector<Type>& other)`：交换两个具有相同数据类型的 `vector`。示例：

```
#include <iostream>
#include <vector>
using namespace std;

int main() {

vector<int> v1(7);
vector<int> v2(10);

v1.swap(v2);
cout << v1.size() << " " << v2.size() << '\n';
}
```

产生输出：

```
10 7
```

## 12.4.3 `list` 容器

`list` 容器实现了一种数据结构。在使用 `list` 容器之前，必须包含头文件 `<list>`。

`list` 的组织结构如图 12.1 所示。12.1 显示 `list` 由指针连接的独立 `list` 元素组成。`list` 可以从左到右遍历，从 `Front` 开始，直到到达最右侧元素末的 `0` 指针。`list` 也可以从右到左遍历：从 `Back` 开始，从右向左遍历 `list`，直到遇到最左侧 `list` 元素的 `0` 指针。

需要注意的是，图 12.1 中给出的表示并不一定用于 `list` 的实际实现中。例如，考虑以下小程序：

Front

![](img/0037575dc38a83100348a92b3d53bd6f_389_0.png)
图 12.1：一个 `list` 数据结构

```
int main() {

    list<int> l;

    cout << "size: " << l.size() << ", first element: " << l.front() << '\n';

}
```

运行此程序时，它实际上可能会产生输出：

```
size: 0, first element: 0
```

它的第一个元素可以被赋值。在这种情况下，实现者选择为 `list` 提供一个隐藏元素。`list` 实际上是一个循环列表，其中隐藏元素作为终止元素，替换了函数 12.1 中的 `0` 指针。如所述，这里存在一个细微之处，但并不影响 `list` 作为以 `0` 指针结尾的结构概念。注意，众所周知，`list` 结构有许多实现方式（参见 Aho, A.V., Hoffman J.E. and Ullman, J.D., (1983) *Data Structures and Algorithms* (Addison-Wesley）。

在必须存储未知数量数据元素的情况下，`list` 和 `vector` 往往都是合适的数据结构。然而，在选择合适的数据结构时，有一些经验法则需要遵循。

- 当进行随机访问时，`vector` 是更好的选择。
- 当元素数量提前已知时，`vector` 是更好的选择。
- 当需要频繁插入或删除时，`list` 是更好的选择。
- 当内存受限时，`list` 是更好的选择。

## 12. 可用容器

`void merge(list<Type> other)`：该成员函数假设当前列表和另一个列表都是排序过的（见下文的成员函数 `sort`）。基于该假设，它将 `other` 中的元素插入到当前列表中，使得修改后的列表保持排序状态。如果两个列表都未排序，则结果列表将“尽可能”按照两个列表中元素的初始次顺序进行排列。`list<Type>::merge` 使用 `Type::operator` 来对列表中的数据进行排序，因此该操作符必须是可用的。接接的示例说明了 `merge` 的用法：列表 `object` 未排序，因此结果列表将“尽可能”按照元素的初始顺序排列。

```cpp
#include <iostream>
#include <string>
#include <list>
using namespace std;

void show(list<string> &target)
{
    for (
        list<string>::iterator from = target.begin();
        from != target.end();
        ++from
    )
    cout << from << "";
    cout << '\n';
}

int main()
{
    list<string> first;
    list<string> second;

    first.push_back("alpha");
    first.push_back("bravo");
    first.push_back("golf");
    first.push_back("quebec");

    second.push_back("oscar");
    second.push_back("mike");
    second.push_back("november");
    second.push_back("zulu");

    first.merge(second);
    show(first);
}

// shows:
// alpha bravo golf oscar mike november quebec zulu
```

`merge` 的微妙之处在于，如果列表本身被用参数，它不会改变列表：`object.merge(object)` 将不会改变 `object` 列表。

`void pop_back()`：移除列表的最后一个元素。在空列表上调用时，程序将终止。

`void pop_front()`：移除列表的第一个元素。在空列表上调用时，程序将终止。

`void push_back(value)`：将 `value` 添加到列表的末尾。

`void push_front(value)`：将 `value` 添加到列表的第一个元素之前。

`list::reverse_iterator rbegin()`：返回指向列表中最后一个元素的反向迭代器。

`void remove(value)`：从列表中移除所有等于 `value` 的元素。在接下来的示例中，两个字符串 `Hellos` 从 `object` 列表中被移除：

```cpp
#include <iostream>
#include <string>
#include <list>
using namespace std;

int main() {
  list<string> object;
  object.push_back("Hellos");
  object.push_back("Worlds");
  object.push_back("Hellos");
  object.push_back("Worlds");

  object.remove("Hellos");

  while (object.size()) {
    cout << object.front() << '\n';
    object.pop_front();
  }
}
```

```
/* Generated output:
World
World */
```

`void remove_if(Predicate pred)`：移除列表中所有谓词函数或对象 `pred` 返回 `true` 的元素。对于列表中存储的每个对象，谓词都会被调用为 `pred(+iter)`，其中 `iter` 代表 `remove_if` 内部使用的迭代器。

如果使用函数，其原型格式为 `bool pred(value_type const &object)`。

`list::reverse_iterator rend()`：该成员返回一个指向列表第一个元素之前的反向迭代器。

`void resize()`：更改当前存储在列表中的元素数量：

- `resize(n, value)` 可用于将列表调整为大小 `n`。`value` 是可选的。如果列表被扩展且未提供 `value`，则额外的元素将初始化为所用数据类型的默认值，否则使用 `value` 来初始化额外的元素。

`void reverse()`：反转列表中元素的顺序。末尾的元素变为开头，反之亦然。

## 12.4 可用容器

`size_t size()`：返回列表中元素的数量。

`void sort()`：对列表进行排序。关于此用法的一个示例见下方下方唯一成员列表的描述。`list<Type>::sort` 使用 `Type::operator<` 对列表中的数据进行排序，该操作符必须是可用。

`void splice(pos, object)`：使用 `splice` 成员函数将 `object` 内容转移到当前列表，从 `object` 的迭代器位置 `pos` 开始插入。执行 `splice` 后，`object` 将为空。例如：

```cpp
#include <iostream>
#include <string>
#include <list>
using namespace std;

int main() {
    list<string> object;
    object.push_front("Hello");
    object.push_back("World");

    list<string> argument(object);
    object.splice(object.begin(), argument);

    cout << "Object contains " << object.size() << " elements, " <<
           "Argument contains " << argument.size() <<
           "elements";
}
```

`void swap()`：交换两个列表的内容。

`void unique()`：移除列表中连续的重复元素。为了使其生效，必须先对列表进行排序。

`void clear()`：移除列表中的所有元素。

`size_t size()`：返回列表中元素的数量。

`bool empty()`：如果列表不包含元素，则返回 `true`。

考虑 `pop` 成员函数的典型实现，它预期返回队列的头部值：

```cpp
Type queue::pop() {
    Type ret{ front() };
    erase_front();
    return ret;
}
```

由于 `queue` 无法控制 `Type` 的行为，第一条语句（`Type front()`）可能会抛出异常。尽管这符合“提交或回滚”原则，但 `queue` 无法保证 `Type` 提供了拷贝构造。因此，`pop` 不返回队列的头部值，而是简单地删元素该元素：

```cpp
Type queue::pop() {
    erase_front();
}
```

注意 `push` 并不需要拷贝构造：`push` 也可以通过移动构造来实现。例如：

```cpp
void queue::push(Type &&tmp)
    d_data.push_back(std::move(tmp)); // 使用移动构造
```

正由于这些原因，我们必须先使用 `front` 然后使用 `pop` 来获取并移除队列的元素。

`push(value)`：此成员函数将 `value` 添加到队列末尾。

`size_t size()`：返回队列中的元素数量。

注意 `queue` 不支持迭代器或索引运算符。唯一可以访问的元素是其首尾元素。队列可以通过以下方式清空：

- 重复其头部元素；
- 使用相同的数据类型将空队列赋值给它；
- 调用其析构函数。

## 12.4.5 `priority_queue` 容器

`priority_queue` 类实现了一种优先级队列数据结构。在使用 `priority_queue` 容器之前，必须包含 `<queue>` 头文件。

优先级队列的理想模型是使用队列，但允许根据优先级规则输入数据元素。真实的优先级队列随处可见，例如机场的登机闸台。在闸台，乘客正常排队等待登机，但迟到的乘客允许插队：他们比其他乘客拥有更高的优先级。

优先级队列使用存储在 `priority_queue` 中的数据类型的 `operator<` 来决定数据元素的优先级。值越小，优先级越低。因此，可以使用 `priority_queue` 在值到达时对其进行排序。这种优先级队列应用的一个简单示例是下面的程序：它从 `cin` 读取单词，并将排序后的单词列表写入 `cout`：

```cpp
#include <iostream>
#include <string>
#include <queue>
using namespace std;

int main() {
    priority_queue<string> q;
    string word;

    while (cin >> word) {
        q.push(word);
    }

    while (q.size()) {
        cout << q.top() << '\n';
        q.pop();
    }
}
```

遗憾的是，单词是倒序列出的：由于底层的运算符影响，在 ASCII 序列中较后出现的单词会先出现在 `priority_queue` 中。解决该问题的方法是为 `string` 数据类型定义一个包装类，反转 `string` 的运算符。这里是修改后的程序：

```cpp
#include <iostream>
#include <string>
#include <queue>

class Text {
    std::string d_s;
public:
    Text(std::string const &str) : d_s(str) {}
    operator std::string const &() const {
        return d_s;
    }
    bool operator<(Text const &right) const {
        return d_s > right.d_s;
    }
};

using namespace std;

int main() {
    priority_queue<Text> q;
    string word;

    while (cin >> word)
        q.push(word);

    while (q.size()) {
        word = q.top();
```
