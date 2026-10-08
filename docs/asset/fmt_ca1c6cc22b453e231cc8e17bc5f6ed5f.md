
```cpp
using std::deque;

using std::sort;

int main() {

    deque<int> data;

    // 读取数据

    cout << "输入一组空格分隔的非零整数：" << endl;

    cout << "输入 0 结束。" << endl;

    int value(0);

    while(cin >> value && value != 0)

        data.push_front(value);

    // 输出数据

    cout << endl << "你输入的元素为：" << endl;

    for(auto n : data)

        cout << n << " ";

    cout << endl;

    // 使用反向迭代器输出数据

    cout << endl << "反序输入的元素为：" << endl;

    for(auto riter = data.rbegin(); riter != data.rend(); riter++)

        cout << *riter << " ";

    // 降序排序数据

    cout << endl;

    cout << endl << "你输入的元素降序：*" << endl;

    sort(data.begin(), data.end(), std::greater<int>()); // 排序元素

    for(auto n : data) {

        cout << n << " * ";

    }

    cout << endl;

    // 计算元素的和

    cout << endl << "元素的总和为：" << endl;

    cout << accumulate(data.begin(), data.end(), 0) << endl;

    return 0;

}
```

输入一组空格分隔的非零整数：
输入 0 结束。

你输入的元素为：
10 20 30 40 50 

反序输入的元素为：
50 40 30 20 10 

你输入的元素降序：*
50 * 40 * 30 * 20 * 10 * 

元素的总和为：
150

# 使用 list 容器

来自 `list` 头头文件的 `list<T>` 容器模板实现了一个双向链表。它相比 `vector` 或 `double-deque` 的巨大优势在于可以在常时间内在序列的任何位置插入或删除元素。主要的缺点是 `list` 无法直接通过位置访问元素。当你需要访问元素时，必须从已知位置（通常是开头或末尾）遍历元素。`list` 容器的构造函数范围与 `vector` 或 `double-deque` 相似。此语句创建了一个空列表：

```cpp
list<string> names;
```

你也可以创建一个包含指定数量默认元素的列表：

```cpp
list<string> sayings(20); // 一个包含 20 个空字符串的列表
```

以下是创建一个包含给定数量相同元素的列表的方法：

```cpp
list<double> values(50, 2.71828);
```

这创建了一个包含 50 个 `double` 类型值的列表。

当然，你也可以通过两个迭代器指定的序列中的值来初始化列表：

```cpp
list<double> samples((++begin(values)), --end(values));
```

这根据 `values` 的内容创建一个列表，忽略了 `values` 中的第一个和最后一个元素。注意，`list` 的 `begin()` 和 `end()` 函数返回的迭代器是双向迭代器，因此你不具备支持随机访问迭代器的 `vector` 或 `deque` 容器的灵活性。你只能使用递增或递减运算符更改双向迭代器的值。

与其他序列容器一样，你可以通过调用 `size()` 成员函数获取 `list` 中的元素数量。你也可以通过调用 `resize()` 函数更改 `list` 中的元素数量。从末尾开始；如果参数大于元素数量，将使用存储元素类型的默认构造函数添加元素。

# 向列表中添加元素

你可以通过调用 `push_front()` 或 `push_back()` 向列表的开头或末尾添加元素，就像对 `double-deque` 一样。要在 `list` 内部添加元素，你使用 `insert()` 函数，该函数有三个版本。使用第一个版本，可以在迭代器指定的位置插入新元素：

```cpp
list<int> data(20, 1); // 包含 20 个值为 1 的元素的列表
data.insert(++begin(data), 77); // 将 77 作为第二个元素插入
```

`insert()` 的第一个参数是插入位置的迭代器，第二个参数是要插入的元素。递增运算符作用于 `begin()` 返回的双向迭代器，它指向列表中的第二个元素。执行此此操作后，列表的内容将是：

1 77 1 1 1 1 1 1 1 1 1 1 1 1 1 1

你可以看到列表现在包含了 21 个元素，从插入点开始的元素简单地向右移动了。

你还可以在给定位置插入多个相同元素的拷贝：

```cpp
auto iter = begin(data);
for(int i = 0; i<9; i++)
  ++iter;
data.insert(iter, 3, 88); // 从第10个位置开始插入 3 个 88
```

`iter` 的类型为 `list<int>::iterator`；`insert()` 函数的第一个参数是指定位置的迭代器，第二个参数是要待插入的元素数量，第三个参数是要重复插入的元素。为了到达第十个元素，在 `for` 循环中递增迭代器九次。因此，这从第十个元素开始向列表中插入了三个 88 的拷贝。列表的内容将是：

1 77 1 1 1 1 1 88 88 88 1 1 1 1 1 1 1 1 1

现在列表包含 24 个元素。

以下是如何向列表中插入一个元素序列：

```cpp
vector<int> numbers(10, 5); // 包含 10 个值为 5 的元素的 vector
data.insert(--end(data)), begin(numbers), end(numbers));
```

`insert()` 的第一个参数是一个指向倒数第二个元素的迭代器，`insert()` 函数的第二个参数是要插入的序列，该序列由 `vector` 指定；因此会将 `vector` 中的所有元素插入到列表中，从倒数第二个元素开始。执行此操作后，列表的内容将是：

1 77 1 1 1 1 1 88 88 88 1 1 1 1 1 1 5 5 5 5 5 5 5 1

在倒数第二个元素位置插入来自 `numbers` 的 10 个元素会将列表中的最后两个元素向右移动。列表现在包含 34 个元素。

有三个函数可以就地构造一个元素：`emplace()`，在迭代器指定的位置构造元素；`emplace_front()`，在开头构造元素；以及 `emplace_back()`，在末尾构造元素。以下是它们用例的一些示例：

```cpp
std::list<string> strings;
strings.emplace_back("first");
```

```cpp
string s("second");
strings.emplace_back(std::move(s));
strings.emplace_front("third");
strings.emplace(++begin(strings), "fourth");
```

`emplace_back()` 函数在列表的末尾添加元素，`emplace_front()` 在开头添加元素。`emplace()` 函数在迭代器指定的位置插入元素。

# 访问列表中的元素

你可以通过调用 `front()` 或 `back()` 获取列表的开头或末尾元素，就像对 `double-deque` 一样。要访问列表的内部，必须使用迭代器。`begin()` 和 `end()` 函数返回指向开头和末尾元素之后元素的迭代器。你可以使用范围 `for` 循环遍历列表：

```cpp
for(auto& s : strings) {
    cout << s << endl;
}
```

`rbegin()` 和 `rend()` 函数返回双向迭代器，允许你反向遍历列表。

# 排序列表元素

由于 `list<T>` 容器不提供随机访问迭代器，你无法使用算法头文件中的 `sort()` 函数。`list` 定义了自己的 `sort()` 成员函数，用于升序排序列表。或者，你可以指定一个函数对象或 lambda 表达式来比较元素。例如：

```cpp
strings.sort(greater<string>()); // 降序序列
```

# 尝试使用列表

在这个示例中，你从键盘读取句子并将其存储在列表中：

```cpp
// Ex10_06.cpp
// 使用列表
#include <iostream>
#include <list>
#include <string>
using std::cin;
using std::cout;
using std::endl;
using std::list;
using std::string;
int main()
{
    list<string> text;
    // 读取数据
    cout << "Enter a few lines of text. Just press Enter to end:" << endl;
    string sentence;
    while(getline(cin, sentence, '\n') && !sentence.empty()) {
        text.push_front(sentence);
    }
    // 使用迭代器输出数据
    cout << endl << "In reverse order, here is the text you entered:" << endl;
    for(auto& s : text)
        cout << s << endl;
    // 按升序排序数据
    cout << endl << "In ascending sequence the sentences you entered:" << endl;
    text.sort();
    for(auto& s : text)
        cout << s << endl;
    return 0;
}
```

这是该程序的输出示例：

Enter a few lines of text. Just press Enter to end:
This sentence contains three errors.
This sentence is false.
People who live in glass houses might well answer the door.
If all else fails, read the instructions.
Home is where the mortgage is.

In reverse order, here is the text you entered:
Home is where the mortgage is.
If all else fails, read the instructions.
People who live in glass houses might well answer the door.
This sentence is false.
This sentence contains three errors.

In ascending sequence the sentences you entered:
This sentence contains three errors.
This sentence is false.
People who live in glass houses might well answer the door.
If all else fails, read the instructions.
Home is where the mortgage is.

# 序列容器 | 537

这句话是假的。
这个句子包含三个错误。

在升序序列中，你输入的句子如下：
家是房贷所在的地方。
如果一切都失败了，请阅读说明。
住在玻璃房子里的人不妨去开门。
这个句子包含三个错误。
这句话是假的。

## 工作原理

你首先创建一个列表（list）来存放字符串：

```
list<string> text;
```

然后，你从标准输入流 `cin` 中读取任意数量的文本：

```
string sentence;
while(getline(cin, sentence, '\n'), !sentence.empty())
text.push_front(sentence);
```

这使用了与上一个示例相同的用法。`while` 循环条件中的第二个表达式在循环结束时触发，此时 `empty()` 将返回 `true`。使用 `push_front()` 函数将每个输入添加到列表中，但你同样可以使用 `push_back()`。唯一的区别是列表中元素的顺序将会反转。

编写此代码的更好方法是使用 `emplace` 函数：

```
while(getline(cin, sentence, '\n'), !sentence.empty())
text.emplace_front(std::move(sentence));
```

这将字符串从 `sentence` 移动到列表的开头。这避免了任何拷贝，因此执行速度更快。在每次 `emplace` 之后，`sentence` 对象将变为空。

你在循环中输出列表的内容：

```
for(auto& s : text);
cout << s << endl;
```

最后，你对列表的内容和输出进行排序：

```
sort();
for(auto& s : text);
cout << s << endl;
```

这使用了 `list<string>` 对象的 `sort()` 成员来按升序序列排序内容。如果你想尝试降序序列，请将第一个语句改为：

```
sort(std::greater<string>());
```

不要忘记包含 `<functional>` 头文件。

## 列表的其他操作

`clear()` 函数删除列表中的所有元素。`erase()` 函数允许你按照通常的方式通过单个迭代器删除指定的单个元素，或者通过一对迭代器（序列中的第一个和最后一个[之后]的迭代器）来删除一个元素序列。

```
int data[] = {10, 22, 4, 56, 89, 77, 13, 9};
list<int> numbers(begin(data),end(data));
numbers.erase(+begin(numbers));    // 删除第二个元素
// 删除第一个和最后两个之外的所有元素
numbers.erase(+begin(numbers), --(end(numbers)));
```

最初，列表将包含 `data` 数组中的所有值。第一个 `erase()` 操作删除了第二个元素，因此列表包含：

10 4 56 89 77 13 9

对于第二个 `erase()` 操作，第一个参数是 `begin()` 返回的迭代器加 1，因此它指向第二个元素。第二个参数是 `end()` 返回的迭代器减 2，因此它指向倒数第二个元素。当然，这是序列末尾之后的一个位置，因此该迭代器指向的元素不包含在待删除的集合中，此操作后的列表内容将为：

10 13

`remove()` 函数从列表中删除所有匹配特定值的元素。使用上一个片段定义的 `numbers` 列表，你可以使用以下语句删除所有等于 22 的元素：

```
numbers.remove(22);
```

`assign()` 函数删除列表中的所有元素，并将单个对象拷贝到列表中指定的次数，或者拷贝由两个迭代器指定的对象序列。这里有一个示例：

```cpp
int data[] = {10, 22, 4, 56, 89, 77, 13, 9};
list<int> numbers(begin(data),end(data));
numbers.assign(10, 99);           // 用 10 份 99 替换内容
numbers.assign(data+1, data+4);  // 用 4 56 替换元素 22
```

`assign()` 函数有两个重载版本，如此处所示。第一个版本的参数是待替换元素的数量和要替换元素的值。第二个版本的参数是两个迭代器或两个指针，以你已经见过的的方式指定一个序列。

`unique()` 函数将消除列表中相邻的重复元素，因此，如果你先对内容进行排序，应用该函数可以确保所有元素都是唯一的。这里有一个示例：

# 序列容器 | 539

```
int data[] = {10, 22, 4, 10, 89, 22, 89, 10};
list<int> numbers(begin(data), end(data)); // 10 22 4 10 89 22 89 10
numbers.sort(); // 4 10 10 10 22 22 89 89
numbers.unique(); // 4 10 22 89
```

每个操作的结果显示在注释中。

`splice()` 函数允许你从一个列表中移除全部或部分并插入另一个列表。显然，两个列表必须存储相同类型的元素。这里你可以使用 `splice()` 函数的最简单方法：

```
int data[] = {1, 2, 3, 4, 5, 6, 7, 8};
```
