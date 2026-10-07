
```cpp
namespace gradebook {
    class Student {
        // 代码在此
    public:
        void addAssignment(const Assignment &a) {
            // 将作业添加到 vector 中
        }

    class Assignment {
        // 代码在此
    }

    void listStudents() {
        // 代码在此
    }
}
```

为了从你代码的其他地方访问这些类，你需要执行类似下面的操作：

```cpp
int main() {
    gradebook::Student student;
    gradebook::Assignment assignment;

    student.addAssignment(assignment);

    gradebook::listStudents();

}
```

其中 `gradebook:` 是访问 `gradebook` 命名空间成员的方法。不过，你也可以通过代码中添加 `using namespace gradebook` 来绕过这一点，最好放在 `using namespace std` 之下。既然提了这里，你并不非要在代码中包含 `using namespace std`。由于它是命名空间，你技术上可以使用命名空间指令来访问其中的所有内容：

```cpp
std::string out= "Hello world";
std::cout << out;
```

通常，命名空间会定义在头文件中。这通过促进使用现有模块和创建新模块来使代码在未来更容易使用，从而了模块化的理念。

头文件是包含大段代码定义的文件，这些定义可以在其他代码中使用。例如，一个头文件技术上可以有一个接受两个变量并返回和的 `add` 函数。你可以将此头文件包含在 `main.cpp` 中，然后访问该函数。

为了创建一个头文件，你必须使用所谓的“预处理器指令”`preprocessor directives` 来定义它。

现在是深入了解预处理器指令究竟是什么的最佳时候了。

所有的 C++ 代码都必须编译。预处理器指令告诉预处理器在编译之前查看代码，然后执行某些操作以以某种方式影响代码或程序。

预处理器指令有几种不同的类型。

首先是宏定义，例如 `#define` 和 `#undef`。这些允许你定义文本中使用的内容并在编译期间将其替换为其他内容。例如：

```cpp
#define INCH_PER_FOOT 12

int main() {
    cout << "In 7 feet, there are " << 7 / INCH_PER_FOOT << " inches.\n";
}
```

它也可以与三元表达式一起使用来描述函数宏。

其他的是条件运算符。`#ifdef`、`#elif` 等。

为了向你展示头文件和额外 CPP 文件的用途，我们实际上将开始一个新项目，我们将这个项目命名为 `Gradebook`。信不信由！

这次我们将保留 `main.cpp`，你已经有足够的练习了。只需删掉 hello world 部分即可。

由于这是我们第一次在一个项目中使用多个文件，我将尽量让它看起来自明易懂。这将把我们目前为止使用的许多概念结合起来，在我们的主文件中产生一些非常漂亮且易于使用的代码，同时教你关于模块化的知识。

C++ 项目通常分为两个部分：接口`头文件`和它们的实现`C++ 文件`。接口旨在是可重用和扩展的。为了这个项目，我们将创建一个成绩单，在头文件的命名空间内存储我们的类数据，将重要函数存储在其他 C++ 文件中，并使用

无论如何，现在你去“文件 -> 新建 -> 空文件”。创建一个名为`gradebook.h`的文件。我们需要向预处理器抛出一些指令，所以这是我们要做的：

```cpp
#ifndef GRADEBOOK_H
#define GRADEBOOK_H

#endif
```

在 `#define` 和 `#endif` 指令之间，我们将创建主命名空间`gradebook`。在其中，我们将创建两个类：`Assignment` 和 `Student`。

- `assignment` 类应该有一个公共字段，包含：

    - 一个构造函数，接收一个用于作业名称的字符串和一个用于分数的浮点数

- 它应该有一个私有字段，包含：

    - 一个字符串：`assignmentName`

    - 一个浮点数：`grade`

- `Student` 类应该有一个公共字段，包含：

    - 一个接收学生名称字符串的构造函数

    - 一个将作业添加到作业 `vector` 中的中的函数，该函数接受该作业作为参数

    - 一个返回学生名称的函数

- 以及一个私有字段，包含：

    - 一个名为 `grades` 的 `vector<Assignment>`

    - 一个学生名称的字符串

## 你的代码看起来应该是这样的：

```cpp
#include <vector>
#include <string>

#ifndef GRADEBOOK_H
#define GRADEBOOK_H

using std::vector;
using std::string;

namespace gradebook {
    class Assignment {
    public:
        Assignment(std::string name, float grade) {
            this->assignmentName = name;
            this->grade = grade;
        }
    private:
        std::string assignmentName;
        float grade;
    };

    class Student {
    public:
        Student(std::string name) {
            this->name = name;
        }
        void addGrade(Assignment &assignment) {
            this->grades.push_back(assignment);
        }
        string getName() {
            return this->name;
        }
    private:
        std::vector<Assignment> grades;
        std::string name;
    };
}
#endif
```

头文件现在写完成了。

去“文件 -> 新建 -> 空文件”并将其命名为 `load.cpp`。

在此文件中，包含 `iostream`, `vector` 和你的头文件 `"gradebook.h"`。

你将使用 `std::vector` 和我们创建的命名空间中的 `Student` 类。通过输入 `using gradebook::student` 告诉编译器你正在使用。

在这里，我们想创建一个返回空内容的函数。将其命名为 `loadStudents`，让它接受一个学生 `vector` 作为参数。这里的想法是我们将从 `main` 发送一个 `vector` 并用学生填充它。

使用 `vector<student>.push_back(Student())` 来填充它。

然而，如果我们想从文件读取学生而不是硬编码呢？

这就是我们的重载课程派上用场的地方。让我们创建一个名为 `loadStudents` 的第二个函数，它接收学生 `vector` 以及名为 `filename` 的字符串。在文件顶部包含 `fstream`，并在你的 `load` 文件中两个变量：一个 `std::ifstream` 变量和一个 `std::string` 变量。

打开文件，并将 `filename` 作为文件名。当还有行需要读取时，使用 `vector<student>.push_back(Student())` 将学生读入 `vector` 中。它看起来应该是这样的：

```cpp
void loadStudents(vector<Student> &vec, std::string &filename) {
    std::ifstream file;
    std::string input;
    file.open(filename);
    while(getline(file, input))
        vec.push_back(Student(input));
    file.close();
}
```

搞定！我们现在有两个适用的 `loadStudents` 函数。

但等一下，我们还没有在主函数中使用它们。

你看，问题在于当你使用来自源文件的函数时，必须执行某种所谓的“前向声明”。

有两种方法可以实现：

1. 在 `main.cpp` 文件的开头声明，在 `using` 语句之后，主函数之前。

2. 在你的头文件中声明它。

我们将采用后者，因为它整洁得多。

所以我们进入头文件，在我们 `gradebook` 命名空间之后就是声明这些函数的地方。

```cpp
void loadStudent(vector<gradebook::Student> &vec);
loadStudent(vector<gradebook::Student> &vec, std::string &filename);
```

现在我们可以回到主文件，确保一切都按预期工作。

首先，创建一个名为 `studentList` 的新学生 `vector`。

调用 `loadStudents` 函数，将你创建的 `vector` 作为参数传递给它。

```cpp
for (Student s : studentList) {
  cout << s.getName() << "\n";
}
```

这是未来许多其他功能的跳板。

让我们现在尝试给学生布置一些作业吧，他们缺少这些。我们已经有了一个内置函数来处理这些，所以我们只需要找一个学生……等一下。在 `vector` 中查找学生有点困难。我们可以通过两种方式来修正这个问题，让那些必须在控制台周围操作的可怜老师们轻松一些。

第一种方案在用户端效率更高，所以我们用这个。让我们重新利用我们的循环，或者说是我们的 `cout` 语句。它现在会在学生名称旁边打印当前索引，这将告诉我们每个学生在 `vector` 中的位置。我们知道它们从 0 开始。所以我们可以定义一个从 0 开始的整数 `i`，它在每次循环循环时递增。我们的 `cout` 函数看起来应该是这样：

```cpp
cout << i << " : " << s.getName() << "\n";
```

之后，我们将测试这个功能。创建一个名为 `input` 的 `int`，然后通过 `cin` 运行它。输出 `studentList.at(input).getName()` 的值。编译并测试。它应该运行得很好，并且看起来像这样：

```cpp
#include <iostream>
#include <vector>
#include "gradebook.h"

using namespace std;
using gradebook::Student;

int main() {
    int i = 0, input;
    vector<Student> studentList;

    loadStudents(studentList);

    for (Student s : studentList) {
        cout << i << " : " << s.getName() << "\n";
        i++;
    }

    cin >> input;

    cout << studentList.at(input).getName();

    return 0;
}
```

如果一切顺利，那就太棒了。我们知道代码运行良好。现在我们需要做的是修改我们刚才的操作，以便以足够简单的方式输入分数？我们将修改那个 `cout` 语句，显示“Enter assignment name”。然后我们将接受一行输入并存储在名为 `assignmentName` 的 `string` 中，并通过 `cin` 过滤一个 `float` 变量 `grade`。为了简单起见，我们将使用标准输入 `cin`。听起来有点吓人，但它是有道理的且运行良好。到结束时，你的代码看起来大致如下：

```cpp
cin >> assignmentName >> grade;

Assignment a = Assignment(assignmentName, grade);

studentList.at(input).addGrade(a);
```

现在我们需要测试它。让我们进入 `assignment` 类并添加一种同时返回名称和分数的的方法。我们还需要进入 `student` 类并添加一种返回其作业 `vector`的方法。你的 `Assignment` 和 `Student` 类理想情况下应该是这样的：

```cpp
class Assignment {
public:
    Assignment(std::string name, float grade)
    {
        this->assignmentName = name;
        this->grade = grade;
    }
    string getName() {
        return assignmentName;
    }
    float getGrade() {
        return grade;
    }
private:
    std::string assignmentName;
    float grade;
};
```

```cpp
class Student {
public:
    Student(std::string name) {
        this->name = name;
    }
    void addGrade(Assignment &assignment) {
        this->grades.push_back(assignment);
    }
    std::vector<assignment> getGrades() {
        return this->grades;
    }
    string getName() {
        return this->name;
    }
private:
    std::vector<Assignment> grades;
    std::string name;
};
```

现在让我们好好利用它。编写一个 `cout` 函数，显示学生的名称，然后是作业名称，最后是该作业的分数。我的代码最后看起来像这样，你的也应该相似。它非常重，有很多方法可以让它看起来更舒服一些，但对于我们的目的来说，它是有效的。

```cpp
cout << "The student's name is: " <<
studentList.at(input) << ".\n"
<< "Their grade on assignment " <<
studentList.at(input).at(0).getName()
 << " was " <<
studentList.at(input).getGrades().at(0).getGrade();
```

有很多方法可以改进本指南，但这主要是为了向你展示 C++ 中模块化的多种用途以及命名空间`namespaces`等内容的巨大用处。你可以在几个循环内实现所有这些代码，如果你愿意，甚至可以为程序实现类似菜单的东西。这有很多可能性。整个章节的核心理由是向你展示 C++ 将大项目拆分为小块的巨大强大能力。

想象一下如果我们必须把所有这些都实在一个小程序的一个函数中会怎样？对于大约 3 行输入和极少的计算，代码将会有近 150 行。尽管如此，为程序拥有一个坚实的基础设施与任何事情一样重要。事实上，这正是面向对象编程的核心思想：为底层概念提供更好的基础设施和利用代码的更好方法。我本人是这一理念非常严格的遵循者——可以说是过头了！如果某物可以做成一个类或一个函数，我将总是这样做。

模块化的完美之处在于重用的潜力。你可以定义跨程序重用的函数或算法。这种模块化的绝佳例子就是游戏引擎。游戏引擎提供了许多重要功能，如图形、音频、接收键盘和控制器输入、运行循环以及

随着本节的完成，本书基本结束了。

# 结语

感谢你阅读《C++：从初学者到专家指南》，希望它具有启发性，并为你提供了实现目标所需的所有工具。下一步是在编程中应用你的知识。与任何事情一样，进步的终极方法是练习、练习再练习。我建议寻找开源项目并看看你可以从源码中分解出什么。思考一些有趣的项目——学习编程 GUI、制作基础网页浏览器、制作音乐播放器、编写游戏引擎——然后一步步地，首先将其拆解为你你熟悉的内容，然后在此基础上构建。例如，如果你想构建网页浏览器，你需要处理连接互联网以发送和接收数据，这超出了本书的范围。如果你想构建点对点聊天客户端，你需要处理建立到另一台计算机的直接隧道，以便你们可以在对方的控制台或聊天框直接对话。一旦你有了想做什么的想法，搜索关于如何做的教程——或者如果你想自己探索，寻找可以帮助你的 API，然后查看它们的文档以弄清楚如何使用它们。无论你最终做什么，提高任何事情的方法都是推自己一把并尽可能地练习，以成为该领域最好的自己。这本书只是开始。你现在已经掌握了 C++ 编程的基础知识，但未来的道路很漫长，每个项目都会有自己的问题和

需求。我只希望我已经为你做好了充分准备，以应对可能出现的任何问题。

最后，如果你觉得这本书很有帮助，欢迎在 Amazon 上给出评价，我们将不胜感激！

# Timothy Short 的其他书籍

- SQL：从入门到专家指南

- Linux：新手快速上手指南

- PowerShell：从入门到专家指南

- 区块链：掌握隐藏经济的全面指南

- 树莓派 3：从入门到专家指南

- WordPress：从入门到专家指南

- Shopify：从入门到专家指南

- 被动收入：财务自由终极指南
