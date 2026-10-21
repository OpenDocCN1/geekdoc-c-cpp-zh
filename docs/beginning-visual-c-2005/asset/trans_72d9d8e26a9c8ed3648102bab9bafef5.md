

```
#pragma once

class CBox
{
public:
    CBox(void);
public:
    ~CBox(void);
private:
    // Length of a box in inches
    double m_Length;
    // Width of a box in inches
    double m_Width;
    // Height of a box in inches
    double m_Height;
};
```

当然，如果你愿意，你完全可以手动输入这些成员的声明，直接写到代码中。你始终可以选择是否使用 IDE 提供的自动化功能。你也可以手动删除自动生成的任何内容，但不要忘记有时 .h 和 .cpp 文件都需要更改。

> 只要你进行手动更改，最好保存所有文件，这样 Class View 中的信息就会得到更新。

如果你查看 Box.cpp 文件，你会看到向导还为你添加的数据成员在构造函数定义中添加了一个初始化列表，每个变量都初始化为 0。你将在下一步修改构造函数以实现你想要的功能。

## 定义构造函数

你需要更改类定义中无参构造函数的声明，使其具有带默认值参数的参数，因此将其修改为：

```
CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0);
```

现在你可以开始实现了。如果 Box.cpp 文件尚未打开，请打开它并将构造函数定义修改为：

```
CBox::CBox(double lv, double wv, double hv)
{
    lv = lv <= 0.0 ? 1.0 : lv;        // Ensure positive
    wv = wv <= 0.0 ? 1.0 : wv;        // dimensions for
    hv = hv <= 0.0 ? 1.0 : hv;        // the object

    m_Length = lv>wv ? lv : wv;      // Ensure that
    m_Width = wv<lv ? wv : lv;       // length >= width
    m_Height = hv;
}
```

请记住，成员函数参数的初始化器应仅出现在类定义中的成员声明中，而不是出现在函数定义中。如果你将它们放在函数定义中，你的代码将无法编译。你已经见过这段代码，所以我不会再讨论它。在此保存文件是个好主意，可以通过单击保存工具栏按钮来实现。养成在切换到其他内容之前保存正在编辑的文件的习惯。如果你需要再次编辑构造函数，你可以通过在 Class View 选项卡的下窗格中双击其条目，或通过从代码显示窗格上方右侧下拉菜单中选择它来轻松访问它。你也可以通过在 Class View 窗格中右键单击其名称并从出现的上下文菜单中选择相应项目，直接在 .cpp 文件中访问成员函数的定义，或在 .h 文件中访问其声明。

## 添加函数成员

你需要将之前看到的所有函数添加到 CBox 类中。之前，你在类定义内定义了几个函数成员，因此这些函数自动成为内联函数。你可以通过手动在类定义中输入这些函数的代码来实现相同的结果，也可以使用添加成员函数向导。

你可能会认为可以在 .cpp 文件中定义每个内联函数，并为函数定义添加 inline 关键字，但问题在于内联函数最终不会成为“真正的”函数。因为每个函数体中的代码必须直接插入到调用位置，因此在编译包含对函数调用的文件时，必须提供函数的定义。如果没有，你将得到链接错误，你的程序将无法运行。如果你希望成员函数为内联，则必须将函数定义包含在类的 .h 文件中。它们可以在类定义内定义，也可以在 .h 文件中紧随其后定义。你应该将需要的任何全局内联函数放入 .h 文件中，并在使用它们的任何 .cpp 文件中 #include 该文件。

要将 GetHeight() 函数作为内联添加，请在 Class View 选项卡上右键单击 CBox 并从上下文菜单中选择 Add > Add Function。你然后可以在显示的对话框中输入定义函数的數據，如图 8-11 所示。

![](img/2359b0c604600c58fba3539c738a356e_489_0.png)

图 8-11

你可以通过从下拉列表中选择来指定返回类型为 double，但同样也可以直接输入它。显然，对于列表中未出现的类型，你只需从键盘输入。选择内联复选框可确保 GetHeight() 将被创建为内联函数。请注意将函数声明为 static、virtual 或 pure 的其他选项。如你所知，静态成员函数独立于类的任何对象存在。我们将在第 9 章讨论虚函数和纯虚函数。GetHeight() 函数没有参数，因此无需添加其他内容。单击 OK 按钮将把函数定义添加到 Box.h 中的类定义中。如果你对 GetWidth()、GetLength() 和 Volume() 成员函数重复此过程，Box.h 中的 CBox 类定义将如下所示：

```
#pragma once

class CBox
{
public:
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0);
    ~CBox(void);
private:
    // Length of a box in inches
    double m_Length;
    // Width of a box in inches
    double m_Width;
    // Height of a box in inches
    double m_Height;
public:
    double GetHeight(void)
    {
        return 0;
    }

    double GetWidth(void)
    {
        return 0;
    }
    double GetLength(void)
    {
        return 0;
    }

    // Calculate the volume of a box
    double Volume(void)
    {
        return 0;
    }
};
```

在类定义中添加了一个额外的 public 部分，其中包含内联函数定义。你需要修改每个定义的提供正确的返回值并将函数声明为 const。例如，GetHeight() 函数的代码应更改为：

```
double GetHeight(void) const
{
    return m_Height;
}
```

你可以以类似方式更改 GetWidth() 和 GetLength() 函数的定义。Volume() 函数定义应更改为：

```
double Volume(void) const
{
    return m_Length*m_Width*m_Height;
}
```

你可以直接在显示代码的编辑器窗格中输入其他非内联成员函数，当然你也可以使用添加成员函数向导来完成，练习会很有用。在 Class View 选项卡上右键单击 CBox 并从上下文菜单中选择 Add > Add Function 菜单项，如前所述。你然后可以在出现的对话框中输入要添加的第一个函数的详细信息，如图 8-12 所示。

![](img/2359b0c604600c58fba3539c738a356e_491_0.png)

图 8-12

这里我将 operator+() 函数定义为 public，返回类型为 CBox。参数类型和名称也已在相应字段中输入。你必须单击 Add 按钮以将参数注册为参数列表的一部分，然后再单击 Finish 按钮。这也会更新 Add Member Function Wizard 对话框底部显示的函数签名。你可以然后如果有多个参数，输入另一个参数的详细信息并再次单击 Add 以添加它。我还在对话框中输入了一条注释，向导将在 Box.h 和 Box.cpp 中插入此注释。当你单击 Finish 时，函数的声明将被添加到 Box.h 文件中的类定义中，并且 Box.cpp 文件中将添加函数的骨架定义。函数需要声明为 const，因此你必须将此关键字添加到类定义中 operator+() 函数的声明中，并添加到 Box.cpp 中函数的定义中。你还必须添加函数体中的代码，如下所示：

```
// Divide one box into another
int CBox::operator/(const CBox& aBox) const
{
    // Temporary for number in horizontal plane this way
    int tc1 = 0;
    // Temporary for number in a plane that way
    int tc2 = 0;

    tc1 = static_cast<int>((m_Length/aBox.m_Length)) *
        static_cast<int>((m_Width/aBox.m_Width));    // to fit this way

    tc2 = static_cast<int>((m_Length/aBox.m_Width)) *
        static_cast<int>((m_Width/aBox.m_Length));    // and that way

    // Return best fit
    return static_cast<int>((m_Height/aBox.m_Height))*(tc1>tc2 ? tc1 : tc2);
}
```

阴影线是你应该手动修改或添加的部分。

特别是那些只是返回数据成员值的非常短的函数，其定义在类定义内，以便它们成为内联函数。如果你点击 Class View 选项卡，然后点击 CBox 类名称旁边的 +，你会看到类的所有成员都显示在下窗格中。

这完成了 CBox 类，但你仍需要定义实现将 CBox 对象体积与数值进行比较的全局函数的定义。

## 添加全局函数

你需要创建一个 .cpp 文件，其中包含支持对 CBox 对象进行操作的全局函数的定义。该文件也需要成为项目的一部分。单击 Solution Explorer 选项卡以显示它（你当前将显示 Class View 选项卡）并右键单击 Source Files 文件夹。从上下文菜单中选择 Add > New Item 以显示对话框。选择类别为 Code，右窗格中的模板为 C++ File (.cpp)，并将文件名输入为 BoxOperators。

现在你可以在编辑器窗格中输入以下代码：

// BoxOperators.cpp
// CBox object operations that don't need to access private members
#include "Box.h"

// Function for testing if a constant is > a CBox object
bool operator>(const double& value, const CBox& aBox)
{ return value > aBox.Volume(); }

// Function for testing if a constant is < CBox object
bool operator<(const double& value, const CBox& aBox)
{ return value < aBox.Volume(); }

// Function for testing if CBox object is > a constant

