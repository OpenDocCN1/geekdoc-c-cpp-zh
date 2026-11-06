

### 清单 3-4（续）

```cpp
{
protected:
    vector<T> data;

public:
    void Add(T const &input);
    void Remove();
    void PrintString();
    void PrintInt();
    bool IsEmpty();
};

template<typename T>
void MyQueue<T>::Add(T const &input)
{
    data.push_back(input);
}

template<typename T>
void MyQueue<T>::Remove()
{
    data.erase(data.begin());
}

template<typename T>
void MyQueue<T>::PrintString()
{
    vector<string>::iterator PrintIt = data.begin();

    while (PrintIt != data.end())
    {
        cout << *PrintIt << endl;
        PrintIt++;
    }
}

template<typename T>
void MyQueue<T>::PrintInt()
{
    vector<int>::iterator PrintIt = data.begin();

    while (PrintIt != data.end())
    {
        cout << *PrintIt << endl;
        PrintIt++;
    }
}

template<typename T>
bool MyQueue<T>::IsEmpty()
{
    return data.begin() == data.end();
}

int main()
{
    MyQueue<string> StringQueue;
}
```

![](img/6ba99460b0feb3585671a4612ff5fabb_746_0.png)

你可以通过为 double 添加特殊处理来解决这个问题。以下是修改后的示例（如 `StringifyDouble` 所示），它兼容了 double 类型。

```cpp
#include <iostream>
#include <sstream>
#include <iomanip>
#include <limits>

using namespace std;

template<typename T> inline string stringify(const T& input)
{
    ostringstream output;
    output << input;
    return output.str();
}

template <> inline string stringify<double>(const double& input)
{
    ostringstream output;
    const int sigdigits = numeric_limits<double>::digits10;
    output << setprecision(sigdigits) << input;
    return output.str();
}

int main()
{
    cout << stringify<int>(42) << endl;
    cout << stringify<double>(45.6789012345) << endl;
    return 0;
}
```

运行此示例时，你会看到预期结果，因为模板的 double 形式使用 `setprecision` 修改了 `ostringstream` 的值。因此，你会看到如下输出：

```text
42
45.6789012345
```

![](img/6ba99460b0feb3585671a4612ff5fabb_746_1.png)

就目前的 C++ 而言，你必须为每个需要特殊处理的数据类型创建专门的模板。从理论上讲，如果 C++ 将来有了 `typeof()` 函数，你就可以检测数据类型并添加 switch 语句，在单个模板内执行专门的处理。在第六册第 2 章的“前缀和后缀”一节中演示的 `typeid()` 函数可以替代 `typeof()`，但它是供应商特定的，并非在每个 C++ 版本中都实现。如果你选择使用 `typeid()` 函数，请确保你所在组织将使用哪个编译器来编译应用程序代码。

![](img/6ba99460b0feb3585671a4612ff5fabb_746_2.png)

你可能还注意到此示例中用于模板的 `inline` 关键字。`inline` 关键字告诉编译器将模板生成的代码与它出现的代码放在一起，而不是作为单独的函数调用放在行外。在某些情况下，例如这个 `stringify()` 函数，结果就是代码执行得更快。编译器没有义务遵循 `inline` 关键字。此外，当模板代码必须执行某种实例化，或者它不代表应用程序可能经常调用的关键路径代码时，你希望将模板代码放在行外。

## 创建模板库

你通常不会创建一个模板并将其放在应用程序项目文件中。本章前面的示例将所有内容放在一起是为了便于解释，但在现实世界中，模板通常驻留在库中。Code::Blocks 提供了几种库项目。本章介绍*静态库*——一种添加到应用程序中的库。模板始终驻留在静态库中。

![](img/6ba99460b0feb3585671a4612ff5fabb_747_0.png)

Code::Blocks 还支持动态链接库（DLL）和共享库，多个应用程序可以同时使用这些库。但是，你不能将模板代码放入 DLL 或共享库中，除非你创建模板的特定实例，因为模板需要预处理器来工作，而 DLL 是预编译的代码。使用 DLL 和共享库比使用静态库更复杂，而且在创建控制台应用程序时，你通常不需要共享库的能力。有关 Code::Blocks 支持的各种项目类型的详细信息，请参阅第 1 册第 2 章的“定义你的第一个项目”一节。

### 定义库项目

创建库项目与控制台应用程序略有不同。以下步骤描述了如何创建库项目：

-   **1. 选择“文件”»“新建”»“项目”。**

    你会看到“从模板新建”对话框，如图 3-1 所示。

    ![](img/6ba99460b0feb3585671a4612ff5fabb_747_1.png)

    **图 3-1：** 为 Code::Blocks 提供项目的描述。

-   **2. 在“项目”选项卡中高亮“静态库”图标，然后点击“开始”。**

    你会看到静态库向导的欢迎页面。

-   **3. 点击“下一步”。**

    你会看到与项目相关的问题列表，如图 3-2 所示。这些问题定义了项目的基本信息，例如项目名称。

    ![](img/6ba99460b0feb3585671a4612ff5fabb_748_0.png)

    **图 3-2：** 为 Code::Blocks 提供静态库的描述。

-   **4. 在“项目标题”字段中为你的项目键入名称。**

    示例使用 `MathLibrary` 作为项目标题。注意，向导会自动开始在“项目文件名”字段中为你创建条目。

-   **5. 在“创建项目的文件夹”字段中键入项目的位置。**

-   **6.（可选）在“项目文件名”字段中键入项目文件名。**

-   **7. 点击“下一步”。**

    你会看到如图 3-3 所示的编译器设置。此示例使用默认的编译器设置。但是，请务必记住，你可以选择不同的编译器，修改项目的调试版和发布版的位置，并根据需要进行其他更改。Code::Blocks 为库提供的定制级别与应用程序相同。

    ![](img/6ba99460b0feb3585671a4612ff5fabb_748_1.png)

    ![](img/6ba99460b0feb3585671a4612ff5fabb_749_0.png)

    **图 3-3：** 更改编译器设置以满足项目需求。

-   **8. 更改任何必需的编译器设置，然后点击“完成”。**

    向导会为你创建应用程序。然后它会显示已加载项目的 Code::Blocks IDE。注意，静态库项目包含一些示例代码，可帮助你入门。你现在就可以编译此库并进行测试。

### 配置库项目

静态库以一个标准的 C 文件开始。为了使此库与模板良好配合，你需要删除 C 文件，添加 C++ 文件，并添加头文件。以下步骤描述了如何执行此过程：

-   **1. 在“管理”窗口的“项目”选项卡中右键单击 `main.c`，然后从出现的上下文菜单中选择“从项目中移除文件”。**

    Code::Blocks 会从项目树中移除该文件。

-   **2. 选择“文件”»“新建”»“文件”。**

    你会看到如图 3-4 所示的“从模板新建”对话框。

-   **3. 高亮“C/C++ 头文件”图标并点击“开始”。**

    你会看到 C/C++ 头文件向导的欢迎页面。

-   **4. 点击“下一步”。**

    向导要求你提供头文件配置信息（见图 3-5）。

    ![](img/6ba99460b0feb3585671a4612ff5fabb_750_0.png)

    **图 3-4：** 使用“从模板新建”对话框添加新文件。

    ![](img/6ba99460b0feb3585671a4612ff5fabb_750_1.png)

    **图 3-5：** 定义头文件需求。

-   **5. 在“带完整路径的文件名”字段中，键入 `MathLibrary.h`，点击省略号按钮，然后点击“保存”。**

    Code::Blocks 会将完整的项目路径添加到你所选的文件名中。注意，Code::Blocks 还会为“头文件保护词”字段提供条目。这个词确保头文件不会多次添加到项目中。

