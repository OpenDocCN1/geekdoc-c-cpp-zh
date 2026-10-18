
# 程序清单18.1 与 vector 一起使用的迭代器

```
//Program to demonstrate STL iterators.
#include <iostream>
#include <vector>
using std::cout;
using std::endl;
using std::vector;
int main()
{
    vector<int> container;
    for (int i = 1; i <= 4; i++)
        container.push_back(i);
    cout << "Here is what is in the container:\n";
    vector<int>::iterator p;
    for (p = container.begin(); p != container.end(); p++)
        cout << *p << " ";
    cout << endl;
    cout << "Setting entries to 0:\n";
    for (p = container.begin(); p != container.end(); p++)
        *p = 0;
    cout << "Container now contains:\n";
    for (p = container.begin(); p != container.end(); p++)
        cout << *p << " ";
    cout << endl;
    return 0;
}
```

## 示例对话

```
Here is what is in the container:
1 2 3 4
Setting entries to 0:
Container now contains:
0 0 0 0
```

由于 vector 的定义将名称 vector 放入 std 命名空间，因此完整的 using 声明是

```
using std::vector<int>::iterator;
```

以下来自程序清单18.1的代码行说明了迭代器与 vector（或任何容器类）的基本用法：

```
vector<int>::iterator p;
for (p = container.begin(); p != container.end(); p++)
    cout << *p << " ";
```

请记住，container 的类型是 vector<int>。

可以将 vector v 想象为其数据元素的线性排列。有第一个数据元素 v[0]、第二个数据元素 v[1]，依此类推。迭代器 p 是一个可以定位在这些元素之一上的对象。（可以把 p 想象为指向这些元素之一。）迭代器可以将其位置从一个元素移动到另一个元素。如果 p 定位在，比如说，v[7] 处，那么 p++ 会将 p 移动到 v[8] 处。这允许迭代器从第一个元素移动到最后一个元素遍历整个 vector，但它需要找到第一个元素，并且需要知道何时已经到达最后一个元素。

使用运算符 ==，可以判断一个迭代器是否与另一个迭代器位于相同位置。因此，如果你有一个指向第一个、最后一个或其他元素的迭代器，就可以测试另一个迭代器，看它是否位于第一个、最后一个或其他元素处。

如果 p1 和 p2 是两个迭代器，那么比较

p1 == p2

当且仅当 p1 和 p2 位于同一元素时为真。（这与指针类似。如果 p1 和 p2 是指针，那么当它们指向同一事物时，该比较为真。）和通常一样，!= 就是 == 的否定，因此

p1 != p2

当 p1 和 p2 不在同一元素位置时为真。

成员函数 begin() 用于将迭代器定位到容器中的第一个元素。对于 vector 以及许多其他容器类，成员函数 begin() 返回一个位于第一个元素的迭代器。（对于 vector v，第一个元素是 v[0]。）因此，

vector<int>::iterator p = v.begin();

将迭代器变量 p 初始化为一个位于第一个元素的迭代器。因此，用于访问 vector v 中所有元素的基本 for 循环是

vector<int>::iterator p;
for (p = v.begin(); Boolean_Expression; p++)
    Action_At_Location p;

所需的用于停止条件的 Boolean_Expression 是

p == v.end()

成员函数 end() 返回一个哨兵值，可以检查该值以判断迭代器是否已越过最后一个元素。如果 p 位于最后一个元素处，那么在执行 p++ 之后，测试 p == v.end() 会从 false 变为 true。因此，带有正确 Boolean_Expression 的 for 循环是

vector<int>::iterator p;
for (p = v.begin(); p != v.end(); p++)
    Action_At_Location p;

注意，p != v.end() 并不会在 p 的位置越过最后一个元素之前从 true 变为 false。因此，v.end() 不位于任何元素处。v.end() 是一个特殊值，用作哨兵值。它不是普通的迭代器，但你可以使用 == 和 != 将 v.end() 与迭代器进行比较。v.end() 类似于第13章中讨论的用于标记链表末尾的 NULL 值。

以下来自程序清单18.1的 for 循环使用这一精确技术，该循环使用名为 container 的 vector：

```
vector<int>::iterator p;
for (p = container.begin(); p != container.end(); p++)
    cout << *p << " ";
```

在迭代器 p 所在位置执行的操作是

```
cout << *p << " ";
```

解引用运算符 * 对 STL 容器迭代器进行了重载，因此 *p 产生 p 位置的元素。特别是，对于 vector 容器，*p 产生位于迭代器 p 处的元素。因此，上面的 cout 语句输出位于迭代器 p 处的元素，整个 for 循环输出 vector 容器中的所有元素。

解引用运算符 *p 总是产生位于迭代器 p 处的元素。在某些情况下，*p 提供只读访问，不允许你修改元素。在其他情况下，它允许你访问元素并修改它。对于 vector，*p 允许你修改 p 处的元素，如下面来自程序清单18.1的 for 循环所示：

```
for (p = container.begin(); p != container.end(); p++)
    *p = 0;
```

这个 for 循环遍历 vector 容器中的所有元素，并将所有元素改为 0。

## 编程技巧 使用 auto 简化变量声明

在处理模板和迭代器时，auto 关键字可以让你的代码更具可读性。声明迭代器可能非常冗长：

```
vector<int>::iterator p = v.begin();
```

使用 auto 可以更简洁地完成同样的事情：

```
auto p = v.begin();
```

## 陷阱 编译器问题

有些编译器在迭代器声明方面存在问题。你可以用不同的方式声明迭代器。例如，我们一直在使用以下方式：

```
using std::vector;
...
vector<char>::iterator p;
```

### 迭代器

迭代器是一种对象，可以与容器一起使用，以访问容器中的元素。迭代器是指针概念的概括，运算符 ==、!=、++ 和 -- 对迭代器的行为与对指针的行为相同。迭代器遍历容器中所有元素的基本框架是

```
STL_Container<type>::iterator p;
for (p = container.begin(); p != container.end(); p++)
    Process_Element_At_Location p;
```

STL_Container 是容器类的名称（例如 vector），type 是要存储项的数据类型。成员函数 begin() 返回一个位于第一个元素的迭代器。成员函数 end() 返回一个值，该值作为位于容器最后一个元素之后一个位置的哨兵值。

或者，如果你的代码只使用一种类型的迭代器，可以使用以下方式：

```
using std::vector<char>::iterator;
. . .
iterator p;
```

你也可以使用以下方式，但这种方式不太好，因为它将 std 命名空间中的所有名称引入当前声明区域，增加了名称冲突的可能性。

```
using namespace std;
. . .
vector<char>::iterator p;
```

还有其他类似的变体。你的编译器应该接受这些备选方案中的任何一种。然而，我们发现有些编译器只接受其中某些方案。如果一种形式不适用于你的编译器，请尝试另一种。

## 解引用

解引用运算符 *p 在应用于迭代器 p 时，产生位于迭代器 p 处的元素。对于某些 STL 容器类，*p 提供只读访问，不允许你修改元素。对于其他 STL 容器类，它允许你访问元素并修改它。

## 自测练习

- 1. 如果 v 是一个 vector，v.begin() 返回什么？v.end() 返回什么？
- 2. 如果 p 是 vector 对象 v 的迭代器，*p 是什么？
- 3. 假设 v 是 int 类型的 vector。编写一个 for 循环，输出 v 中除第一个元素之外的所有元素。

## 迭代器的种类

不同的容器有不同种类的迭代器。迭代器根据可对其执行的操作种类进行分类。vector 迭代器是最通用的形式；也就是说，所有操作都适用于 vector 迭代器。因此，我们将再次使用 vector 容器来说明迭代器。在这种情况下，我们使用 vector 来说明递减和随机访问的迭代器运算符。程序清单18.2 显示了另一个使用名为 container 的 vector 对象和迭代器 p 的程序。

## 程序清单18.2 双向迭代器和随机访问迭代器的使用（第1部分，共2部分）

```
//Program to demonstrate bidirectional and random access iterators.
#include <iostream>
#include <vector>
using std::cout;
using std::endl;
using std::vector;

int main()
{
    vector<char> container;
    container.push_back('A');
    container.push_back('B');
    container.push_back('C');
    container.push_back('D');

    for (int i = 0; i < 4; i++)
        cout << "container[" << i << "] == " << container[i] << endl;
    vector<char>::iterator p = container.begin();
    cout << "The third entry is " << container[2] << endl;
    cout << "The third entry is " << p[2] << endl;
    cout << "The third entry is " << *(p + 2) << endl;

    cout << "Back to container[0].\n";
    p = container.begin();
    cout << "which has value " << *p << endl;
```

同一事物的三种不同表示法。

这种表示法专用于 vector 和数组。

这两种适用于任何随机访问迭代器。

