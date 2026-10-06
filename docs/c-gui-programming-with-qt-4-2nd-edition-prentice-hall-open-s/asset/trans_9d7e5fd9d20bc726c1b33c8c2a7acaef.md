

```
RC_FILE        = objectsafetyimpl.cpp
DEF_FILE        = qaxserver.def
```

.pro 文件引用的 qaxserver.rc 和 qaxserver.def 文件是标准文件，可以从 Qt 的 `src\activeqt\control` 目录复制。
make 生成的 makefile 或 Visual C++ 项目文件包含了在 Windows 注册表中注册服务器的规则。要在终端用户机器上注册服务器，我们可以使用所有 Windows 系统都可用的 `regsvr32` 工具。
然后我们可以使用 `<object>` 标签在 HTML 页面中包含 Bouncer 组件：

```
<object id="AxBouncer" classid="clsid:5e2461aa-a3e8-4f7a-8b04-307549a4c08c"><<b>The ActiveX control is not available. Make sure you have built and registered the component server.</b></object>
```

我们可以创建调用槽的按钮：
<input type="button" value="Start" onclick="AxBouncer.start()">
<input type="button" value="Stop" onclick="AxBouncer.stop()">

我们可以像管理其他 ActiveX 控制一样使用 JavaScript 或 VBScript 管理小部件。查看书中示例包含的 `demo.html` 文件，这是一个使用 ActiveX 服务器的简单页面。

我们的最后一个示例是一个可脚本的地址录应用程序。该应用程序可以作为一个标准的 Qt/Windows 应用程序，也可以作为一个进程外 ActiveX 服务器。后一种允许我们对应用程序进行脚本化，例如 Visual Basic。

代码视图：

```
class AddressBook : public QMainWindow
{
    Q_OBJECT
    Q_PROPERTY(int count READ count)
    Q_CLASSINFO("CLASSID", "{S58114ef-110d-42eb-95ab-ee6a478b576d}")
    Q_CLASSINFO("InterfaceID", "{718780ec-b30c-4d88-b3b3-79b3d9e78502}")
    Q_CLASSINFO(ToSuperClass, "AddressBook")
public:
```

```
AddressBook(QWidget *parent = 0);
~AddressBook();

int count() const;
```

```
public slots:
ABIBItem createEntry(const QString &contact);
ABIBItem findEntry(const QString &contact) const;
ABIBItem entryAt(int index) const;
```

```
private slots:
void addEntry();
void editEntry();
void deleteEntry();
```

```
private:
void createActions();
void createMenus();
```

```
QTreeWidget treeWidget;
QMenu fileMenu;
QMenu editMenu;
Action exitAction;
Action addEntryAction;
QAction editEntryAction;
QAction deleteEntryAction;
```

AddressBook 小部件是应用程序的主窗口。该部件的属性及其公共槽将可用于脚本化。`Q_CLASSINFO()` 宏用于指定与类相关的类和接口 ID。这些是使用如 `guid` 或 `uuid` 等工具生成的。

在上一个示例中，当我们使用 `QAXFACTORY_DEFAULT()` 宏导出 QAxBouncer 时指定了类和接口 ID。在这个示例中，我们想要导出多个类，因此不能使用 `QAXFACTORY_DEFAULT()`。有两种方案可用：

- 我们可以派生 `QFactory` 类，重新实现其虚函数以提供有关我们要导出的类型的信息，并使用 `QAXFACTORY_EXPORT()` 宏来注册工厂。

- 我们可以使用 `QAXFACTORY_BEGIN()`、`QAXFACTORY_END()`、`QAXCLASS()` 和 `QAXTYPE` 宏来声明并注册工厂。这种方法需要使用 `Q_CLASSINFO()` 指定类和接口 ID。

回到 `AddressBook` 类定义：第三次出现 `Q_CLASSINFO()` 看起来有些神秘。默认情况下，ActiveX 事件不仅控制它们的属性、信号和槽，还控制它们直到 `QWidget` 的祖先项。`ToSuperClass` 属性允许我们指定继承树中想要暴露的最高祖先。在这里，我们将组件的类名（AddressBook）指定为最高导出项，这意味着继承自 AddressBook 自身祖先的属性、信号和槽将不会被导出。

```
class ABItem : public QObject, public QTreeWidgetItem
{
    Q_OBJECT
    Q_PROPERTY(QString contact READ contact WRITE setContact)
    Q_PROPERTY(QString address READ address WRITE setAddress)
    Q_PROPERTY(QString phoneNumber READ phoneNumber WRITE setPhoneNumber)
    Q_CLASSINFO("ClassID", "{8bc2730e-5f39-4e5c-96be-461c2cd0d282")
    Q_CLASSINFO("InterfaceID", "c8bc1656-87e0-48a9-9937-fbe1ceff8b2e")


public:
    ABItem(QTreeWidgetItem* tree);

    void setContact(const QString &contact);
    QString contact() const { return text(0); }
    void setAddress(const QString &address);
    QString address() const { return text(1); }
    void setPhoneNumber(const QString &number);
    QString phoneNumber() const { return text(2); }

public slots:
    void remove();
};
```

`ABItem` 类代表地址录中的一个条目。它派生自 `QTreeWidgetItem` 以便显示。

```
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    if (!QAxFactory::isServer()) {
        AddressBook addressBook;
        addressBook.show();
    }
    return app.exec();
}
```

# 处理 X11 会话管理

我们在 X11 上注销时，某些窗口管理器会询问我们是否要保存会话。如果我们说“是”，运行中的应用程序将在下次登录时重启，并保持相同的布局，理想情况下保持与注销相同的状态。这种示例如图 23.7 所示。

# 图 23.7. 在 KDE 上注销

![](img/5a524abdf0b0d58fa99d30abb4463611_919_0.png)

负责保存和恢复会话的 X11 特定组件被称为会话管理器。为了让 Qt/X11 应用程序感知会话管理器，我们必须重新实现 `QApplication::saveState()` 并在保存应用程序的状态。

Microsoft Windows 和某些 Unix 系统提供了另一种名为休眠（hibernation）的机制。当用户将计算机进入休眠时，操作系统只需将计算机内存转到磁盘并在唤醒时重新加载。应用程序不需要做任何事情，甚至不需要感知到这种发生。

当用户启动关机时，我们可以在关机发生前通过重新实现 `QApplication::commitData()` 来获取控制。这允许我们保存任何未保存的数据并在并在时与用户交互。会话管理的这部分在 X11 和 Windows 上都受支持。

我们将通过查看图 23.8 所示的感知会话的井棋应用程序的代码探索会话管理。首先，让我们看看 `main()` 函数：

```
int main(int argc, char *argv[])
{
    Application app(argc, argv);
    TicTacToe toe;
    toe.setObjectName("toe");
}
```

