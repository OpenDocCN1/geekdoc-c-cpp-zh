
```cpp
employeeView->setColumnHidden(Employee_DepartmentId, true);

employeeView->setColumnHidden(Employee_StartDate, true);

employeeLabel = new QLabel(tr("Employees"));

employeeLabel->setBuddy(employeeView);
```
员工视图的编辑触发器设置为 `QAbstractItemView::NoEditTriggers`，实际上使该视图变为只读。在此应用程序中，用户可以通过点击“编辑员工”来添加、编辑和删除员工记录，这会调用上一节中的 `EmployeeForm`。

这一次我们隐藏了三列而不仅仅列。我们隐藏了 `id` 列，因为这对用户来说没有意义。我们还隐藏了 `departmentid` 列，因为任何时候显示的员工都是当前选择部门的员工。最后，我们隐藏了 `startDate` 列，因为它很少相关，并且可以通过点击“编辑员工”来访问。

```cpp
void MainForm::updateEmployeeView() {
    QIndex index = departmentView->currentIndex();
    if (index.isValid()) {
        SqlRecord record = departmentModel->record(index.row());
        int id = record.value("id").toInt();
        employeeModel->setFilter(QString("department = %1").arg(id));
        employeeLabel->setText(tr("E&employees in the %1 Department").arg(record.value("name").toString()));
    } else {
        employeeModel->setFilter("department = -1");
        employeeLabel->setText(tr("E&employees"));
    }
}
```

```cpp
employeeModel->select();
employeeView->horizontalModel->setVisible(
employeeModel->rowCount() > 0);
}
```

每当当前部门发生变化时（包括启动时），此槽就会被调用。如果存在有效的部门，该函数将获取部门的 ID 并在员工模型上设置过滤器。这会将员工限制为那些具有匹配部门 ID 外键的员工。（过滤器仅仅是不带 WHERE 关键字的 WHERE 子句。）我们还会更新显示在员工上方的标签，以显示员工所属部门的名称。

如果没有有效的部门（例如数据库为空），我们将设置过滤器以匹配一个不存在的部门 ID，以确保没有记录匹配。

然后，我们对模型调用 `select()` 以应用过滤器。反过来，模型将发出信号，视图将通过响应这些信号来更新自身。最后，我们根据是否显示了员工来显示或隐藏员工的列标题。

```cpp
void MainForm::addDepartment()
{
    int row = departmentModel->rowCount();
    departmentModel->insertRow(row);
    QModelIndex index = departmentModel->index(row, Department_Name);
    departmentView->setCurrentIndex(index);
    departmentView->edit(index);
}
```

如果用户点击“添加部门”（Add Dept.）按钮，我们在部门表的末尾插入新行，使此行变为当前行，并启动部门名称列的编辑，就像用户按了 F2 或双击了它一样。如果我们需要提供某些默认值，将通过调用 `insertRow()` 来。

我们不需要担心为新记录创建唯一键，因为我们使用了自增列来为我们处理此工作。如果这种方法不可行或不，我们连接到模型的 `beforeInsert()` 信号。该信号在用户编辑之后、数据库执行插入之前发出。还有类似的 `beforeDelete()` 和 `beforeUpdate()`。

```cpp
void MainForm::deleteDepartment()
{
    QModelIndex index = departmentView->currentIndex();
    if (!index.isValid()) {
        return;
    }
    QSqlDatabase::database().transaction();
    QSqlRecord record = departmentModel->index(index.row());
    int id = record.value(Department_Id).toInt();
    int numEmployees = 0;
    QSqlQuery query(QString("SELECT COUNT(*) FROM employee "
        "WHERE departmentid = %1").arg(id));
    if (query.next()) {
        numEmployees = query.value(0).toInt();
        if (numEmployees > 0) {
            int r = QMessageBox::warning(this, tr("Delete Department"),
                tr("Delete %1 and all its employees?")
                .arg(record.value(Department_Name).toString()),
                QMessageBox::Yes | QMessageBox::No);
            if (r == QMessageBox::No) {
                QSqlDatabase::database().rollback();
                return;
            }
        }
        query.exec(QString("DELETE FROM employee "
            "WHERE departmentid = %1").arg(id));
    }
    departmentModel->removeRow(index.row());
    departmentModel->removeAll();
    QSqlDatabase::database().commit();
}
```

如果用户想要删除一个部门，如果该部门没有员工，我们可以让他们直接删除。但如果有员工，我们会要求用户确认删除，如果他们确认了，我们将执行级联删除以确保维护关系的完整性。为了实现这一点，至少对于不为我们强制执行关系完整性的 SQLite 3 等数据库，我们必须使用事务。

一旦启动事务，我们就会执行查询来查找该部门中有多少员工。如果至少有一个，我们会弹出一个消息框请求确认。如果用户说“否”，我们将回滚事务并返回。否则，我们将删除该部门的所有员工以及部门本身，并提交事务。

```cpp
void MainForm::editEmployees(){
    int employeeId = -1;
    QModelIndex index = employeeView->currentIndex();
    if (index.isValid()){
        QSqlRecord record = employeeModel->record(index.row());
        employeeId = record.value(Employee_Id).toInt();
    }
    EmployeeForm form(employeeId, this);
    form.exec();
    updateEmployeeView();
}
```

每当用户点击“编辑员工”（Edit Employees）按钮时，就会调用 `editEmployees()`。我们分配一个无效的员工 ID。如果可能，我们将用当前员工的 ID 覆盖它。然后我们构造 `EmployeeForm` 并模态显示它。最后，我们调用 `updateEmployeeView()` 槽来让表单的详情视图刷新自身，因为可能发生了员工的变化。

本章展示了 Qt 的视图类使得在 SQL 数据库中查看和编辑数据尽可能简单。在那些希望使用表单视图展示记录的情况下，可以使用 `QDataMapper` 将小部件映射到用户界面与数据库记录的字段上。设置主从关系是非常简单的，只需要一个信号-槽连接并实现一个简单的槽。钻取（Drill-down）也很直观，只需要在钻取表单的构造函数中导航到选中的记录，或者在未选择记录时跳转到第一条记录。

## 4. 多线程

![](img/5a524abdf0b0d58fa99d30abb4463611_536.png)

- 创建线程
- 同步线程
- 与主线程通信
- 使用 Qt 类

在主线程中使用 Qt 类

传统的 GUI 应用只有一个线程，一次执行一个操作。如果从用户界面调用耗时操作，界面通常会冻结。第 7 章提供了一些解决方案。多线程是另一种解决方案。

在多线程应用程序中，GUI 运行在自己的线程中。在单处理器上运行时，多线程应用程序由于线程开销运行得比单线程慢。但在日益常见的多处理器系统上，多线程应用程序可以同时执行多个线程，从而提高性能。

在本章中，我们将首先展示如何子类 `QThread` 以及如何使用 `QMutex`、`QSemaphore` 和 `QWaitCondition` 来同步线程。我们将看到如何从辅助线程与主线程通信。最后，我们将回顾哪些类可以使用辅助线程哪些不能。

多线程是一个巨大的课题，有很多书籍致力于该主题，例如《Threads Primer: A Guide to Multithreaded Programming》（Bill Lewis and Daniel J. Berg, Prentice Hall, 1995）和《Multithreaded, Parallel, and Distributed Programming》（Gregory Andrews, Addison-Wesley, 2000）。这里假设你已经理解多线程编程的基础，所以重点是如何开发多线程应用程序 own线程本身。

### 创建线程

在 Qt 应用中提供多线程是非常直接的：我们只需要子类 `QThread` 并重写 `run()` 函数。为了展示它是如何工作的，我们将首先回顾一个反复在控制台打印字符串的简单 QThread 子类的代码。该应用程序的用户界面如图 14.1 所示。

```cpp
class Thread : public QThread
{
    Q_OBJECT
public:
    Thread();
    void setMessage(const QString &message);
    void stop();
protected:
    void run();
private:
    QString messageStr;
    volatile bool stopped;
};
```

### 图 14.1. Threads 应用

![](img/5a524abdf0b0d58fa99d30abb4463611_537.png)

`stopped` 变量被声明为 `volatile` 是因为它被不同的线程访问，并且我们希望确保每次需要它时都是新鲜读取的。如果我们省略了 `volatile` 关键字，编译器可能会对变量进行优化，可能导致错误的结果。

```cpp
Thread::Thread()
{
    stopped = false;
}
```

我们在构造函数中将 `stopped` 设置为 `false`。

```cpp
void Thread::run()
{ 
    while (!stopped)
        std::cerr << QPrintable(messageStr);
    stopped = false;
    std::cerr << std::endl;
}
```

`run()` 函数被调用以开始执行线程。只要 `stopped` 变量为 `false`，该函数就会持续向控制台打印指定的的消息。当控制离开 `run()` 函数时，线程终止。

```cpp
void Thread::stop()
{
    stopped = true;
}
```

`stop()` 函数将 `stopped` 变量设置为 `true`，通知 `run()` 停止向控制台打印文本。此函数可以在任何线程的任何时间被调用。为了本示例的目的，我们假设对 `bool` 的赋值是一个原子操作。考虑到 `bool` 只有两种状态，这是一个合理的假设。我们将在本节稍后的部分介绍如何使用 `QMutex` 来保证对变量的赋值是原子操作。

`Thread` 提供了一个 `terminate()` 函数，可以在线程仍在运行时终止其执行。不建议使用 `terminate()`，因为它可能在任何点停止线程，并且没有给线程留下清理工作的机会。像我们这里这样使用 `stopped` 变量和 `stop()` 函数总是更安全的。

现在我们将展示如何在一个小型 Qt 应用程序中使用 `Thread` 类，该程序除了主线程外还使用了两个线程 A 和 B。

```cpp
class ThreadDialog : public QDialog
{
    Q_OBJECT
public:
    ThreadDialog(QWidget parent = 0);
protected:
    void closeEvent(QCloseEvent event);
public slots:
    void startOrStopThreadA();
    void startOrStopThreadB();
private:
    Thread threadA;
    Thread threadB;
    QPushButton threadAButton;
    QPushButton threadBButton;
    QPushButton *quitButton;
};
```

`ThreadDialog` 类声明了两个 `Thread` 类型的变量以及一些提供用户界面的按钮。

```cpp
ThreadDialog::ThreadDialog(QWidget *parent)
 : QDialog(parent)
{
    threadA.setMessage("A");
    threadB.setMessage("B");
    threadAButton = new QPushButton(tr("Start A"));
    threadBButton = new QPushButton(tr("Start B"));
    quitButton = new QPushButton(tr("Quit"));
    quitButton->setDefault(true);
    connect(threadAButton, SIGNAL(clicked()),
           this, SLOT(startOrStopThreadA()));
    connect(threadBButton, SIGNAL(clicked()),
           this, SLOT(startOrStopThreadB()));
    ...
```

在构造函数中，我们调用 `setMessage()` 让第一个线程反复打印 'A'，第二个线程打印 'B'。

```cpp
void ThreadDialog::startOrStopThreadA()
{
    if (threadA.isRunning()) {
        threadA.stop();
        threadAButton->setText(tr("Start A"));
    } else {
        threadA.start();
        threadAButton->setText(tr("Stop A"));
    }
```

当用户点击线程 A 的按钮时，`startOrStopThreadA()` 会在线程正在运行时运行时停止它，否则启动它。它还会更新按钮的文本。

```cpp
void ThreadDialog::startOrStopThreadB()
{
  if (threadB.isRunning()) {
    threadB.stop();
    threadBButton->setText(tr("Start B"));
  } else {
    threadB.start();
    threadBButton->setText(tr("Stop B"));
  }
}
```

`startOrStopThreadB()` 的代码在结构上相同。

```cpp
void ThreadDialog::closeEvent(QCloseEvent *event)
{
  threadA.stop();
  threadB.stop();
  threadA.wait();
  threadB.wait();
  event->accept();
}
```
