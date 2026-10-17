
这很少需要，因为当对象被删除时，Qt 会自动移除涉及该对象的所有连接。

要将信号连接到槽（或另一个信号），它们必须以相同顺序具有相同的参数类型：

```
connect(ftp, SIGNAL(rawCommandReply(int, const QString)),
      this, SLOT(processReply(int, const QString)));
```

特殊情况下，如果信号的参数比它连接的槽多，多出的参数将被简单忽略：

```
connect(ftp, SIGNAL(rawCommandReply(int, const QString)),
      this, SLOT(checkErrorCode(int)));
```

到目前，我们只在小部件使用了信号和槽。但该机制本身并不限于 GUI 编程。该机制可以被任何 `QObject` 子类使用：

```
class Employee : public QObject
{
    Q_OBJECT

public:
    Employee() { mySalary = 0; }

    int salary() const { return mySalary; }

public slots:
    void setSalary(int newSalary);

signals:
    void salaryChanged(int);

private:
    int mySalary;
};
```

![](img/5a52abdf0b0d58fa99d30abb446361_60_png)

## Qt 元对象系统

Qt 的成就之一是对 C++ 了一种扩展，允许组件在相互不知晓的情况下绑定。

该机制被称为元对象系统，它提供了两项关键服务：信号-槽和反射。反射功能对于实现信号和槽是必要的，并允许应用程序程序员在运行时获取 `QObject` 子类的元信息，包括支持的信号和槽列表以及类名。该机制还支持属性（Qt Designer 广泛使用）和文本翻译（国际化），并为 QtScript 模块奠定了基础。从 4.2 版本开始，可以动态添加属性，我们将在第 19 和 22 章看到这一特性。

标准 C++ 不支持 Qt 元对象系统所需的动态元信息。Qt 通过提供一个独立的工具 `moc` 来解决这个问题，它解析 `Q_OBJECT` 类定义并通过 C++ 函数提供这些信息。由于 `moc` 使用 C++ 实现所有功能，因此 Qt 的元对象系统适用于任何 C++ 编译器。

该机制的工作原理如下：

- `Q_OBJECT` 宏声明了一些每个 `QObject` 子类必须实现的反射函数：`metaObject()`、`tr()`、`qt_metacall()` 等。

- Qt 的 `moc` 生成由 `Q_OBJECT` 声明的函数以及所有信号的实现。

- `QObject` 成员函数（如 `connect()` 和 `disconnect()`）使用反射函数完成工作。

这一切都由 `qmake`、`moc` 和 `QObject` 自动处理，因此你很少需要考虑它。但如果你好奇，可以阅读 `QMetaObject` 类文档并查看 `moc` 生成的 C++ 源文件，以了解实现原理。

```cpp
mySalary = newSalary;
emit salaryChanged(mySalary);
}
```

注意 `setSalary()` 槽函数的实现。只有当 `newSalary != mySalary` 时，我们才发射 `salaryChanged()` 信号。这确保循环连接不会导致无限循环。

## 快速对话框设计

Qt 的设计目标是手工编写愉快且直观，程序员纯通过编写 C++ 源代码开发整个 C++ 应用程序并不罕见。尽管如此，许多程序员倾向于使用可视化方法来设计表单，因为他们认为这比手动编码更自然、更快，而且他们希望比手动编码表单更快速、方便地尝试不同的设计。

`Qt Designer` 通过提供可视化设计功能扩展了程序员的可用选项。`Qt Designer` 可用于开发应用程序的所有或部分表单。使用 `Qt Designer` 创建的表单最终会被 C++ 代码，因此 `Qt Designer` 可以配合传统的工具链使用，且对编译器没有特殊要求。

在本节中，我们将使用 `Qt Designer` 创建图 2.4 所示的“跳转单元格”对话框。无论是在代码中还是在 `Qt Designer` 中创建，创建对话框始终涉及相同的根本步骤：

- 1. 创建并初始化子控件。
- 2. 将子控件放入布局管理器中。
- 3. 设置标签顺序。
- 4. 建立信号与槽连接。
- 5. 实现对话框的自定义槽。

### 图 2.4. 跳转单元格对话框

![](img/5a524abdf0b0d58fa99d30abb4463611_63_0.png)

要启动 `Qt Designer`，在 Windows 的开始菜单中点击 `Qt by Trolltech v4.x.y|Designer`，在 Unix 命令行中输入 `designer`，或在 Mac OS Finder 中双击 `Designer`。当 `Qt Designer` 启动时，会弹出一个模板列表。点击“Widget”模板，然后点击“Create”（创建）。（带有底部按钮的对话框”模板看起来很有吸引力，但对于本示例，我们将手动创建 OK 和 Cancel 按钮以展示如何操作。）你现在应该有一个名为“Untitled”（无标题）的窗口。

`Qt Designer` 的用户界面由几个顶级窗口组成。如果你更喜欢 MDI 风格的界面（具有一个顶级窗口和若干个子窗口，如图 2.5 所示），点击 `EditPreferences`（编辑选项）并将用户界面模式设置为 `Docked Window`（停靠窗口）。

### 图 2.5. Windows Vista 上停靠窗口模式下的 Qt Designer

[查看完整尺寸]

![](img/5a524abdf0b0d58fa99d30abb4463611_64_0.png)

第一步是创建子控件并将它们放置在表单上。创建一个标签（label）、一个水平间距符（spacer）和两个按钮（push buttons）。对于每个项目，从 `Qt Designer` 的控件框中拖动其名称或图标，将其释放到表单上大致位置。间距符在最终表单中是不可见的，在 `Qt Designer` 中以蓝色弹簧的形式显示。

现在拖动表单的底部使其变短。这应该产生一个与图 2.6 类似的表单。不要在表单上定位控件上花费过多时间；Qt 的布局管理器稍后会精确地布局它们。

### 图 2.6. 带有某些控件的表单

![](img/5a524abdf0b0d58fa99d30abb4463611_64_1.png)

使用 `Qt Designer` 的属性编辑器设置每个控件的属性：

1. 点击文本标签。确保 `setName` 属性为 "`label`"，并将 1. `text` 属性设置为 `&Cell Location:`。
2. 点击行编辑器（line editor）。确保 `setName` 属性为 "`lineEdit`"。
3. 点击第一个按钮。将 `setName` 属性设置为 "`okButton`"，将 `enabled` 属性设置为 "`false`"，将 `text` 属性设置为 "`OK`"，并把 `defaultFocus` 属性设置为 "`true`"。
4. 点击第二个按钮。将 `setName` 属性设置为 "`cancelButton`"并把 `text` 属性设置为 "`Cancel`"。
5. 点击表单背景以选择表单本身。将 `setName` 属性设置为 "`GoToCell`"，并将 `windowTitle` 属性设置为 "`Go to Cell`"。

所有控件看起来都正常，但文本标签除外，它显示为 `&Cell Location`。进入允许你设置快捷伙伴（buddies）的特殊模式。点击标签并将红线拖到行编辑器上，释放。标签现在应该显示为 Cell Location（如图 2.7 所示），并将行编辑器作为其快捷伙伴。点击 `Edit Buddies` 退出伙伴模式。

### 图 2.7. 设置了属性的表单

![](img/5a524abdf0b0d58fa99d30abb4463611_65_0.png)

下一步是将控件布局在表单上：

- 1. 点击 Cell Location 标签，并在点击旁边的行编辑器时按住 Shift 键，这样两者都被选中。点击 `Lay Out Horizontally`（水平布局）。
- 2. 点击间距符，然后按住 Shift 键点击表单的 OK 和 Cancel 按钮。点击 `Lay Out Horizontally`（水平布局）。
- 3. 点击表单背景以取消所有选中项目，然后点击 `Lay Out Vertically`（垂直布局）。
- 4. 点击 `Adjust Size`（调整大小）将表单调整为所需尺寸。

表单上会出现已创建布局的线条，如图 2.8 所示。在运行表单时这些线条不会出现。

### 图 2.8. 带有布局的表单

![](img/5a524abdf0b0d58fa99d30abb4463611_66_0.png)

现在点击 `Edit Tab Order`（编辑标签顺序）。每个可以聚焦的控件旁边都会出现一个蓝色矩形数字，如图 2.9 所示。按照你希望的顺序依次点击每个控件，然后点击 `Edit Widgets` 退出标签顺序模式。

### 图 2.9. 设置表单的标签顺序

![](img/5a524abdf0b0d58fa99d30abb4463611_66_1.png)

要预览对话框，点击“Form Preview”（表单预览）菜单选项。反复按 Tab 键检查标签顺序。使用标题栏中的关闭按钮关闭对话框。

将对话框保存为 `gotocell` 目录下的 `gotocelldialog.ui`，并在同一目录下使用纯文本编辑器创建 `main.cpp`：

```cpp
#include <QApplication>
#include <QDialog>

#include "ui_gotocldialog.h"

int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    Ui::GoToCell ui;
    QDialog dialog;
    ui.setupUi(&dialog);
    dialog.show();

    return app.exec();
}
```

```cpp
void GoToCellDialog::lineEdit_textChanged()
{
    okButton->setEnabled(lineEdit->hasAcceptableInput());
}
```

在构造函数中，我们调用 `setupUi()` 来初始化表。由于多重继承，我们可以直接访问 `Ui::GoToCellDialog` 的成员。创建用户界面后，`setupUi()` 会自动将任何遵循 `on_objectName_signalName()` 命名规范的槽连接到相应 `objectName` 的信号。在我们的示例中，这意味着 `setupUi()` 将建立以下信号槽连接：

`connect(lineEdit, SIGNAL(textChanged(const QString &)), this, SLOT(on_lineEdit_textChanged()));`

在构造函数中，我们还设置了一个验证器来限制输入范围。包括 `QIntValidator`、`QDoubleValidator` 和 `QRegExpValidator`。这里我们使用了带有正则表达式 `[A-Za-z][1-9]{0-9]{2}` 的 `QRegExpValidator`，允许一个大写或小写字母，后面跟着 1 到 9 之间的数字，然后是两个或两个 0 到 9 之间的数字。（有关正则表达式的介绍，请参阅 `QRegExp` 类文档。）

通过将 `this` 传递给 `QRegExpValidator` 构造函数，我们使其成为 `GoToCellDialog` 对象的子。这样做，我们就不需要担心以后删除 `QRegExpValidator`；当父对象被删除时，它会被自动删除。

Qt 的父子机制在 `QObject` 中实现。当我们带父对象创建一个对象（控件、验证器或其他任何类型）时，父对象会将该对象添加到其子列表中。当父对象被删除时，它会遍历子列表并删除每个子。子对象也会删除它们的所有子，以此递归进行，直到为空。父子机制极大简化了内存管理，降低了内存泄漏的风险。我们必须调用 `delete` 的对象只有那些通过 `new` 创建且没有父对象的对象。如果在删除父对象之前删除子对象，Qt 会将该对象从父对象的子列表中移除。

对于控件，父对象具有额外的含义：子控件显示在父对象的区域内。当我们删除父控件时，子控件不仅会从内存中消失，还会从屏幕上消失。

在构造函数的末尾，我们将 `OK` 按钮连接到 `QDialog` 的 `accept()`。

`accept()` 将取消按钮连接到 `reject()` 槽。这两个槽都会关闭对话框，`accept()` 将结果设置为 `QDialog::Accepted`（等于 1），而 `reject()` 将结果设置为 `QDialog::Rejected`（等于 0）。当我们使用此对话框时，可以使用结果来判断用户是否点击了 OK 并据此操作。

`on_lineEdit_textChanged()` 槽根据行编辑器是否包含有效的单元格位置来启用或禁用 OK 按钮。`QLineEdit::hasAcceptableInput()` 使用我们在构造函数中设置的验证器。

对话框完成了。我们现在可以重写 `main.cpp` 来使用它：

```cpp
#include <Application>
```

```cpp
#include "gotocelldialog.h"
```

```cpp
int main(int argc, char argv[])
{
    QApplication app(argc, argv);
    GoToCellDialog *dialog = new GoToCellDialog;
    dialog->show();
    return app.exec();
}
```

使用 `qmake -project` 重新生成 `gotocell.pro`（因为我们已向项目添加源文件），运行 `qmake gotocell.pro` 更新 makefile，然后编译并运行应用程序。在行编辑器中输入“A12”，注意 OK 按钮变为可用。尝试输入一些随机文本以查看验证器如何工作。点击取消关闭对话框。

对话框工作正常，但对于 Mac OS 用户来说，按钮的布局方式不对的。我们选择单独添加按钮是为了演示如何操作，但实际上我们应该使用 `QDialogButtonBox`，它包含了我们指定的按钮，并根据运行程序的窗口系统以正确的方式展示它们，如图 2.10 所示。

### 图 2.10 Windows Vista 和 Mac OS 上的跳转单元格对话框

![](img/5a524abdf0b058fa99d30abb446111_0_0)

/5555524000000599993001_0_1.png)

为了让对话框使用 `QDialogButtonBox`，我们必须修改它的设计和代码。在 `Qt Designer` 中只需四个步骤：

- 1. 点击表（而不是任何控件或布局），然后点击“断开布局”（Break Layout）。
- 2. 点击并删除 OK 按钮、取消按钮、水平间距以及（空的）水平布局。
- 3. 将“按钮框”（Button Box）拖到单元格位置标签和行编辑器下方。
- 4. 点击表，然后点击“垂直布局”（Lay Out Vertically）。

如果我们只进行设计更改（例如更改对话框的布局和控件属性），就可以重新构建应用程序。在这里我们删除了一些控件并添加了一个新控件，在这种情况下通常也会修改代码。

我们必须做的修改都在 `gotialog` 文件中。以下是新代码：

```cpp
void GoToCellDialog::on_lineEdit_textChanged()
{
    ui->buttonBox->setEnabled(lineEdit->hasAcceptableInput());
}
```

`on_lineEdit_textChanged()` 槽根据行编辑器是否包含有效的单元格位置来启用或禁用 OK 按钮。`QLineEdit::hasAcceptableInput()` 使用我们在构造函数中设置的验证器。

对话框完成了。我们现在可以重写 `main.cpp` 来使用它：

```cpp
#include <Application>
```

```cpp
#include "gotocelldialog.h"
```

```cpp
int main(int argc, char argv[])
{
    QApplication app(argc, argv);
    GoToCellDialog *dialog = new GoToCellDialog;
    dialog->show();
    return app.exec();
}
```

使用 `qmake -project` 重新生成 `gotocell.pro`（因为我们已向项目添加源文件），运行 `qmake gotocell.pro` 更新 makefile，然后编译并运行应用程序。在行编辑器中输入“A12”，注意 OK 按钮变为可用。尝试输入一些随机文本以查看验证器如何工作。点击取消关闭对话框。

对话框工作正常，但对于 Mac OS 用户来说，按钮的布局方式不对。我们选择单独添加按钮是为了演示如何操作，但实际上我们应该使用 `QDialogButtonBox`，它包含了我们指定的按钮，并根据运行程序的窗口系统以正确的方式展示它们，如图 2.10 所示。

### 图 2.10 Windows Vista 和 Mac OS 上的跳转单元格对话框
