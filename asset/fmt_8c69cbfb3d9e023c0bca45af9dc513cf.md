
```
// to the preferred range-for loop for further beyond

for (int i = 0; i < studentBody1.size(); i++)

    studentBody1[i].print(); // print first vector

studentBody2 = studentBody1; // assign one to another

if (studentBody1 == studentBody2)

    cout << "Vectors are the same" << endl;

// Notice: auto keyword specifies iterator declaration

for (auto iter = studentBody2.begin();

    iter != studentBody2.end(); iter++)

    (*iter).EarnPhD();

// Preferred range-for loop (and to simplify type)

for (const auto &student : studentBody2)

    student.print();

if (!studentBody1.empty()) // clear first vector

    studentBody1.clear();
```

在之前列出的代码段中，我们 `#include <vector>` 来包含相应的 STL 头文件。我们还添加了 `std::vector;` 以从标准命名空间包含 vector。现在，在 `main()` 中，我们使用 `vector<Student> studentBody1, studentBody2;` 实例化两个 vector。然后，我们可以使用 `vector::push_back()` 方法连续向我们的第一个 vector 中添加多个 `Student` 实例。再次注意，这些 `Student` 实例在 `main()` 中是匿名对象。没有引用它们的局部标识符 – 它们仅是为了放入我们的 vector 而创建的，这在插入时会创建每个实例的本地副本。一旦我们的 vector 中有了元素，我们就会遍历第一个 vector，使用 `studentBody1[i].print();` 打印每个 `Student`。

接下来，我们通过使用 `studentBody1 = studentBody2;` 将一个 vector 赋值给另一个，演示 vector 的重载赋值运算符。在这里，我们在赋值时进行了从右到左的深拷贝。然后我们可以在条件语句中使用重载的比较运算符测试两个 vector 是否相等，即 `if (studentBody1 == studentBody2)`。

然后，我们使用带有迭代器 `auto iter = studentBody2.begin();` 的 `for` 循环，对第二个 vector 的内容应用 `EarnPhD()`。`auto` 关键字允许通过其初始用法来确定迭代器的类型。接着，我们使用首选的 range-for 循环打印第二个 vector 的内容（同时使用 `auto` 简化了 range-for 循环中的变量）。最后，我们检查第一个 vector，测试它是否为空 `empty()`，然后使用 `studentBody1.clear();` 逐个清除元素。我们现在已经了解了 vector 方法及其功能。

让我们来看看这个程序的输出：

```
Dr. Hana U. Sato with id: 178PSU GPA: 3.8 Course: C++

Dr. Sara B. Kato with id: 272PSU GPA: 3.9 Course: C++

Ms. Giselle R. LeBrun with id: 299PSU GPA: 3.4 Course: C++

Vectors are the same

Everyone to earn a PhD

Dr. Hana U. Sato with id: 178PSU GPA: 3.8 Course: C++

Dr. Sara B. Kato with id: 272PSU GPA: 3.9 Course: C++

Dr. Giselle R. LeBrun with id: 299PSU GPA: 3.4 Course: C++
```

### 使用 STL deque

STL `deque` 类（读音为 *deck*）实现了双端队列的抽象数据类型。这种 ADT 扩展了队列是先进先出的概念。相反，`deque` 类提供了更大的灵活性。在 `deque` 的两端添加元素是非常快速的。在 `deque` 的中间添加元素是耗时的。你可能认为 `deque` 是一个顺序容器，尽管它是 `list` 的特化版本。让我们来看看常见的 `deque` 函数：

| method | description |
| :--- | :--- |
| `iterator begin();` | 返回指向第一个元素的迭代器 |
| `iterator end();` | 返回指向最后一个元素的迭代器 |
| `size_type size() const;` | 返回元素数量 |
| `void push_back(const value_type &element);` | 在末尾添加元素 |
| `void push_front(const value_type &element);` | 在头部添加元素 |
| `void pop_back();` | 从末尾移除元素 |
| `void pop_front();` | 从头部移除元素 |
| `bool empty() const;` | 如果 vector 为空则返回 TRUE |
| `void clear();` | 清除 vector 中的所有元素 |

STL `deque` 类还额外重载了运算符 `operator=`（赋值将用源 vector 替换目标 vector）、`operator==`（vector 之间的比较，逐个元素比较）以及 `operator[]`（返回请求位置的引用，即可写内存）。

```cpp
#include <deque>

using std::deque;

int main() {
// instantiate two vectors
deque<Student> studentBody1, studentBody2;
// add 3 Students, which are anonymous objects
studentBody.push_back(Student("Hana", "Sato", 'U',"Dr.", 3.8, "C++", "178PSU"));
studentBody1.push_back(Student("Sara", "Kato", 'B',"Dr.", 3.9, "C++", "272PSU"));
studentBody1.push_back(Student("Giselle", "LeBrun",'R', "Ms.", 3.4, "C++", "299TU"));
// Compare this to next loop using an iterator and
// to the preferred range-for loop for further beyond
for (int i = 0; i < studentBody1.size(); i++)
    studentBody1[i].print(); // print first vector
studentBody2 = studentBody1; // assign one to another
if (studentBody1 == studentBody2)
    cout << "Vectors are the same" << endl;
// Notice: auto keyword specifies iterator declaration
for (auto iter = studentBody2.begin();
    iter != studentBody2.end(); iter++)
    (*iter).EarnPhD();
// Preferred range-for loop (and to simplify type)
for (const auto &student : studentBody2)
    student.print();
if (!studentBody1.empty()) // clear first vector
    studentBody1.clear();
}
```

在之前列出的代码段中，我们 `#include <vector>` 来包含相应的 STL 头文件。我们还添加了 `std::deque;` 以从标准命名空间包含 deque。现在，在 `main()` 中，我们使用 `vector<Student> studentBody1, studentBody2;` 实例化两个 vector。我们可以使用 `vector::push_back()` 方法连续向我们的第一个 vector 中添加多个 `Student` 实例。再次注意，这些 `Student` 实例在 `main()` 中是匿名对象。没有引用它们的局部标识符 – 它们仅是为了放入我们的 vector 而创建的，这在插入时会创建每个实例的本地副本。一旦我们的 vector 中有了元素，我们就会遍历第一个 vector，使用 `studentBody1[i].print();` 打印每个 `Student`。

该接口不公开其底层实现。毕竟，栈（stack）可能会改变其实现；ADT（抽象数据类型）的使用不应以任何方式依赖其底层实现。STL 栈被视为基础顺序容器的自适应接口。

回想一下我们在第 6 章“使用继承实现层次结构”中创建了自己的栈类，并使用了 `LinkedList` 作为私有基类。STL 版本会更详尽；有趣的是，它是使用 `deque` 作为其底层私有基类的。通过将 `deque` 作为 STL 栈的私有基类，`deque` 更通用的底层能力被隐藏了；仅使用适用于的方法来实现栈的公共接口。此外，由于实现手段是隐藏的，在以后的日期可以使用另一个容器类来实现栈，而不会影响其使用。

让我们来看一组常用的栈成员函数。这远不是完整列表。需要注意的是，栈的公共接口比其私有基类 `deque` 小得多：

```
size_type size() const;               返回元素数量
void push(const value_type &element);  向栈顶添加元素
void pop();                         从栈顶删除元素
bool empty() const;                 如果为空则返回 TRUE
value_type &top();                返回栈顶元素
const value_type &top() const;      返回栈顶元素（只读）
```

STL 栈类还包含了重载的 `operator=`（将源栈赋值给目标栈）、`operator==` 和 `operator!=`（两个栈的相等/不相等）、`operator<`、`operator>`、`operator<=` 以及 `operator>=`（栈的比较）。

让我们看看如何利用 STL 栈类。这个示例作为一个完整工作程序的形式在我们的 GitHub 上找到：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter14/Chp14-Ex5.cpp`

```cpp
#include <stack>           // 模板类声明
using std::stack;
int main() {
    stack<Student> studentBody;      // 创建一个栈
    // 向栈添加学生 ("Hana", "Sato", 'Uj', "Dr."
    studentBody.push(Student("Hana", "Sato", 'Uj', "Dr.", 3.8, "C++", "178PSU"));
```

```cpp
studentBody.push(Student("Sara", "Kato", 'B', 'Dr",3.9, "C++", "272PSU"));
studentBody.push(Student("Giselle", "LeBrun", 'R',"Ms.", 3.4, "C++", "299TU"));
while (!studentBody.empty()) {
    studentBody.top().Print();
    studentBody.pop();
}
return 0;
```
