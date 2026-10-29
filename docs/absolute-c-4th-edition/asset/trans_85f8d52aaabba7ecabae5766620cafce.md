

成员函数 `begin()` 用于将迭代器定位到容器中的第一个元素。对于 vector 以及许多其他容器类，成员函数 `begin()` 返回一个位于第一个元素的迭代器。（对于 vector v，第一个元素是 `v[0]`。）因此，

```
iterator p = v.begin( );
```

将迭代器变量 p 初始化为一个位于第一个元素的迭代器。因此，遍历 vector v 的所有元素的基本 for 循环为

```
iterator p;
for (p = v.begin( ); Boolean_Expression; p++)
    Action_At_Location p;
```

所需的停止条件是

```
p = v.end( )
```

成员函数 `end()` 返回一个哨兵值，可用于检查迭代器是否已越过最后一个元素。如果 p 位于最后一个元素，那么在 `p++` 之后，测试 `p = v.end()` 会从 false 变为 true。因此，正确的 `Boolean_Expression` 是这个停止条件的否定：

```
iterator p;
for (p = v.begin( ); p != v.end( ); p++)
    Action_At_Location p;
```

注意，`p != v.end()` 直到 p 的位置越过最后一个元素之后才会从 true 变为 false。因此，`v.end()` 并不位于任何元素上。`v.end()` 是一个特殊值，用作哨兵。它不是迭代器，但你可以使用 `==` 和 `!=` 将 `v.end()` 与迭代器进行比较。`v.end()` 类似于用来标记第 17 章讨论的那种链表结尾的 `NULL` 值。

下面来自 Display 19.1 的 for 循环使用了相同的技术，容器名为 container：

```
iterator p;
for (p = container.begin( ); p != container.end( ); p++)
    cout << *p << " ";
```

在迭代器 p 的位置执行的动作是

```
cout << *p << " ";
```

解引用运算符 `*` 已针对 STL 容器迭代器进行了重载，因此 `*p` 会生成位置 p 处的元素。具体来说，对于 vector 容器，`*p` 生成位于迭代器 p 处的元素。因此，上面的 cout 语句输出位于迭代器 p 处的元素，所以整个 for 循环输出了 vector 容器中的所有元素。

解引用运算符 `*p` 总是生成位于迭代器 p 处的元素。在某些情况下，`*p` 提供只读访问，不允许你更改元素。在其他情况下，它允许你访问该元素并允许你更改元素。对于 vector，`*p` 允许你更改位于 p 处的元素，如下面来自 Display 19.1 的 for 循环所示：

```
for (p = container.begin(); p != container.end(); p++)
    *p = 0;
```

这个 for 循环遍历 vector 容器中的所有元素，并将所有元素更改为 0。

## 迭代器

迭代器是一种对象，可配合容器使用以访问容器中的元素。迭代器是指针概念的泛化。运算符 `==`、`!=`、`++` 和 `--` 对迭代器的行为与对指针的行为相同。迭代器如何遍历容器中所有元素的基本轮廓如下：

```
iterator p;
for (p = container.begin(); p != container.end(); p++)
    Process_Element_At_location p;
```

成员函数 `begin()` 返回一个位于第一个元素的迭代器。成员函数 `end()` 返回一个值，一旦迭代越过容器中的最后一个元素，该值就充当哨兵值。

## 解引用

解引用运算符 `*p` 在应用于迭代器 p 时，生成位于迭代器 p 处的元素。在某些情况下，`*p` 提供只读访问，不允许你更改元素。在其他情况下，它允许你访问该元素并允许你更改元素。

## 自测练习

- 1. 如果 v 是一个 vector，`v.begin()` 返回什么？`v.end()` 返回什么？
- 2. 如果 p 是 vector 对象 v 的迭代器，`*p` 是什么？
- 3. 假设 v 是一个 int 类型的 vector。编写一个 for 循环，输出除第一个元素之外的所有元素。

## 迭代器的种类

不同的容器具有不同种类的迭代器。迭代器根据可对它们执行的操作类型进行分类。vector 迭代器是最通用的形式；也就是说，所有操作都适用于 vector 迭代器。因此，我们将再次使用 vector 容器来演示迭代器。在这种情况下，我们使用 vector 来演示*递减*和*随机访问*迭代器操作。Display 19.2 显示了另一个使用名为 container 的 vector 对象和迭代器 p 的程序。

递减运算符用于 Display 19.2 的第 30 行。正如你所期望的，`p--` 将迭代器 p 移动到前一个位置。递减运算符 `--` 类似于递增运算符 `++`，但它向相反方向移动迭代器。

```
//Program to demonstrate bidirectional and random-access iterators.
#include <iostream>
#include <vector>
using std::cout;
using std::endl;
using std::vector;
using std::vector<char>::iterator;

int main( )
{
    vector<char> container;

    container.push_back('A');
    container.push_back('B');
    container.push_back('C');
    container.push_back('D');

    for (int i = 0; i < 4; i++)
        cout << container[i] << " " << endl;

    iterator p = container.begin( );
    cout << "The third entry is " << container[2] << endl;
    cout << "The third entry is " << p[2] << endl;
    cout << "The third entry is " << *(p + 2) << endl;

    cout << "Back to container[0].\n";
    p = container.begin( );
    cout << "which has value " << *p << endl;

    cout << "Two steps forward and one step back:\n";
    p++;
    cout << *p << endl;
}
```

*同一事物的三种不同表示法*

*这种表示法专门用于 vector 和数组。*

*这两种适用于任何随机访问迭代器。*

## Display 19.2 双向和随机访问迭代器的使用（第 2 部分，共 2 部分）

```
28  p++;
29  cout << *p << endl;
30  p--;
31  cout << *p << endl;
32
33 }
```

> 这适用于任何双向迭代器。

## 示例对话

```
container[0] == A
container[1] == B
container[2] == C
container[3] == D
The third entry is C
The third entry is C
The third entry is C
Back to container[0].
which has value A
Two steps forward and one step back:
B
C
B
```

递增和递减运算符可以用于前缀（`++p`）或后缀（`p++`）表示法。除了改变 p 之外，它们还返回一个值。返回值的具体细节与 int 变量上的递增和递减运算符完全类似。在前缀表示法中，先更改变量，然后返回更改后的值。在后缀表示法中，先返回值，然后再更改变量。我们倾向于不使用递增和递减运算符作为返回值的表达式；我们只用它们来更改变量的值。

Display 19.2 中的以下几行说明，使用 vector 迭代器，你可以随机访问 vector（如 container）的元素：

```
iterator p = container.begin();
cout << "The third entry is " << container[2] << endl;
cout << "The third entry is " << p[2] << endl;
cout << "The third entry is " << *(p + 2) << endl;
```

随机访问意味着你可以一步直接到达任何特定元素。我们已经使用 `container[2]` 作为对 vector 的一种随机访问形式。这只是数组和 vector 标准的方括号运算符。新的地方在于你可以对迭代器使用相同的方括号表示法。表达式 `p[2]` 是一种访问索引为 2 的元素的方式。

表达式 `p[2]` 和 `*(p + 2)` 完全等价。类似于指针算术（参见第 10 章），`(p + 2)` 表示 p 之后两个位置的位置。由于在前面的代码中 p 位于第一个（索引 0）位置，因此 `(p + 2)` 位于第三个（索引 2）位置。表达式 `(p + 2)` 返回一个迭代器。表达式 `*(p + 2)` 解引用该迭代器。当然，你可以将 2 替换为不同的非负整数，以获得指向不同元素的指针。

请务必注意，`p[2]` 和 `(p + 2)` 都不会改变迭代器变量 p 中迭代器的值。表达式 `(p + 2)` 返回另一个位置的另一个迭代器，但它将 p 留在原处。类似的情况在 `p[2]` 背后也会发生。还要注意，`p[2]` 和 `(p + 2)` 的含义取决于 p 中迭代器的位置。例如，`(p + 2)` 表示 p 位置之后两个位置的位置，无论 p 在哪里。

例如，假设将前面 Display 19.2 中的代码替换为以下代码（注意添加了 `p++`）：

```
iterator p = container.begin( );
p++;
cout << "The third entry is " << container[2] << endl;
cout << "The third entry is " << p[2] << endl;
cout << "The third entry is " << *(p + 2) << endl;
```

这三个 cout 的输出将不再是

```
The third entry is C
The third entry is C
The third entry is C
```

而是

```
The third entry is C
The third entry is D
The third entry is D
```

`p++` 将 p 从位置 0 移动到位置 1，因此 `(p + 2)` 现在是位置 3 的迭代器，而不是位置 2。所以，`*(p + 2)` 和 `p[2]` 等价于 `container[3]`，而不是 `container[2]`。

我们现在已经足够了解如何操作迭代器，从而可以理解迭代器是如何分类的。迭代器的主要种类如下。

- *前向迭代器*：`++` 可作用于该迭代器。
- *双向迭代器*：`++` 和 `--` 都可作用于该迭代器。
- *随机访问迭代器*：`++`、`--` 和随机访问都可作用于该迭代器。

注意，这些是逐级增强的类别：每个随机访问迭代器也是双向迭代器，每个双向迭代器也是前向迭代器。

正如我们将看到的，不同的模板容器类具有不同种类的迭代器。vector 模板类的迭代器是随机访问迭代器。

