
第 10、11 行创建了 `QSpinBox` 和 `QSlider`，第 12、13 行设置了它们的有效范围。我们可以安全地确保用户年龄最多为 130 岁。我们可以将 `window` 传递给 `QSpinBox` 和 `QSlider` 的构造函数，指定这些组件以窗口为父组件，但这不是必要的，因为布局系统会自动处理并设置数字框和滑动条的父组件，我们很快就会看到。

第 14 到 17 行中的两次 `QObject::connect()` 调用确保了数字框和滑动条是同步的，以便始终显示相同的值。每当一个组件的值改变时，就会发射其 `valueChanged(int)` 信号，并用新值调用另一个组件的 `setValue(int)` 槽。

第 18 行将数字框的值设置为 35。当这种情况发生时，`QSpinBox` 发出带有整型参数 35 的 `valueChanged(int)`。该参数传递给 `QSlider` 的 `setValue(int)` 槽，将滑动条的值设置为 35。滑动条因为其自己的值改变而发射 `valueChanged(int)` 信号，从而触发数字框的 `setValue(int)` 槽。此时，`setValue(int)` 不会发射任何信号，因为数字框的值已经是 35。这防止了无限递归。图 1.5 总结了这种情况。

### 图 1.5. 改变一个组件的值会同时改变两个

1. 0: `setValue(35)`

2. 35: `valueChanged(35)`, `setValue(35)`

3. 35: `valueChanged(35)`, `setValue(35)`

4. 35:

在第 19 到 22 行中，我们使用布局管理器布局了数字框和滑动条组件。布局管理器是一个对象，负责设置其管理范围内组件的大小和位置。Qt 有三个主要的布局管理器类：

- `QHBoxLayout` 从左到右水平布局组件（对于某些文化背景为从右到左）。
- `QVBoxLayout` 从上到下垂直布局组件。
- `QGridLayout` 以网格形式布局组件。

![](img/5a524abdf0b0d58fa99d30abb4463611_35_0.png)

## 组件样式

我们目前看到的截图是在 Linux 上拍摄的，但 Qt 应用程序在所有支持的平台上看起来都是原生的。Qt 通过模拟平台的视觉效果来实现这一点，而不是封装特定平台或工具包的组件集。预定义样式

![](img/5a524abdf0b0d58fa99d30abb4463611_36_0.png)

Plastique 样式是运行在 KDE 下 Qt/X11 应用程序的默认样式。与其他样式不同，Windows XP、Vista 和 Mac 样式仅在其平台上可用，因为它们依赖原生引擎。要使用 Motif 样式启动应用程序，只需使用以下命令：

```bash
./age -style motif
```

首页“API Reference”部分的链接提供了导航 Qt 类的方法。“All Classes”页面列出了 Qt 中的所有类。“Main Classes”页面列出了最常用的 Qt 类。作为练习，你可能想查找本章中用过的类和函数。

### 图 1.7. 年龄应用程序的组件与布局

![](img/5a524abdf0b0d58fa99d30abb4463611_37_0.png)

尽管我们没有显式地设置任何组件的位置或大小，`QSpinBox` 和 Slider 看起来也并齐排列在一起。这是因为 `QHBoxLayout` 根据组件的需求自动为其分配了合理的位置和大小。布局管理器让我们免于在应用程序中硬编码屏幕位置的工作，并确保窗口能够流畅地缩放。

Qt 构建用户界面的方法简单易懂且灵活。Qt 程序员使用的常用模式是实例化所需的组件，然后根据需要设置它们的属性。将组件添加到布局中，布局会自动处理尺寸和定位。用户界面的行为通过 Qt 的信号和槽连接组件来管理。

## 使用参考文档

Qt 参考文档是 Qt 开发者必备的工具，因为它涵盖了 Qt 中的每一个类和函数。本书使用了许多类和函数，但并没有涵盖所有内容，也没有对提到的内容提供细节。为了从 Qt 中获得最大收益，你应该尽快熟悉 Qt 参考文档。

文档以 HTML 格式存储在 Qt 的 `doc/html` 目录下，可以使用任何网络浏览器阅读。你也可以使用 Qt Assistant（Qt 帮助浏览器），它强大的搜索和索引功能使其比网络浏览器更快、更方便。要启动 Qt Assistant，在 Windows 菜单中点击“Qt Trolltech v4.x.y Assistant”，在命令行中输入 `assistant`，或在 Mac OS X Finder 中双击 `Assistant`。

### 图 1.8. Windows Vista 上 Qt Assistant 中的 Qt 文档

![](img/5a524abdf0b0d58fa99d30abb4463611_38_0.png)

注意，继承的函数记录在基类中；例如，`QPushButton` 没有自己的 `show()` 函数，但它继承自 `QWidget`。

图 1.9 显示了我们目前为止看到的类之间的关系。

![](img/5a524abdf0b0d58fa99d30abb4463611_39_0.png)

当前版本的 Qt 以及某些早期版本的参考文档可以在 http://doc.trolltech.com/ 在线获取。该网站还收了《Qt 季度刊》（Qt Quarterly）的精选文章，这是一份发送给所有商业许可者的 Qt 程序员通讯。

本章介绍了信号槽连接（signal-slot connections）和布局的核心概念。它还开始揭示 Qt 在构建和使用部件时一贯且完全面向对象的方法。如果你浏览 Qt 文档，你会发现其方法的统一性，这使得学习如何使用新部件变得非常简单；你还会发现 Qt 为函数、参数、枚举等精心选择的名称，使得在 Qt 中编程变得出乎意料地愉悦和简单。

第一部分的后续章节将建立在本章介绍的基础之上，展示如何创建带有菜单、工具栏、文档窗口、状态栏和对话框的完整 GUI 应用程序，以及读取、处理和写入文件的底层功能。

## 2. 创建对话框

![](img/5a524abdf0b0d58fa99d30abb4463611_40_0.png)

- 子类 `QDialog`
- 深入理解信号与槽
- 快速对话框设计
- 变形对话框
- 内置部件和对话框类

本章将教你如何使用 Qt 创建对话框。对话框为用户提供选项和选择，允许他们将选项设置为其偏好值并做出选择。它们被称为对话框（dialog boxes），或简单称为“对话框”（dialogs），因为它们提供了一种用户与应用程序之间“对话”的方法。

大多数 GUI 应用程序由一个带有菜单栏和工具栏的主窗口以及几十个辅助主窗口的对话框组成。也可以创建通过执行相应操作直接响应用户选择的对话框应用程序（例如计算器应用程序）。

我们将通过编写代码来创建第一个对话框，展示如何进行操作。然后，我们将看到如何使用 Qt Designer（Qt 的可视化设计工具）来构建对话框。使用 Qt Designer 比手写快得多，并且便于测试不同的设计并在以后更改设计。

### 子类 QDialog

我们的第一个示例是一个完全用 C++ 编写的查找对话框。它如图 2.1 所示。我们将该对话框作为一个独立的类来实现。通过这样做，我们使其成为一个独立的、自包含的组件，拥有它自己的信号和槽。

### 图 2.1. 查找对话框

![](img/5a524abdf0b0d58fa99d30abb4463611_40_1.png)

源代码跨越两个文件：`finddialog.h` 和 `finddialog.cpp`。

我们将从 `finddialog.h` 开始。

```
#ifndef FINDDIALOG_H
#define FINDDIALOG_H
#include <Q>
class QCheckBox;
class QLabel;
class QLineEdit;
class QPushButton;
```

第 1 行和 (2) 行以及第 27 行保护头文件防止多次包含。

第 3 行包含了 `QDialog` 的定义，它是 Qt 中对话框的基类。`QDialog` 继承自 `QWidget`。

第 4 到 7 行是我们将用于实现对话框的 Qt 类的的前向声明。前向声明告诉 C++ 编译器某个类存在，而无需提供类定义（通常位于其自己的头文件中）所拥的所有细节。稍后我们将进行详细说明。

接下来，我们将 `FindDialog` 定义为 `QDialog` 的子类：

```
class FindDialog : public QDialog
{
Q_OBJECT
public:
FindDialog(QWidget *parent = 0);
```

类定义开头的 `QOBJECT` 宏对于所有定义信号或槽的类都是必要的。

`FindDialog` 构造函数是典型的 Qt 部件类。`parent` 参数指定部件对话框。默认值是空指针，意味着对话框没有父对象。

```
signals:
void findNext(const QString &str, Qt::CaseSensitivity cs);
void findPrevious(const QString &str, Qt::CaseSensitivity cs);
```

`signals` 部分声明了对话框在用户点击 Find 按钮时发射的两个信号。如果启用了“向后搜索”选项，对话框发射 `findPrevious()`；否则，发射 `findNext()`。

`signals` 关键字是一个宏。C++ 预处理器会在编译器看到之前将其转换为标准的 C++。`Qt::CaseSensitivity` 是一个枚举类型，可以取 `Qt::CaseSensitive` 和 `Qt::CaseInsensitive` 值。

在类的私有部分中，我们声明了两个槽。为了实现这些槽，我们需要访问对话框的大多数子部件，因此我们也保留了指向它们的指针。`slots` 关键字和 `signals` 一样，是一个宏，会被展开为 C++ 编译器可以理解的内容。

对于私有变量，我们使用了它们类的前向声明。这是可能的，因为它们都是指针，且我们没有在头文件中访问它们，所以编译器不需要完整的类定义。我们本包含相关的头文件（`<QCheckBox>`、`<QLabel>` 等），但在可行时使用前向声明会让编译速度快快。

我们现在来看下 `finddialog.cpp`，它包含了 `FindDialog` 类的实现。

```
#include <QtGui>
#include "finddialog.h"
```

首先，我们包含了 `<QtGui>`，这是一个包含 Qt GUI 类定义的头文件。它由多个模块组成，每个模块都位于自己的库中。最常用的模块是 `QtCore`、`QtGui`、`Network`、`Script`、`Svg` 和 `Xml`。

在 `finddialog.h` 中，我们使用布局管理器来布局子部件。布局可以包含部件也可以包含其他布局。通过嵌套 `QHBoxLayout`、`QVBoxLayout` 和 `QGridLayout`，可以构建非常复杂的

```
FindDialog::FindDialog(QWidget *parent)
    : QDialog(parent)
{
    label = new QLabel(this);
    lineEdit = new QLineEdit(this);
    caseCheckBox = new QCheckBox("Match case", this);
    backwardCheckBox = new QCheckBox("Search backward", this);
    findButton = new QPushButton("Find", this);
    closeButton = new QPushButton("Close", this);

    QHBoxLayout *topLayout = new QHBoxLayout;
    topLayout->addWidget(label);
    topLayout->addWidget(lineEdit);

    QVBoxLayout *leftLayout = new QVBoxLayout;
    leftLayout->addWidget(topLayout);
    leftLayout->addWidget(caseCheckBox);
    leftLayout->addWidget(backwardCheckBox);

    QVBoxLayout *rightLayout = new QVBoxLayout;
    rightLayout->addWidget(findButton);
    rightLayout->addWidget(closeButton);
    rightLayout->addStretch();

    QHBoxLayout *mainLayout = new QHBoxLayout;
    mainLayout->addLayout(leftLayout);
    mainLayout->addLayout(rightLayout);
    setLayout(mainLayout);

    label->setText("Find:");
    findButton->setEnabled(false);
}
```

在 `finddialog.h` 中，我们使用 ampersands（&）来指示快捷键。例如，第 11 行创建了一个带有快捷键（Alt+F）的标签，我们在第 8 行将标签的 buddy 设置为行编辑器。buddy 是一个当按下标签快捷键时会被激活的部件。

在 `finddialog.cpp` 中，我们包含了信号和槽的实现。

```cpp
void FindDialog::findNext(const QString &str, Qt::CaseSensitivity cs)
{
    // ...
}

void FindDialog::findPrevious(const QString &str, Qt::CaseSensitivity cs)
{
    // ...
}

void FindDialog::enableFindButton(const QString &text)
{
    // ...
}

void FindDialog::clicked()
{
    // ...
}

void FindDialog::close()
{
    // ...
}
```

对于查找（Find）对话框，我们使用了两个 `QHBoxLayout` 和两个 `QVBoxLayout`，如图 2.2 所示。最外层布局是主布局；它在第 35 行安装在 `FindDialog` 上，负责对话框的整个区域。另外三个布局是子布局。图 2.2 右下角的小“弹簧”是一个间距项（或“拉伸”项）。它使用了查找（Find）和关闭（Close）按钮下方的空白空间，确保这些按钮占据它们所在布局的顶部。

### 图 2.2 查找对话框的布局

![](img/5a524abdf0b0d58fa99d30abb4463611_45_0.png)

布局管理器类的一个微妙之处是它们不是控件。相反，它们派生自 `QLayout`，而 `QLayout` 又派生自 `QObject`。在图中，控件用实线框表示，布局用虚线框表示，以突出它们之间的区别。在运行应用程序中，布局是不可见的。

当子布局被添加到父布局时（第 25、33 和 34 行），子布局会自动重新设置父对象（reparented）。然后，当主布局安装到对话框上（第 35 行）时，它成为对话框的子，布局中的所有控件都会重新设置父对象成为对话框的子。生成的父子层级关系如图 2.3 所示。

```
36     setWindowTitle(tr("Find"));
37     setFixedHeight(sizeHint().height());
38 }
```

### 图 2.3 查找对话框的父子关系

最后，我们设置了显示在对话框标题栏的标题，并设置了窗口固定高度，因为对话框中没有控件可以有意义地占据额外的垂直空间。`QWidget::sizeHint()` 返回控件的“理想”尺寸。

到此，对 `FindDialog` 构造函数的审查结束。由于我们使用 `new` 来创建对话框的控件和布局，似乎我们需要编写一个析构函数来对创建的每个控件和布局调用 `delete`。这是必要的，因为 Qt 在父对象被销毁时会自动删除子对象，而子控件和布局都是 `FindDialog` 的后代。

现在我们来看对话框的槽：

```
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

```
51 void FindDialog::enableFindButton(const QString &text)
52 {
53     findButton->setEnabled(!text.isEmpty());
54 }
```

当用户点击查找按钮时，会调用 `findClicked()` 槽。它根据搜索选项发射 `findPrevious()` 或 `findNext()` 信号。

`emit` 关键字是 Qt 特有的；与其他 Qt 扩展不同，它会被 C++ 预处理器转换为标准的 C++。

每当用户更改行内编辑器中的文本时，就会调用 `enableFindButton()` 槽。如果编辑器中有某些文本，则启用该按钮，否则禁用它。

这两个槽函数完成了对话框的编写。我们现在可以创建一个 `main.cpp` 文件来测试我们的 `FindDialog` 控件：
