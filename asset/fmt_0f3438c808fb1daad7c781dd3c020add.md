
在上述代码段中，我们 `#include <stack>` 来包含相应的 STL 头文件。我们还添加了 `using std::stack;` 以从标准命名空间包含栈。现在，在 `main()` 中，我们使用 `stack<Student> studentBody;` 实例化一个包含 `Student` 实例的栈。然后我们调用 `stack:push()` 将几个 `Student` 实例添加到我们的栈中。注意，我们使用的是传统的 `push()` 方法，这有助于栈的 ADT。

然后，我们在栈不为空（`empty()`）时对其进行遍历。我们的目标是使用 `studentBody.top().Print()` 访问并打印栈顶元素。然后我们使用 `stack studentBody.pop()` 整齐地弹出栈顶元素。

Ms. Giselle R. LeBrun id: 299TU GPA: 3.4 Course: C++
Dr. Sara B. Kato id: 272PSU GPA: 3.9 Course: C++
Dr. Hana U. Sato id: 178PSU GPA: 3.8 Course: C++

接下来，让我们研究 STL 队列类以进一步扩展我们的 STL 技能库。

# 使用 STL 队列

STL 队列类实现了队列的 ADT。作为一个典型的队列类，STL 的队列类支持成员插入和删除的先进先出（FIFO）顺序。

回想一下我们在第 6 章“使用继承实现层次结构”中创建了 `Queue` 类；我们使用私有继承从 `LinkedList` 类派生了 `Queue`。STL 队列类使用 `deque` 作为其底层实现（同样使用私有继承）。记住，由于实现手段通过私有继承被隐藏，在以后的日期可以使用另一个数据类型来实现队列，而不会影响其公共接口。STL 队列类是基础顺序容器自适应接口的另一个示例。

让我们来看一组常用的队列成员函数。这远不是完整列表。需要注意的是，队列的公共接口比其私有基类 `deque` 小得多：

| `size_type size() const;` | 返回元素数量 |
| `bool empty() const;` | 如果为空则返回 TRUE |
| `value_type &front();` | 返回头部元素 |
| `const value_type &front() const;` | 返回元素（只读） |
| `value_type &back();` | 返回队尾元素 |
| `const value_type &back() const;` | 返回队尾元素（只读） |
| `void push(const value_type &element);` | 向队尾添加元素 |
| `void pop();` | 从队头部删除元素 |

STL 队列类还包含了重载的 `operator=`（将源队列赋值给目标队列）、`operator==` 和 `operator!=`（两个栈的相等/不相等）、`operator<`、`operator>`、`operator<=` 以及 `operator>=`（栈的比较）。

让我们看看如何利用 STL 栈类。这个示例作为一个完整工作程序的形式在我们的 GitHub 上找到：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter14/Chp14-Ex5.cpp`

```cpp
#include <queue>           // 模板类声明

using std::queue;

int main() {

    queue<Student> studentBody;      // 创建一个栈

    // 向栈添加学生 ("Hana", "Sato", 'Uj', "Dr."

    studentBody.push(Student("Hana", "Sato", 'Uj", "Dr.", 3.8, "C++", "178PSU"));
```

```cpp
studentBody.push(Student("Sara", "Kato", 'B', 'Dr",

3.9, "C++", "272PSU"));

studentBody.push(Student("Giselle", "LeBrun", 'R",

"Ms.", 3.4, "C++", "299TU"));

while (!studentBody.empty()) {

    studentBody.front().Print();

    studentBody.pop();

}

return 0;
```

在上述代码段中，我们 `#include <queue>` 来包含相应的 STL 头文件。我们还添加了 `using std::queue;` 以从标准命名空间包含队列。现在，在 `main()` 中，我们使用 `queue<Student> studentBody;` 实例化一个包含 `Student` 实例的队列。然后我们调用 `queue:push()` 将几个 `Student` 实例添加到我们的栈中。注意，我们使用的是传统的 `push()` 方法，这有助于队列的 ADT。

然后，我们在栈不为空（`empty()`）时对其进行遍历。我们的目标是使用 `studentBody.front().Print()` 访问并打印头部元素。然后我们使用 `queue studentBody.pop()` 整齐地弹出头部元素。

Ms. Giselle R. LeBrun id: 299TU GPA: 3.4 Course: C++
Dr. Sara B. Kato id: 272PSU GPA: 3.9 Course: C++
Dr. Hana U. Sato id: 178PSU GPA: 3.8 Course: C++

接下来，让我们研究 STL 优先级队列类以进一步扩展我们的 STL 技能库。

# 使用 STL 优先级队列

STL 优先级队列类实现了优先级队列的 ADT。作为一个典型的优先级队列类，STL 的优先级队列类支持成员插入和删除的先进先出（FIFO）顺序。

回想一下我们在第 6 章“使用继承实现层次结构”中创建了 `PriorityQueue` 类；我们使用私有继承从 `Queue` 类派生了 `PriorityQueue`。STL 优先级队列类使用 `deque` 作为其底层实现（同样使用私有继承）。记住，由于实现手段通过私有继承被隐藏，在以后的日期可以使用另一个数据类型来实现队列，而不会影响其公共接口。STL 优先级队列类是基础顺序容器自适应接口的另一个示例。

`LinkedList` 的实现，因为 `Queue` 是私有继承自 `LinkedList` 的；我们无法跨越非公开的继承边界进行向上转换。

相比之下，STL 版本的 `priority_queue` 使用 STL `vector` 作为其底层实现。请记住，由于实现方式是隐藏的，`priority_queue` 在此后可以使用其他数据类型实现，而不会影响其公共接口。

STL `priority_queue` 允许检查顶元素，但不允许对其进行修改。STL `priority_queue` 不允许通过元素进行插入。也就是说，元素只能被添加，并形成从大到小的顺序。因此，可以检查顶元素，也可以移除顶元素。

让我们来看一些常用的 `priority_queue` 成员函数。这并不是完整的列表。需要注意的是，`priority_queue` 的公共接口远比其私有基类 `vector` 要小得多：

| `size_type size() const;` | 返回元素数量 |
| `bool empty() const;` | 如果为空则返回 TRUE |
| `const value_type top() const;` | 返回顶元素（只读） |
| `void push(const value_type& element);` | 在末尾添加一个元素 |
| `void pop();` | 从前端移除一个元素 |
| `void emplacement(args);` | 使用 args 构建一个新元素并添加 |

与之前检查的容器类不同，STL `priority_queue` 不重载运算符，包括 `operator=`、`operator==` 等。

`priority_queue` 最有趣的方法是 `void emplacement(args)`。该成员函数允许优先级入队机制向此 ADT（抽象数据类型）添加项。我们还注意到，必须使用 `top()` 来返回顶元素（区别于 `queue` 使用的 `front()`）。但话又回来，STL `priority_queue` 是使用 `queue` 实现的。为了使用 `priority_queue`，我们像使用 `queue` 一样 `#include <queue>`。

由于 `priority_queue` 的用法与 `queue` 非常相似，我们将在本章末尾的习题中从编程角度的角度进一步探索它。

现在我们已经看到了 STL 中许多顺序容器类型的示例（包括自适应接口），让我们来研究 STL 的 `map` 类，这是一种关联容器。

## 检查 STL map

STL `map` 类实现了哈希表（hash table）的抽象数据类型。`map` 类允许使用键（key）或索引快速存储和检索哈希表或 map 中的元素。键可以是数值或任何其他数据类型。一个键只能与一个值元素关联。然而，如果有多个数据需要与同一个键关联，则可以使用 STL 容器 `multimap`。

哈希表（maps）在数据存储和查找方面非常快。其性能保证为 $O(\log(n))$。STL `map` 被认为是一种关联容器，因为它将键与值关联起来以便快速检索值。

让我们来看一些常用的 `map` 成员函数。这并不是完整的列表：

| `bool empty() const;` | 如果为空则返回 TRUE，否则返回 FALSE |
| `size_type size() const;` | 返回元素数量 |
| `void clear();` | 清空 map |
| `size_type erase(const key_type &k);` | 删除键为 k 的元素 |
| `iterator erase(const iterator pos);` | 删除迭代器位置的元素 |
| `void swap(map &map);` | 交换两个 map 的内容 |
| `iterator insert(iterator pos, const value_type &val);` | 在 pos 处插入 val |
| `iterator begin();` | 返回指向第一个元素的迭代器 |
| `iterator end();` | 返回指向末尾之后的迭代器 |
| `iterator find(const key_type &k);` | 查找键为 k 的元素 |

STL `map` 类还额外包含了重载的运算符 `operator==`（逐个元素比较 map），该运算符被实现为全局函数。STL `map` 还包含了重载的运算符 `operator[]`（返回与用作索引的键关联的 map 元素的引用；这是可写内存）。

让我们来看看如何利用 STL `map` 类。你可以在我们的 GitHub 上找到此示例的完整程序，如下：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter14/Chp14-Ex7.cpp`

```cpp
#include <map>

using std::map;

using std::pair;

bool operator<(const Student &s1, const Student &s2)

{

    // 我们需要重载运算符来比较 Students

    return s1.GetGpa() < s2.GetGpa();

}

int main()

{

    Student s1("Hana", "Lo", "U", "Dr.", 3.8, "C++", "178UD");

    Student s2("Alice", "Li", "B", "Dr.", 3.9, "C++", "272UD");

    Student s3("Rui", "Qi", "R", "Ms.", 3.4, "C++", "299TU");

    Student s4("Jiang", "Wu", "C", "Ms.", 3.8, "C++", "887TU");

    // 创建三组到 Students 的键对

    pair<string, Student> studentPair1(

            s1.GetStudentId(), s1);

    pair<string, Student> studentPair2(

            s2.GetStudentId(), s2);

    pair<string, Student> studentPair3(

            s3.GetStudentId(), s3);

    // 创建 string 到 Student 的 map

    map<string, Student> studentBody;

    // 将三个键对插入 map 中

    studentBody.insert(studentPair1);

    studentBody.insert(studentPair2);

    studentBody.insert(studentPair3);

    // 使用 operator[] 将第四个学生插入 map

    studentBody[s4.GetStudentId()] = s4;

    // 使用 range-for 循环遍历 map

    for (auto &[id, student] : studentBody) {

        cout << id << " " << student.GetFirstName() << endl;

    }

    // 使用迭代器遍历

    map<string, Student>::iterator mapIter;

    mapIter = studentBody.begin();

    while (mapIter != studentBody.end())

    {

        // 将 temp 设置为当前对元素

        pair<string, Student> temp = *mapIter;

        // 设置 tempS 为 Student 的临时引用

        Student &tempS = temp.second;

        // 打印 studentId 和 firstName

        cout << temp.first << " " << tempS.GetFirstName() << endl;

        // 迭代器自增

        ++mapIter;

    }

    return 0;

}
```

我们将迭代的数据类型。括号 `([1])` 将解构元对，并将迭代元素分别绑定到 `id` 和 `student` 标识符。注意，我们现在可以如此轻松地遍历 `studentBody` 映射。

让我们来看看这个程序的输出结果：

```
178UD Hana Lo
272UD Ali Li
299TU Rui Qi
887TU Jiang Wu
178UD Hana Lo
272UD Ali Li
299TU Rui Qi
887TU Jiang Wu
```

接下来，让我们来看另一种使用 STL map 的替代方案，这将向我们引入 STL 函数对象（functor）的概念。

## 使用函数对象检查 STL map

STL map 具有很高的灵活性，就像许多 STL 类一样。在之前的 map 示例中，我们假设 `Student` 类中存在比较方法。毕竟，我们已经为两个 `Student` 实例重载了 `operator<`。然而，如果我们无法修改没有提供此重载运算符的类，而且我们也不选择作为外部函数来重载 `operator<`，会发生什么呢？

幸运的是，在实例化 map 或 map 迭代器时，我们可以为模板展开指定第三种数据类型。这个额外的数据类型是一个特定的类类型，被称为函数对象（functor）。函数对象是一个可以被视为函数或函数指针的对象。我们将创建一个类（或结构体）来表示我们的函数对象类型，并在该类（或结构体）内部，我们必须重载 `operator()`。我们将在重载的 `operator()` 中为相关对象提供比较方法。函数对象本质上是通过重载 `operator()` 来封装一个函数指针。

让我们来看看可能如何修改 map 示例以使用简单的函数对象。我们可以在 GitHub 上找到该示例的完整运行程序，地址如下：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter14/Chp14-Ex8.cpp`

```cpp
#include <map>

using std::map;

using std::pair;

struct comparison    // 这个结构体代表一个'函数对象'

{    // 即，一个'函数对象'

    bool operator()(const string &key1,

                  const string &key2) const

    {

        int ans = key1.compare(key2);

        if (ans >= 0) return true;    // 返回布尔值

        else return false;

    }

    // 默认构造函数和析构函数足够

};

int main()
{
```
