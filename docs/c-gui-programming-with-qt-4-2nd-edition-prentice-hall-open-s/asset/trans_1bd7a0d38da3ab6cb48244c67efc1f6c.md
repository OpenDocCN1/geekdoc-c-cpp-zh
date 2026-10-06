

# Qtopia APIs

Qtopia Edition 和 Qtopia Phone Edition 提供了一组与移动设备用户相关的应用程序。这些应用程序的大多数功能都被抽象为库，或者使用了特定于版本的库。这些库可以在我们自己的 Qtopia 应用程序中使用，使我们能够访问设备服务，如闹钟、电子邮件、电话拨号、短信、语音录制等。

如果我们想从应用程序中访问设备特定功能，有许多选择：

- 我们可以使用 Qt/Embedded Linux 并编写自己的代码来与设备交互。
- 我们可以获取现有的 Qtopia 应用程序并对其修改以实现我们需要的功能。
- 可以使用额外的 API 进行编写，例如 Qtopia Phone API 或 Qtopia PIM（个人信息管理器）应用程序库。

在本节中，我们将采用最后一种方法。我们将编写一个简单的应用程序，用于记录简单的开支信息。它利用 Qtopia PIM 的数据弹出一个联系人列表，然后将开支报告作为短信消息发送给选定的联系人。它还演示了如何使用 Qtopia 对大多数手机上常见的多功能“软键”的支持。

如图 24.4 所示，该应用程序将出现在应用程序包列表中，就像我们在上一节中构建的示例一样。和之前一样，我们将首先查看 .pro 文件，然后是 .desktop 文件，最后是应用程序的源代码。这里是 expenses.pro：

```
qtopia_project(qtopia app)
depends(libraries/qtopiapim)

CONFIG += qtopia_main no_quicklaunch
HEADERS += expensedialog.h \
expensewindow.h \
SOURCES += expense.cpp \
expensedialog.cpp \
expensewindow.cpp \
main.cpp

INSTALLS += desktop pics

desktop.files = expenses.desktop
```

```
deskt = appsApplications
desktop.hint = desktop
pics.files = pics/*
pics.path = picsexenses
pics.hint = pics

pkg.name = expenses
pkg.desc = A program to record and SMS expenses
pkg.version = 1.0.0
pkg.domain = window
```

## 图 24.4. 定位并运行 Expenses 应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_943_0.png)

qtopia_project() 行与之前相同。由于此应用程序依赖于 Qtopia PIM 库，我们使用 depends() 指令来指定该库。如果想使用多个库，可以通过逗号将它们分开。.pro 文件的其余部分与我们在单元转换器示例中看到的相似，这次我们有更多源文件，因为该应用程序更加复杂。

expenses.desktop 文件与我们之前看到的非常相似：

```
[Desktop Entry]
Comment[]=A program to record and SMS expenses
Exec=expenses/expenses
Icon=expenses/expenses
Type=Application
Name[]=Expenses
```

main.cpp 也是如此：

```cpp
#include <QtopiaApplication>
```

```cpp
#include "expensewindow.h"

QTOPIA_ADD_APPLICATION("Expenses", ExpenseWindow)
QTOPIA_MAIN
```

我们现在将查看 Expenses 应用程序的头文件以及源代码中与 Qtopia 特有或特别相关的部分，从 Expense 类开始：

```cpp
class Expense
{
public:
    Expense();
    Expense(const QDate &date, const QString &desc, qreal amount);

    bool isNull(const);
    void setState(const QDate &date);
    QDate date() const;
    void setDescription(const QString &desc);
    QString description() const;
    void setAmount(qreal amount);
    qreal amount() const;

private:
    QDate my;
    QString myDesc;
    qreal myAmount;
};
```

这个简单的类包含一个日期、描述和金额。我们不会回顾 expense.cpp 文件，因为它的代码中没有 Qtopia 特有的，而且非常简单。

```cpp
class ExpenseWindow : public QMainWindow
{
public:
    Q_OBJECT
    ExpenseWindow(QWidget parent = 0, Qt::WFlags flags = 0);
protected:
    void closeEvent(QCloseEvent event);
private slots:
    void add();
```

```cpp
void edit();
void del();
void send();
void clear();

private:
void createActions();
void createMenuToolbar();
void loadData();
void showData();
...
QList<Expense> expenses;
};
```

ExpenseWindow 是应用程序的主表单。它为用户提供了添加、编辑和删除单个开支项、发送包含所有项的短信以及清除它们的功能。开支以值的形式存储在 QList<Expense> 中。

构造函数创建一个 QListWidget 和两个 QLabel。一个标签显示文本“Total”，另一个显示开支总和。动作由 createActions() 创建，菜单或工具栏由 createMenuToolbar() 创建。预存在的开支在构造函数结束时通过调用 loadData()加载。我们将跳过构造函数本身，而是回顾它调用的函数：

```cpp
void ExpenseWindow::createActions() {
addAction = new QAction(tr("Add"), this);
addAction->setIcon(QIcon(":icon/add"));
connect(addAction, SIGNAL(triggered()), this, SLOT(add));
...
clearAction = new QAction(tr("Clear"), this);
clearAction->setIcon(QIcon(":icon/clear"));
connect(clearAction, SIGNAL(triggered()), this, SLOT(clear));
}
```

createActions() 函数创建了 Add、Edit、Delete、Send 和 Clear 动作。虽然可以使用资源文件 (.qrc)，但在处理 Qtopia 应用程序时，图标的标准做法是将它们存储在 pics 目录中，并复制到设备上（得益于 .pro 中的 INSTALLS 行）。它们可以在多个应用程序之间共享，Qtopia 会对其进行优化。

在 Qt 或 Qtopia 期望提供文件名的地方，我们可以提供 Qtopia 资源。这些资源通过文件名开头的冒号识别，后跟指定资源种类的单词。在这种情况下，我们指定需要图标并给出一个文件名，例如：:icon/add，省略文件扩展名。Qtopia 将在多个标准位置查找合适的图标。详见：doc.qt.com/qtopia-resource.html。

```cpp
void ExpenseWindow::createMenuToolbar() {
#ifdef QTOPIA_PHONE
    QMenuBar menu = new QMenuBar;
#else
    QToolBar toolbar = new QToolBar;
#endif
...
}
```

某些手机具有“软键”，即其操作取决于上下文的多功能键。对于 PDA，我们通常有一个工具栏而不是弹出菜单。用户期望能够关闭应用程序而无需强制显式保存数据。他们还期望在稍后重新启动应用程序时恢复数据。这通过在构造函数中调用 loadData()并在 closeEvent() 中保存数据可以轻松实现。Qtopia 提供了许多数据存储选择，包括保存到 SQLite 数据库或保存到文件。由于开支数据非常小，我们将使用 QSettings。我们将查看它是如何保存的，然后查看它是如何加载的。

```cpp
void ExpenseWindow::closeEvent(QEvent *event)
{
    ByteArray data;
    QDataStream out(&data, QIODevice::WriteOnly);
    out.setVersion(QDataStream::Qt_4_2);

    foreach (Expense expense, expenses) {
        out << expense.date() << expense.description()
        << expense.amount();
    }

    QSettings settings("BookSoft Ltd", "Expenses");
    settings.setValue("data", data);

    event->accept();
}
```

```cpp
void ExpenseWindow::loadData() {
    QSettings settings("BookSoft Ltd", "Expenses");
    QByteArray data = settings.value("data").toByteArray();
    if (data.isEmpty()) {
        return;
    }

    expenses.clear();
    QDataStream in(&data, QIODevice::ReadOnly);
    in.setVersion(QDataStream::Qt_4_2);

    while (!in.atEnd()) {
        QDate date;
        QString desc;
        qreal amount;

        in >> date >> desc >> amount;
        expenses.append(Expense(date, desc, amount));
    }
    showData();
}
```

如果存在之前会话的数据，我们将清除现有数据，然后读取每个新的开支项。showData() 函数清除列表部件，然后

