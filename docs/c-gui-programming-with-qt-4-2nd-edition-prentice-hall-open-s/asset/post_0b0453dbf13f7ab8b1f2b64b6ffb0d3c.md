
# Qtopia APIs

Qtopia Edition and Qtopia Phone Edition provide sets of applications that are relevant to mobile device users. Most of these applications have their functionality abstracted into libraries, or make use of edition-specific libraries. These libraries can be used in our own Qtopia applications, giving us access to device services such as alarms, email, phone dialing, SMS, voice recording, and many others.

If we want to access device-specific features from our applications, we have many options:

- We can use Qt/Embedded Linux and write our own code for interacting with the device.
- We can take an existing Qtopia application and modify it to have the functionality we want.
- We can write using the additional APIs, for example, the Qtopia Phone API or the Qtopia PIM (Personal Information Manager) application's library.

In this section, we will take the last of these approaches. We will write a simple application that records simple information about expenses. It makes use of the Qtopia PIM's data to pop up a list of contacts, and then sends an expense report to the selected contact as an SMS message. It also demonstrates how to use Qtopia's support for the multi-function "soft keys" found on most mobile phones.

As Figure 24.4 shows, the application will end up in the application packages list, like the example we built in the previous section. As before, we will begin by looking at the .pro file, then the .desktop file, and finally the application's source files. Here's expenses.pro:

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

## Figure 24.4. Locating and running the Expenses application

![](img/5a524abdf0b0d58fa99d30abb4463611_943_0.png)

The qtopia_project() line is the same as before. Since this application relies on the Qtopia PIM library, we use a depends() directive to specify the library. If we want to use multiple libraries, we can do so by separating them with commas. The rest of .pro file is similar to what we saw in the Unit Converter example, this time we have a few more source files because the application is more elaborate.

The expenses.desktop file is very similar to the one we saw before:

```
[Desktop Entry]
Comment[]=A program to record and SMS expenses
Exec=expenses/expenses
Icon=expenses/expenses
Type=Application
Name[]=Expenses
```

The same is true of main.cpp:

```cpp
#include <QtopiaApplication>
```

```cpp
#include "expensewindow.h"

QTOPIA_ADD_APPLICATION("Expenses", ExpenseWindow)
QTOPIA_MAIN
```

We will now look at the Expenses application's header files and those parts of the source files that are Qtopia-specific or particularly relevant, starting with the Expense class:

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

This simple class holds a date, a description, and an amount. We won't review the expense.cpp file since none of its code is Qtopia-specific and it is very simple.

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

The ExpenseWindow is the application's main form. It provides functions for the user to add, edit, and delete individual expense items, to send an SMS message with all of them, and to clear them. The expenses are held as values in a QList<Expense>.

The constructor creates a QListWidget and two QLabel. One label shows the text "Total", and the other sum of the expenses. The actions are created by createActions(), and the menu or toolbar is created by createMenuToolbar(). Both preexisting expenses are loaded at the end of the constructor by calling loadData(). We will skip the constructor itself, and instead just review the functions that it calls:

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

The createActions() function creates the Add, Edit, Delete, Send, and Clear actions. Although it is possible to use resource (.qrc) files, when processing Qtopia applications the standard practice for icons is to store them in a pics directory gets copied onto the device (thanks to the .pro INSTALLS line). They can then be shared among several applications, and Qtopia optimizes them

Everywhere Qt or Qtopia expects a file name, we can supply a Qtopia resource instead. These are identified by a leading colon in the file name, followed by a word specifying the kind of resource. In this case, we specify that we want icons and give a file name, for example: :icon/add, omitting the file extension. Qtopia will look for a suitable icon in a number of standard locations. See: doc.qt.com/qtopia-resource.html for the details.

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

Some phones have "soft keys", that are multi-function keys whose actions are context-specific. PDAs, we would normally have a toolbar rather than a popup menu. Users will expect to be able to close the application without being forced to explicitly save their data. They will also expect the data to be restored when they restart the application at a later time. This is easily taken care by calling loadData() in the constructor, and saving the data in closeEvent(). Qtopia offers many choices for data storage, including saving to SQLite database or saving to a file. Since the expense data is so small, we will be using QSettings. We will look at how it is saved, and then at how it is loaded.

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

If data exists from a previous session, we clear the existing data and then read each new expense item. The showData() function clears the list widget, then
