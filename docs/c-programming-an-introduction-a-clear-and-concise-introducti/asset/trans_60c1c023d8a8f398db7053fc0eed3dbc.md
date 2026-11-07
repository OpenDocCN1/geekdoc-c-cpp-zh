
```cpp
last = lastName;
}

Name::Name(string firstName, string lastName)
{
    first = firstName;
    middle = "";
    last = lastName;
}

Name::Name(string lastName)
{
    first = "";
    middle = "";
    last = lastName;
}

void Name::setFirst(string firstName)
{
    first = firstName;
}

void Name::setMiddle(string middleName)
{
    middle = middleName;
}

void Name::setLast(string lastName)
{
    last = lastName;
}

void Name::setName(string firstName,
                  string middleName,
                  string lastName)
{
    first = firstName;
    middle = middleName;
    last = lastName;
}

string Name::getFirst()
{
    return first;
}

string Name::getMiddle()
{
    return middle;
}

string Name::getLast()
{
    return last;
}

string Name::getName()
{
    return first + " " + middle + " " + last;
}

string Name::getInitials()
{
    return first.substr(0,1) + middle.substr(0,1) +
           last.substr(0,1);
}
```

首先要注意的是，我们必须在程序顶部包含头文件。必须告诉编译器在哪里找到后续方法定义的原型。

这个源文件与前面 Name 类的代码之间的主要区别在于，每个方法名前面都有 `Name::`。例如，`getName()` 方法的定义是：

```cpp
string Name::getName()
{
    return first + " " + middle + " " + last;
}
```

在方法名前加上 `Name::` 可以确保编译器正确识别该方法属于 Name 类，而不只是一个未附加到任何特定类的“普通”函数。

`::` 运算符称为作用域解析运算符，在这里它要求运算符左侧是类名，右侧是方法名。像这样定义作用域是必要的，因为我们是在类定义之外定义该类的方法，编译器必须知道这些方法定义属于哪个类。

## 编译 Name 类

尽管我们还没有编写任何实际使用 Name 类的代码，但仍然可以编译该类，以确保一切在语法上正常工作。在 Visual C++ Express 中，单击菜单区域中的 Debug，然后选择 Build Solution。这会编译你的头文件和源文件，并让你知道这两个文件中是否有任何错误。

假设没有任何错误，你就可以进入最后一步——编写一些代码来测试该类。

## 测试 Name 类

我们已经编写了测试 Name 类的代码，但需要演示如何在将 Name 类代码与使用该代码的程序分离的背景下进行测试。我们已经有用于编写测试代码的文件。它是一个源文件，名称与项目名称相同；如果你一直按照上面的讨论操作，项目名称就是“NameTest”。

现在只需添加我们之前用来测试 Name 类第一个实现的代码。代码如下：

```cpp
// NameClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

#include "Name.h"

int main(array<System::String ^> ^args)
{
        Name myName("Mary", "Alice", "Smith");
        cout << myName.getName() << endl;
        // Mary gets married to Joe Brown
        myName.setLast("Brown");
        cout << myName.getName() << endl;
        cout << "The first name in myName is: "
             << myName.getFirst()
             << endl;
        cout << "The middle name in myName is: "
             << myName.getMiddle()
             << endl;
        cout << "The last name in myName is: "
             << myName.getLast()
             << endl;
        cout << "myName's initials are: "
             << myName.getInitials()
             << endl;
        Console::ReadKey();
        return 0;
}
```

## 开发 List 类

Name 类是一个有用的第一个示例，但它并没有展示用类可以做的所有事情。我们需要开发的许多类都要求每个对象存储不止一条数据（比如一个姓名）。一个存储列表的类将展示如何把数据结构纳入类设计中。

### 创建抽象数据类型

开发类时，在编写任何代码之前，你需要做的第一件事就是仔细思考类的设计。你可以通过问自己几个问题来做到这一点——类中要存储什么数据？需要对数据执行哪些操作？在开始编程之前把这些信息写下来是个不错的主意。

在编程开始之前勾勒出的类称为*抽象数据类型*，简称*ADT*。ADT 会包含诸如类名、类成员列表及它们存储的数据、类方法列表及它们执行的操作等信息。

如果要为 List 类设计 ADT，首先必须决定希望这个类做什么。当然，我们希望该类存储一组项（即列表）。我们希望能够向列表中添加项、显示列表中的项、清空列表并重新开始，以及显示列表中项的数量。对列表还可以做更多事情，但这些操作对于本示例已经足够。（例如，从列表中移除项以及按字母顺序对列表排序涉及高级 C++ 技术，本书没有篇幅讨论。）

我们还需要决定在类中存储什么数据。由于我们正在构建 List 类，因此需要某种能存储数据集合的东西，比如 vector。另一项可能有用的数据是列表中项的数量，即计数。

List 类的 ADT 会列出该 ADT 的每个成员和方法，并描述成员中存储什么数据，或者方法应执行什么操作。下面是 List 类的 ADT：

ADT 名称：List  
ADT 目的：存储相关项

### ADT 成员

| # | 成员 | 描述 |
|---|---|---|
| 1 | Datastore | 字符串向量 |
| 2 | numItems | 整数 |

### ADT 方法

| # | 方法 | 描述 |
|---|---|---|
| 1 | Add | 向列表中添加新的字符串项 |
| 2 | Clear | 从列表中移除所有项 |
| 3 | Display | 将列表写成字符串 |
| 4 | Count | 列表中项的数量 |

ADT 描述中可能仍会遗漏一些细节，例如我们究竟如何实现排序方法，但把这些信息写下来的过程会通过将注意力集中在我们知道希望类完成的事情上，帮助我们实际编写类。你会注意到，当需要数据类型时，就提供了一种数据类型。例如，vector 将存储字符串，而 numItems 成员将存储整数。

### 为 List 类开发代码

现在我们可以直接从 List 类的 ADT 转到编写该类的头文件。如下所示：

```cpp
#include <iostream>
using namespace std;

class List
{
private:
    vector<string> datastore;
    int numItems;
public:
    List();
    void add(string);
    void clear();
    void display();
    int count();
};
```

下一步是编写 List 类源文件的代码。这个类的许多方法几乎与完成该任务所需的 vector 方法相同。例如，`remove()` 方法将调用 vector 的 `erase()` 方法，因此我们真正做的只是把 vector 方法重命名为对列表操作来说更常见的名称。甚至类的一个成员 `numItems`，实际上也只是 vector 的 `size()` 方法的另一个名称。事实上，当我们需要使用 `numItems` 时，我们会通过调用 datastore 向量上的 `size()` 方法来给它的值赋值。否则，我们就必须持续记录添加和移除项的数量，而在代码中这样做容易出错。

下面是 List 类的源文件代码：

```cpp
#include "stdafx.h"
using namespace System;
#include "List.h"

List::List()
{
    vector<string> datastore;
    int numItems = 0;
}

void List::add(string item)
{
    datastore.push_back(item);
}

void List::clear()
{
    datastore.clear();
}
```
