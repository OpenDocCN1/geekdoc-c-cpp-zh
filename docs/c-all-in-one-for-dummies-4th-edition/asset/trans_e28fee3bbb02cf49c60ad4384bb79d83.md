
但即使这些也不够好。首先，通常应允许用户按 Enter 键。只按一次键就自动执行某些操作可能会让用户感到意外。此外，你可能还希望支持多个选项。如果用户想在菜单中选择选项 A，你可能需要支持以下任意一种输入：

- A
- a
- Add
- ADD
- add

这可以全部封装成类似下面这样的简短代码：

```cpp
string choice;
cin >> choice;
char ch = choice[0];
ch = toupper(ch);
switch (ch)
{
    case 'A':
        cout << "Adding random data..." << endl;
        break;
    case 'B':
        cout << "Boiling it down!" << endl;
        break;
    case 'C':
        cout << "Compressing!" << endl;
        break;
    case 'D':
        cout << "Deleting..." << endl;
        break;
}
```

现在用户可以输入任意单词，而应用程序只检查第一个字母。但如果你不喜欢把 aompress 当作 add 而不是 compress 的想法，可以这样做：

```cpp
string choice;
cin >> choice;
choice = MyUppercase(choice);
if (choice == "A" || choice == "ADD")
{
    cout << "Adding random data..." << endl;
}
else if (choice == "B" || choice == "BOIL")
{
    cout << "Boiling it down!" << endl;
}
else if (choice == "C" || choice == "COMPRESS")
{
    cout << "Compressing!" << endl;
}
else if (choice == "D" || choice == "DELETE")
{
    cout << "Deleting..." << endl;
}
else
{
    cout << "I don't know that word" << endl;
}
```

这段代码只查找第一个字母或完全匹配的单词，字母可以是大写或小写，而单词可以是大写、小写或混合大小写。这种选择可能是最好的。不过，你可能会注意到示例使用了一个名为 MyUppercase() 的函数，它依赖 lambda 表达式（有关使用 lambda 表达式的详细信息，请参见第 3 册第 1 章）来执行处理（使用此版本需要 C++ 20 或更高版本，但你也可以使用简单的 for 循环来完成该任务）。

```cpp
string MyUppercase(string str) {
    for_each(str.begin(), str.end(), [](char & c) {
        c = ::toupper(c);
    });
    return str;
}
```

## 处理文本输入

如果你要处理复杂的应用程序，请务必小心。假设你正在编写一个应用程序，要在数据库中查找特定客户姓名的信息。你可能会遇到以下情况：

- 数据库中的姓名全部为大写字母（例如，GEORGE WASHINGTON），而用户可以输入大小写混合的姓名（例如，George Washington）。
- 名和姓是分开存储的，因此你的应用程序必须在数据库中查找姓为 Washington、名为 George 的情况。用户不知道只需输入姓，可能会将名和姓都输入到同一个文本框中。或者你可能允许用户一次输入两个名字，但用户没有意识到应该先输入姓，或者可能是先输入姓，然后输入逗号，再输入名。
- 用户可能会在姓名开头或结尾输入一些空格。应用程序随后会查找类似 " George Washington " 的条目，却找不到，因为它存储为 "George Washington"（前后没有空格）。
- 用户可能会在数据库未存储中间名首字母的情况下输入中间名首字母。

所有这些问题都很容易避免。以下是一些提示：

- 在查找姓名之前，你必须了解姓名在数据库中是如何存储的。如果它们以全大写形式存储，你不应要求用户以全大写形式输入。相反，应接受任意大小写的单词，并将其转换为大写。
- 你必须了解姓名在存储时是否将名与姓分开。然后允许任何格式。如果用户输入 **George Washington**（没有逗号），你可以在空格处拆分字符串，提取出名和姓。但如果用户输入的姓名在名和姓之间带有逗号，你可以在逗号处拆分，先提取姓，再提取名。
- 空格不应成为问题。用户输入字符串后，你可以去掉字符串中的空格。
- 你的应用程序应清楚告诉用户是输入中间名、中间名首字母，还是两者都不输入。如果你使用文本控件，在不需要中间名时，甚至不要包含中间名字段。或者如果需要，请在窗口上明确说明用户应输入中间名首字母还是完整的中间名。如果输入项只是首字母，你可以删除末尾的句点，或添加句点，具体取决于数据库中存储的内容。

所有这些步骤都有助于让你的应用程序万无一失。其理念是鼓励用户按照自己喜欢的方式操作，但防止他们以应用程序不喜欢的方式操作。如果你的应用程序不需要中间名首字母，就不要给用户输入它们的机会。

## 执行字符串处理

清单 1-1 中的 `StringProcess` 示例展示了如何去掉空格、去掉中间名首字母末尾可能存在的句点，以及根据空格或逗号拆分字符串。此示例使用了一个名为 vector 的特殊类。vector 类很像数组，但 vector 类更强大一些：因为 vector 是一个类，所以你可以使用方法轻松地向其中添加和删除内容。不过，vector 也是一个 *模板*，因此声明它时，必须说明希望它保存什么类型的变量。变量类型放在尖括号中。示例使用字符串声明它，如下所示：`vector<string>`。为了让代码更简单，代码使用 typedef 为该类型起了一个更简单的名称：`StringList`。

**清单 1-1：处理字符串以减少错误**

```cpp
#include <iostream>
#include <vector>
#include <string.h>
#include <algorithm>

using namespace std;

typedef vector<string> StringList;
StringList Split(string orig, string delims) {
    StringList list;
    int pos;
    while((pos = orig.find_first_of(delims)) != -1) {
        list.push_back(orig.substr(0, pos));
        orig = orig.substr(pos + 1);
    }
    list.push_back(orig);
    return list;
}

string MyUppercase(string str) {
    for_each(str.begin(), str.end(), [](char & c) {
        c = ::toupper(c);
    });
    return str;
}

string stripspaces(string orig) {
    int left;
    int right;
```

```cpp
// Name has no comma, so start with first name.
list = Split(name, ",");
size = list.size();
if (size > 0)
    first = list[0];
if (size > 2) {
    middle = list[1];
    last = list[2];
}
if (size == 2)
    last = list[1];
}
// If middle name is just initial and period,
// then remove the initial.
if (middle.length() == 2)
    if (middle[1] == '.')
        middle.erase(1,1);

// Convert all to uppercase
first = MyUppercase(first);
middle = MyUppercase(middle);
last = MyUppercase(last);

cout << "first: " << first << endl;
cout << "middle: " << middle << endl;
cout << "last: " << last << endl;
cout << endl;
}

int main() {
    string name;
    name = "   Washington, George Zeus   ";
    ProcessName(name);
    name = "Washington, George Z.";
    ProcessName(name);
    name = "George Z. Washington";
    ProcessName(name);
    name = "George Zeus Washington";
    ProcessName(name);
    name = "George Washington";
    ProcessName(name);
    return 0;
}
```

清单 1-1 几乎可以防止错误，但它仍然不能正确处理某些情况。例如，如果有人尝试处理带有中间名（如 Zeus.，注意名字后面的句点）的字符串，应用程序不会删除该句点。以下是你可能对此应用程序做出的其他一些改进：

- **消除不合适的字符：** 你可以确保姓名中不出现不合适的字符。在找到名、中间名和姓之后再进行此处理；这样，你就不会因为需要根据可能用于指定姓名顺序的单个逗号来查找数据而破坏查找尝试。你可以使用各种 if 语句来完成这类操作。
- **处理超过三个名字的情况：** 针对超过三个名字的情况添加特殊预防措施。有些人的名字很多（比如 10 个或 11 个，尤其是英国皇室成员）。但是，如果此应用程序用于例如换油操作，你大概不会遇到查尔斯·菲利普·阿瑟·乔治，威尔士亲王这样的名字。如何处理姓名取决于你的具体情况。
- **执行初始处理：** 进行一些初始处理。用户输入姓名后，立即确保姓名不是空字符串——即 ""（一对引号，中间没有空格）。

### 万无一失应用程序的神话

任何花时间阅读行业媒体的人都知道，许多应用程序都存在反复出现的缺陷问题。供应商刚修复一个缺陷，另一个缺陷又出现了。一些开发者可能认为这些公司的开发者是傻瓜，让我们所有人都蒙羞。然而，这些开发者往往和我们一样。因为他们是人，而人都会犯错——无论是在应用程序的开发者端还是用户端——所以应用程序永远不会没有缺陷。当然，你或许能够创建一个简单、几乎万无一失的应用程序，但随着应用程序复杂性的增加，交互数量和潜在缺陷的数量也会增加。到某个时候，应用程序各部分之间的交互数量会增加到无缺陷应用程序变得不可能的程度。

万无一失的应用程序是一个神话。如果你相信这个神话，你可能会在开发人员再也找不到缺陷的那一刻就想停止寻找缺陷。不幸的是，这种态度会导致头条新闻宣称你的应用程序是下一个重大安全漏洞。不要相信万无一失应用程序的神话——始终警惕潜在错误。
