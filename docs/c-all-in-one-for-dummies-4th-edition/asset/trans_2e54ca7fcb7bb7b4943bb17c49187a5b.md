
要向列表中添加项，请使用该列表的 `push_front()` 方法或 `push_back()` 方法。`push_front()` 函数会将项插入列表开头，位于当前列表中所有其他项之前。如果连续多次使用 `push_front()`，项的顺序将与你放入它们的顺序相反。`push_back()` 函数会将项添加到列表末尾。因此，如果使用 `push_back()` 将项放入列表，它们的顺序将与你添加它们的顺序相同。使用 `insert()` 和 `splice()` 可以将项放到列表中的其他位置。你使用迭代器找到想要的位置，然后在该位置拼接新项。

![](img/128ab511de4e7360e167e3b15cdd5dd0_684_0.png)

对于需要指向列表中某项的指针的操作，你需要使用迭代器。*迭代器* 只是指向列表中某项的指针的 typedef；不过，它指向的是列表中的项，而不是你添加到列表中的原始项。记住，容器保存的是副本。因此，如果你对列表执行 `insert()` 并指向一个原始项，该项不会成为列表的成员，`insert()` 也不会起作用。

![](img/128ab511de4e7360e167e3b15cdd5dd0_684_1.png)

尽管 list 模板包含 `insert()` 函数，但这个函数只有非常特殊的用途。要使用 `insert()`，你必须有一个指向列表中某项的指针——也就是说，你需要有一个通过遍历列表获得的迭代器。它没有 `find()` 函数，因此实际上你唯一会使用 `insert()` 函数的时候，是你已经在沿着列表逐步操作的时候。但如果你确实需要执行插入，并且愿意使用迭代器在列表中移动以找到想要放置新项的位置，`insert()` 就能完成这项工作。

Lists 示例（如代码清单 6–12 所示）使用鸭子比喻（即让你的所有鸭子排好队）来演示列表。这个示例创建一个列表，添加鸭子，然后将其反转。接下来，代码创建第二个列表，并将其成员拼接到第一个列表中。

### 代码清单 6-12：处理列表模板中的项

```cpp
#include <iostream>
#include <list>

using namespace std;

class Duck {
public:
  string name;
  int weight;
  int length;
};

ostream& operator << (ostream &out, const Duck &duck) {
    out << "(" << duck.name;
    out << ", " << duck.weight;
    out << ", " << duck.length;
    out << ")";
    return out;
}

void Dump(list<Duck> *mylist) {
    list<Duck>::iterator iter = mylist->begin();
    while (iter != mylist->end())
    {
        cout << *iter << endl;
        iter++;
    }
}

list<Duck>::iterator Move(list<Duck> *mylist, int pos) {
    list<Duck>::iterator res = mylist->begin();
    for (int loop = 1; loop <= pos; loop++)
    {
        res++;
    }
    return res;
}

bool operator < (const Duck& first, const Duck& second) {
    return first.name < second.name;
}

int main() {
    list<Duck> Inarow;

    // Push some at the beginning
    Duck d1 = {"Jim", 20, 15}; // Braces notation!
    Inarow.push_front(d1);
    Duck d2 = {"Sally", 15, 12};
    Inarow.push_front(d2);

    // Push some at the end
    Duck d3 = {"Betty", 18, 25};
    Inarow.push_front(d3);
    Duck d4 = {"Arnold", 19, 26};
    Inarow.push_front(d4);

    // Display the ducks
    cout << "===Ducks===" << endl;
    Dump(&Inarow);

    // Reverse
    Inarow.reverse();
    cout << "\n===Reversed===" << endl;
    Dump(&Inarow);

    // Create the second list.
    list<Duck> extras;
    Duck d5 = {"Grumpy", 8, 8};
    extras.push_back(d5);
    Duck d6 = {"Sleepy", 8, 8};
    extras.push_back(d6);

    // Display the extras list.
    cout << "\n===Extras===" << endl;
    Dump(&extras);

    // Determine the positions.
    list<Duck>::iterator first = Move(&extras, 0);
    list<Duck>::iterator last = Move(&extras, 2);
    list<Duck>::iterator into = Move(&Inarow, 2);

    // Perform the splicing.
    Inarow.splice(into, extras, first, last);
    cout << "\n===Extras After Splice===" << endl;
    Dump(&extras);
    cout << "\n===Inarow After Splice===" << endl;
    Dump(&Inarow);

    // Sort the list.
    Inarow.sort();
    cout << "\n===Sorted===" << endl;
    Dump(&Inarow);
    return 0;
}
```

Move() 会移动到列表中的某个位置。这个函数可能看起来多此一举，因为 list 模板不允许随机访问。但你需要三个迭代器来执行拼接：两个用于定位第二个列表（源列表）的起始和结束位置，一个用于定位第一个列表中用来保存被拼接成员的位置。Move() 负责定位目标位置。

![](img/128ab511de4e7360e167e3b15cdd5dd0_687_0.png)

Move() 是一个模板函数。不过，调用该函数时，你不需要在尖括号中提供类型名；编译器会根据作为参数传入函数的对象类型，决定使用哪个类版本。

要使用 sort()，你必须提供一个 < 运算符函数，如前面示例所述。下面是应用程序输出：

```
===Ducks===
(Arnold,19,26)
(Betty,18,25)
(Sally,15,12)
(Jim,20,15)

===Reversed===
(Jim,20,15)
(Sally,15,12)
(Betty,18,25)
(Arnold,19,26)

===Extras===
(Grumpy,8,8)
(Sleepy,8,8)

===Extras After Splice===

===Inarow After Splice===
(Jim,20,15)
(Sally,15,12)
(Grumpy,8,8)
(Sleepy,8,8)
(Betty,18,25)
(Arnold,19,26)

===Sorted===
(Arnold,19,26)
(Betty,18,25)
(Grumpy,8,8)
(Jim,20,15)
(Sally,15,12)
(Sleepy,8,8)
```

你可以看到拼接前后两个列表内部的元素；鸭子从一个列表移动到了另一个列表。

## 对决：列表与向量

列表提供顺序访问，这意味着你不能直接进入列表中间并查看那里存储的任何项（就像使用 vector 那样）。如果你想查看列表中的项，必须从开头或末尾开始，一次一项地逐步遍历。vector 允许使用方括号进行随机访问，例如 MyVector[3]。这个要求对 list 来说似乎是一个缺点，但 ANSI 文档说“许多算法反正只需要顺序访问”。列表有明确的优势。list 模板允许你将多个列表拼接在一起，并且很好地支持对列表排序、将成员从一个列表拼接到另一个列表，以及合并多个列表。

## 堆叠 deque

双端队列 deque（发音为“deck”）容器是像 vector 和 list 一样的顺序项列表。与 vector 一样，但与 list 不同，deque 允许使用方括号表示法进行随机访问。与 vector 不同，deque 允许你在开头或末尾压入（插入）项，并从开头或末尾弹出（移除）项。要创建一个保存整数的 deque，可以这样做：

```cpp
deque<int> mydek;
mydek.push_front(10);
mydek.push_front(20);
mydek.push_back(30);
mydek.push_back(40);
```

然后你可以遍历 deque，使用方括号访问其成员，就像它是一个数组一样：

```cpp
int loop;
for (loop = 0; loop < mydek.size(); loop++) {
    cout << mydek[loop] << endl;
}
```

你也可以从 deque 的前端或后端取出项。下面是从前端取出的示例：

```cpp
while (mydek.size() > 0) {
    cout << mydek.front() << endl;
    mydek.pop_front();
}
```

## 对决：deque 与 vector

如果你上网到任何讨论板，使用类似 C++ deque vector 的搜索短语，你会看到很多关于何时使用 deque、何时使用 vector 的讨论、争论和困惑。要知道何时使用哪一个，你需要理解两者之间的差异。在底层，vector 通常将所有数据存储在一个常规数组中，这使得直接访问成员很容易。但这也意味着，要插入项，vector 必须将所有内容滑动到一边，为插入的项腾出空间。deque 不使用 vector 那样的连续存储方式。对 deque 来说插入更容易，因为它不需要来回搬移元素。此外，deque 在调整大小时不必添加新元素，而 vector 在空间不足时则需要这样做。最后，deque 包含一个 push_front() 方法，允许在开头添加项。

这里出现了两个函数：front() 和 pop_front()。front() 函数返回对 deque 前端项的引用。pop_front() 函数移除位于 deque 前端的项。

## 用栈和队列排队

标准库中有两种常见的编程数据结构：

- **栈：** 你一项一项地将项放到栈顶——并且你一项一项地从栈顶取出项。你可以在从栈顶取出项之前，连续添加若干项。这个过程有时称为后进先出（LIFO）算法。
- **队列：** 队列就像在邮局排队——随着人们到来，队伍会变长。每个新来的人走到队尾。人们从队首离开。与栈一样，队列也有另一个名称：它是先进先出（FIFO）算法。

要使用标准库创建栈，你可以使用 deque、list 或 vector 作为底层存储容器。然后声明栈，如下例所示：

```cpp
stack<int, vector<int> > MyStack;
```

或者，你也可以选择使用默认的 deque：

```cpp
stack<int> MyStack;
```

