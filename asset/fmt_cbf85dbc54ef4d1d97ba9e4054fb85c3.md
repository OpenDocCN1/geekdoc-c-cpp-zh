
这个简单的类包含一个日期、描述和金额。我们不会回顾 `expense.cpp` 文件，因为它的代码中没有 Qtopia 特有的，而且非常简单。

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

`ExpenseWindow` 是应用程序的主表单。它为用户提供了添加、编辑和删除单个开支项、发送包含所有项的短信以及清除它们的功能。开支以值的形式存储在 `QList<Expense>` 中。

构造函数创建一个 `QListWidget` 和两个 `QLabel`。一个标签显示文本“Total”，另一个显示开支总和。动作由 `createActions()` 创建，菜单或工具栏由 `createMenuToolbar()` 创建。预存在的开支在构造函数结束时通过调用 `loadData()` 加载。我们将跳过构造函数本身，而是回顾它调用的函数：

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

`createActions()` 函数创建了 Add、Edit、Delete、Send 和 Clear 动作。虽然可以使用资源文件 `.qrc`，但在处理 Qtopia 应用程序时，图标的标准做法是将它们存储在 `pics` 目录中，并复制到设备上（得益于 `.pro` 中的 `INSTALLS` 行）。它们可以在多个应用程序之间共享，Qtopia 会对其进行优化。

在 Qt 或 Qtopia 期望提供文件名的地方，我们可以提供 Qtopia 资源。这些资源通过文件名开头的冒号识别，后跟指定资源种类的单词。在这种情况下，我们指定需要图标并给出一个文件名，例如：`:icon/add`，省略文件扩展名。Qtopia 将在多个标准位置查找合适的图标。详见：`doc.qt.com/qtopia-resource.html`。

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

某些手机具有“软键”，即其操作取决于上下文的多功能键。对于 PDA，我们通常有一个工具栏而不是弹出菜单。用户期望能够关闭应用程序而无需强制显式保存数据。他们还期望在稍后重新启动应用程序时恢复数据。这通过在构造函数中调用 `loadData()` 并在 `closeEvent()` 中保存数据可以轻松实现。Qtopia 提供了许多数据存储选择，包括保存到 SQLite 数据库或保存到文件。由于开支数据非常小，我们将使用 `QSettings`。我们将查看它是如何保存的，然后查看它是如何加载的。

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

如果存在之前会话的数据，我们将清除现有数据，然后读取每个新的开支项。`showData()` 函数清除列表部件，然后遍历并更新总金额标签，为每项支出添加一个新的列表项，并完成。

一旦应用程序运行，用户就可以添加、编辑或删除开支项，将它们全部通过短信消息发送，或者清除所有条目。

对于删除操作，我们检查列表小部件（list widget）中是否存在有效行，然后使用标准的 `QMessageBox::warning()` 静态方便函数请求用户确认删除。如果用户选择清除所有开支，我们再次使用消息对话框。这是标准的 Qt 编程方式。Qtopia 负责确保消息对话框显示并正确集成到 Qtopia 环境中。

如果用户选择“添加”选项来添加新的开支项，将调用 `add()` 槽：

```
void ExpenseWindow::add()
{
    ExpenseDialog dialog(Expense(), this);
    if (QtopiaApplication::execDialog(&dialog)) {
        expenses.append(dialog.expense());
        showData();
    }
}
```

该槽函数创建了一个 `ExpenseDialog` 对象（我们稍后会查看这个类），但我们没有调用对话框的 `QDialog::exec()` 函数，而是调用 `QtopiaApplication::execDialog()`，并将对话框作为参数传递。调用 `exec()` 是完全有效的且可以工作，但使用 `execDialog()` 可以确保对话框在小型设备上具有适当的尺寸和位置，并在必要时将其最大化。

`edit()` 槽函数也类似类似。当 `edit()` 函数被调用时，它会检查列表小部件中是否存在有效行，如果是，它会将与该行对应的开支作为第一个参数传递给 `ExpenseDialog` 构造函数。如果用户接受编辑，原始开支的详情将用编辑后的详情覆盖。

我们将涵盖的最后一个 `ExpenseWindow` 函数是 `send()`，但在那之前，我们先讨论 `ExpenseDialog` 类：

```
class ExpenseDialog : public QDialog
{
    Q_OBJECT
public:
```

```
ExpenseDialog(const Expense &expense, QWidget *parent = 0);
Expense expense() const { return currentExpense; }
```

```
public slots:
  void accept();
```

```
private:
```

```
  void createActions();
  void createMenuToolbar();
  Expense currentExpense;
  ..
```

一个显而易见的方面是，我们拥有创建动作以及菜单或工具栏的函数，就像在 `ExpenseWindow` 中一样。我们不会创建 `QPushButton` 或 `QDialogButton`，而是创建一个工具栏或 `QMenuBar`，因为这些比按钮能与 Qtopia 环境提供更好的集成。代码与我们为应用程序主窗口编写非常相似：

```
void ExpenseDialog::createActions()
{
  okAction = new QAction(tr("OK"), this);
  okAction->setIcon(QIcon(":icon/ok"));
  connect(okAction, SIGNAL(triggered()), this, SLOT(accept()));
  cancelAction = new QAction(tr("Cancel"), this);
  cancelAction->setIcon(QIcon(":icon/cancel"));
  connect(cancelAction, SIGNAL(triggered()), this, SLOT(reject()));
}
```

```
void ExpenseDialog::createMenuToolbar()
{
#ifdef QTOPIA_PHONE
QMenu menuToolbar = QMenuBar::menuFor(this);
#else
  QToolbar menuToolbar = new QToolbar;
  menuToolbar->setMovable(false);
  addToolbar(menuToolbar);
#endif
  menuToolbar->addAction(okAction);
  menuToolbar->addAction(cancelAction);
}
```

如果用户接受当前对话框，我们将设置当前开支的日期、描述和金额属性，并让调用者通过对话框的 `expense()` 函数检索这些信息。

如果用户选择“发送”动作，将调用 `send()` 函数。该函数提示用户选择联系人来发送开支，准备要发送的消息文本，然后使用 SMS 协议发送消息（见图 24.5）。

```
void ExpenseWindow::send()
{
    QContactSelector dialog(false, this);
    dialog.setModel(new QContactModel);
    QtopiaApplication::execDialog(&dialog);
    if (!dialog.contactSelected())
        return;
```

# 图 24.5 选择联系人并发送短信

![](img/5a524abdf0b0d58fa99d30abb4463611_950_0.png)

`QContactSelector` 对话框和 `QContactModel` 模型/视图类都由 PIM 库提供。`QContactModel` 访问用户的联系联系数据库。如果联系人超过几个，`QtopiaApplication::execDialog()` 将以最大化的方式弹出 `QContactSelector` 对话框。如果用户没有选择联系人，`contactSelected()` 返回一个空联系人（求值为 false），在这种情况下我们什么都不做。否则，我们准备并发送开支：

代码视图：

```
QTemporaryFile file;
file.setAutoRemove(false);
if (file.open()) {
    QMessageBox::warning(this, tr("Expenses",
        tr("Failed to send expenses: %1")
        .arg(file.errorString()));
    return;
}
```

```
QString fileName = file.fileName();
real total = 0.00;
QTextStream out(&file);
out.setCodec("UTF-8");
out << tr("Expenses\n");
foreach (Expense expense) {
    out << tr("%1 $%2 %3\n")
        .arg(expense.date()).toString(Qt::ISODate)
        .arg(expense.amount(), 0, 'f', 2)
        .arg(expense.description());
    total += expense.amount();
}
out << tr("Total $%1\n").arg(total, 0, 'f', 2);
file.close();
```
为了发送短信，我们需要传递包含短信的文件名。在这里我们使用 `QTextStream` 将开支数据写入临时文件。通常 `QTemporaryFile` 在我们调用 `close()` 后会自动删除文件，但我们需要在短信发送前保留它。`total` 变量声明为 `real` 类型。该类型根据架构定义为 `float` 或 `double`。

```
QContact contact = dialog.selectedContact();
QtopiaServiceRequest request("SMS",
    "writeSMS(QString, QString)");
request << tr("%1 %2").arg(contact.name()).arg(fileName);
```
