
`signals` 部分声明了用户点击查找按钮时对话框发射的两个信号。如果启用了“向后搜索”选项，对话框将发射 `findPrevious()`；否则发射 `findNext()`。

`signals` 关键字是一个宏。C++ 预处理器会在编译器看到它之前将其转换为标准的 C++。Qt::CaseSensitivity` 是一个枚举类型，可以取 `Qt::CaseSensitive` 和 `Qt::CaseInsensitive` 值。

在类的私有部分，我们声明了两个槽（slots）。为了实现这些槽，我们需要访问对话框的大多数子控件，因此我们也保留了它们的指针。`slots` 关键字和 `signals` 一样，也是一个展开为 C++ 编译器可以理解的内容宏。

对于私有变量，我们使用了它们类的前置声明。之所以可以这样做是因为它们都是指针，而且我们没有在头文件中访问它们，因此编译器不需要完整的类定义。我们本可以包含相关的头文件（`<QCheckBox>`, `<QLabel>` 等），但在可以使用前置声明的情况下可以使编译速度快一些。

我们现在来看 `finddialog.cpp`，它包含了 `FindDialog` 类的实现。

```cpp
#include <QtGui>
#include "finddialog.h"
```

首先，我们包含了 `<QtGui>`，这是一个包含 Qt GUI 类定义的头文件。它由几个模块组成，每个模块都位于自己的库中。最主要的模块有 `QtCore`、`QtGui`、`Network`、`QtOpenGL`、`QtScript`、`QtSvg` 和 `QtXml`。`<QtGui>` 头文件包含了 `QtCore` 和 `QtGui` 模块的所有类定义。包含这个头文件避免了单独包含每个类的麻烦。

 `findialog.h` 中，与其包含 `<Dialog>` 并对 `QCheckBox`、`QLabel`、`QLineEdit` 和 `QPushButton` 使用前置声明，我们可以直接包含 `<QtGui>`。然而，从另一个头文件中包含如此大的头文件通常是不好的，尤其是在较大的应用程序中。

```cpp
3 FindDialog::FindDialog(QWidget *parent)
4     : QDialog(parent)
5 {
6     label = new QLabel(tr("Find &what:"));
7     lineEdit = new QLineEdit;
8     label->setBuddy(lineEdit);

10    caseBox: QCheckBox = new QCheckBox(tr("Match &case"));
11    backwardCheckBox = new QCheckBox(tr("Search &backward"));

13    findButton = new QPushButton(tr("Find"));
14    findButton->setDefault(true);
15    findButton->setEnabled(false);

17    closeButton = new QPushButton(tr("Close"));
```

在第 4 行，我们将参数 `parent` 传递给基类构造函数。然后我们创建了控件。`tr()` 函数调用字符串字面量并将其标记为翻译成其他语言。该函数定义在 `QObject` 以及每个包含 `Q_OBJECT` 宏的子类中。将用户可见的字符串包裹在 `tr()` 中是一个良好的习惯，即使你暂没有计划将你的应用程序翻译到其他语言。我们将在第 18 章介绍 Qt 应用程序。

在字符串字面量中，我们使用取和符号（`&`）来指示快捷键。例如，第 11 行创建了一个查找按钮，在支持快捷键的平台上，用户可以通过按下 `Alt-F` 来激活它。取和符号也可以用于控制焦点：在第 6 行我们创建了一个带有快捷键（Alt+W）的标签，在第 8 行我们将标签的伙伴（buddy）设置为行编辑器。伙伴是一个当标签的快捷键被按下时接受焦点的控件。因此，当用户按下 `Alt+W` 时，焦点将进入行编辑器（伙伴）。

在第 12 行，我们通过调用 `setDefault(true)` 将查找按钮设置为对话框的默认按钮。默认按钮是按下 Enter 键时被按下的按钮。在第 13 行，我们禁用了查找按钮。当控件被禁用时，它通常会显示为灰色且不对用户交互做出响应。

```cpp
connect(lineEdit, SIGNAL(textChanged(const QString &)),
this, SLOT(enableFindButton(const QString &)));
connect(findButton, SIGNAL(clicked()),
this, SLOT(clicked()));
connect(closeButton, SIGNAL(clicked()),
this, SLOT(close()));
```

私有槽 `enableFindButton(const QString &)` 在每当行编辑器中的文本发生变化时被调用。私有槽 `findClicked()` 在用户点击查找按钮时被调用。当用户点击关闭时，对话框会自动关闭。`close()` 槽继承自 `QWidget`，其默认行为是将控件从视图中隐藏（而不删除它）。我们稍后会查看 `enableFindButton()` 和 `findClicked()` 槽的代码。

由于 `QText` 是 `FindDialog` 的祖先之一，我们可以在 `connect()` 调用前省略 `QObject::` 前缀。

```cpp
QHBoxLayout *topLeftLayout = new QHBoxLayout;
topLayout->addWidget(label);
topLayout->addWidget(lineEdit);

QVBoxLayout *leftLayout = new QVBoxLayout;
leftLayout->addWidget(topLeftLayout);
leftLayout->addWidget(caseCheckBox);
leftLayout->addWidget(backwardCheckBox);

QVBoxLayout *rightLayout = new QVBoxLayout;
rightLayout->addWidget(findButton);
rightLayout->addWidget(closeButton);
rightLayout->addStretch();

HBoxLayout *mainLayout = new QHBoxLayout;
mainLayout->addLayout(leftLayout);
mainLayout->addLayout(rightLayout);
setLayout(mainLayout);
```

接下来，我们使用布局管理器来布局子控件。布局可以同时包含控件和其他布局。通过以各种组合中嵌套 `QHBoxLayout`、`QVBoxLayout` 和 `QGridLayout`，可以构建出非常复杂的界面。

对于查找对话框，我们使用了两个 `QHBoxLayout` 和两个 `QVBoxLayout`，如图 2.2 所示。外层布局是主布局；它在第 35 行安装到 `FindDialog` 并负责对话框的整个区域。另外三个布局是子布局。图 2.2 底部的弹簧（或“stretch”）使用了查找和关闭按钮下方的空白空间，确保这些按钮占据布局的顶部。

# 图 2.2 查找对话框的布局

![](img/5a524abdf0b0d58fa99d30abb446311_png)

布局类的一个微妙之处是它们不是控件。相反，它们继承自 `QLayout`，而 `QLayout` 又继承自 `QObject`。在图中，控件用实线表示，而布局用虚线表示以突出它们的区别。在运行的应用程序中，布局是不可见的。

当子布局添加到父布局（第 25、33 和 34 行）时，子布局会自动重新父化。然后，当主布局安装到对话框（第 35 行）时，它成为了对话框的子级，布局中的所有控件都被重新父化。结果父子层次结构如图 2.3 所示。

```cpp
36     setWindowTitle(tr("Find"));
37     setFixedHeight(sizeHint().height());
38 }
```

# 图 2.3 查找对话框的父子关系

最后，我们将标题设置在对话框标题栏中，并设置固定的高度，因为对话框中没有可以有效占据额外空间的控件。`QWidget::sizeHint()` 返回控件的“理想”大小。

这完成了 `FindDialog` 构造函数的回顾。由于我们使用了 `new` 创建对话框的控件和布局，似乎我们需要编写析构函数来删除创建的每个控件和布局。这不是必要的，因为 Qt 在父对象销毁时会自动删除子对象，而子控件和布局都是 `FindDialog` 的后代。

现在我们来看对话框的槽：

```cpp
39 void FindDialog::findClicked()
40 {
41     QString text = lineEdit->text();
42     Qt::CaseSensitivity cs =
43         caseBox->isChecked() ? Qt::CaseSensitive
44         : Qt::CaseInsensitive;
45     if (backwardCheck->isChecked()) {
46         emit findPrevious(text, cs);
47     } else {
48         emit findNext(text, cs);
49     }
50 }
```

```cpp
51 void FindDialog::enableFindButton(const QString &text)
52 {
53     findButton->setEnabled(!text.isEmpty());
54 }
```
