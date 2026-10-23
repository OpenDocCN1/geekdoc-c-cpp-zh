
```
qDebug() << "Transaction failed:" <<
db.lastError().text();
}
```

## 错误处理：

事务期间的正确错误处理至关重要。您应该在每次操作后检查错误并进行相应处理。

```
cpp
Copy code
QSqlQuery query;
if (!query.exec("UPDATE users SET age = age + 1")) {
    qDebug() << "Update failed:" << query.lastError().text();
    db.rollback(); // Rollback on error
}
```

## 数据类型与绑定值

在使用数据库时，理解数据类型的管理方式至关重要。Qt 提供了一种将不同类型的值绑定到 SQL 查询的方法。

### 支持的数据类型：

Qt 支持各种数据类型，包括整数、字符串、日期和二进制数据。在将值绑定到查询时，请确保为每个字段使用适当的类型。

```
cpp
Copy code
query.bindValue(":age", QVariant(30)); // Binding an integer
query.bindValue(":birthdate",
QVariant(QDate::currentDate())); // Binding a date
```

## QVariant 类：

QVariant 类允许您在单个变量中存储不同类型的值。它提供了一种方便的方式来处理绑定值时的各种数据类型。

```
cpp
Copy code

QVariant value = query.value("name");
if (value.isNull()) {
    qDebug() << "Name is null.";
} else {
    QString name = value.toString();
    qDebug() << "Name:" << name;
}
```

## 在用户界面中显示数据

在用户界面中显示从数据库检索到的数据是数据库驱动应用程序的一个关键方面。我们将讨论如何使用 Qt 部件有效地呈现数据。

### 使用 QTableView：

QTableView 是显示表格数据的绝佳部件。您可以使用 QSqlTableModel 或 QSqlQueryModel 来用数据库中的数据填充视图。

```
cpp
Copy code

QSqlTableModel *model = new QSqlTableModel(this, db);
model->setTable("users");
model->select(); // Load data
QTableView *tableView = new QTableView(this);
tableView->setModel(model);
tableView->resizeColumnsToContents(); // Resize columns to fit data
```

## 编辑数据：

借助模型/视图架构，用户可以直接在视图中编辑数据。您可以通过在模型上设置适当的标志来启用编辑。

```
cpp

Copy code

model->setEditStrategy(QSqlTableModel::OnFieldChange); // Save changes on field change
```

## 过滤与排序：

您可以在视图中实现过滤和排序功能，以提升用户体验。Qt 提供了在模型中设置过滤器和排序顺序的方法。

```
cpp

Copy code

model->setFilter("age > 25"); // Filter users older than 25
model->sort(1); // Sort by the second column (age)
```

## 自定义视图：

您可以通过设置标头、调整行高以及应用样式表来自定义 QTableView 的外观，以获得更好的视觉呈现。

```
cpp

Copy code

tableView->horizontalHeader()->setStretchLastSection(true); // Stretch last section
tableView->setAlternatingRowColors(true); // Enable alternating row colors
```

## 示例应用程序：数据库驱动的联系人管理器

为了说明本章讨论的概念，我们将创建一个简单的联系人管理器应用程序，允许用户添加、编辑和删除存储在 SQLite 数据库中的联系人。

### 设置应用程序：

创建一个带有 QTableView 的主窗口用于显示联系人，以及用于添加、编辑和删除条目的按钮。

```
cpp
Copy code
class ContactsManager : public QMainWindow {
    Q_OBJECT

public:
    ContactsManager(QWidget *parent = nullptr) :
QMainWindow(parent) {
        setupUI();
        setupDatabase();
    }

private:
    void setupUI() {
        tableView = new QTableView(this);
        setCentralWidget(tableView);

        QPushButton *addButton = new QPushButton("Add Contact", this);
        QPushButton *editButton = new QPushButton("Edit Contact", this);
        QPushButton *deleteButton = new
QPushButton("Delete Contact", this);

        QVBoxLayout *layout = new QVBoxLayout;
        layout->addWidget(addButton);
```

联系人，并使用本章前面讨论的技术。

```
cpp

Copy code

void ContactsManager::addContact() {
    // Open a dialog to get contact information and insert into database
}

void ContactsManager::editContact() {
    // Open a dialog to edit selected contact's information
}

void ContactsManager::deleteContact() {
    // Delete the selected contact from the database
}
```

### 测试应用程序：

编译并运行该应用程序。您应该能够添加、编辑和删除联系人，同时看到更改反映在 QTableView 中。

## 结论

在本章中，我们介绍了如何使用 Qt SQL 模块将数据库集成到 Qt 应用程序中。我们探讨了如何连接数据库、执行 SQL 查询、管理事务以及在用户界面中显示数据。掌握这些技能后，您可以创建功能强大的数据库驱动应用程序，利用 Qt 的功能来增强用户体验。在继续开发应用程序时，请考虑错误处理、用户反馈以及维护简洁直观的数据交互界面的重要性。

## 第 16 章：Qt 中的高级图形与自定义部件

在本章中，我们将深入探讨 Qt 的高级图形功能，并探索如何创建自定义部件。我们将介绍在部件上绘图、使用 Qt Graphics View 框架以及创建复杂自定义控件等概念。到本章结束时，您将掌握必要的技能，以丰富的图形和个性化用户界面来增强您的 Qt 应用程序。

### 理解绘图系统

Qt 的绘图系统允许开发人员在应用程序中高效地渲染图形。它提供了一套强大的工具，用于在部件上绘制形状、文本和图像。Qt 中的绘图过程通常涉及重写部件的 `paintEvent()` 方法。

### 设置自定义部件：

要创建自定义部件，您需要继承 `QWidget` 并实现 `paintEvent()` 方法。该方法就是您定义绘图逻辑的地方。

```
```cpp
class CustomWidget : public QWidget {
public:
    CustomWidget(QWidget *parent = nullptr) :
    QWidget(parent) {}

protected:
    void paintEvent(QPaintEvent *event) override {
        QPainter painter(this);
        painter.setPen(Qt::blue);
        painter.setBrush(Qt::green);
        painter.drawRect(10, 10, 100, 100);
```
```

```
}
};
```

## 使用 QPainter：

QPainter 类是用作渲染的核心类。它提供了绘制形状、文本和图像的方法。在执行绘图操作之前，您可以设置各种属性，例如画笔颜色、画刷样式和字体。

```
cpp
Copy code

void CustomWidget::paintEvent(QPaintEvent *event) {
    QPainter painter(this);
    painter.setPen(QPen(Qt::red, 2));
    painter.drawLine(0, 0, width(), height());
    painter.setFont(QFont("Arial", 16));
    painter.drawText(rect(), Qt::AlignCenter, "Hello, Qt!");
}
```

## 坐标系：

Qt 使用一个坐标系，其中 (0,0) 位于部件的左上角。x 坐标向右增加，y 坐标向下增加。
理解这个坐标系对于准确放置图形元素至关重要。

## Graphics View 框架

Qt Graphics View 框架旨在管理和交互大量二维图形项。它提供了一种场景图架构，使开发人员能够轻松创建复杂的图形应用程序。

### 创建场景：

场景是 QGraphicsScene 的一个实例，用于容纳图形项。您可以向场景中添加形状、图像和文本等项。

```
cpp
Copy code
QGraphicsScene *scene = new QGraphicsScene();
scene->setSceneRect(0, 0, 400, 300);
```

### 添加图元：

要向场景中添加图元，请创建 QGraphicsItem 或其子类（例如 QGraphicsRectItem、QGraphicsEllipseItem）的实例，并将它们添加到场景中。

```
cpp
Copy code
QGraphicsRectItem *rectItem = scene->addRect(10, 10, 100, 100, QPen(Qt::blue), QBrush(Qt::green));
QGraphicsEllipseItem *ellipseItem = scene->addEllipse(150, 10, 100, 100, QPen(Qt::red), QBrush(Qt::yellow));
```

### 显示场景：

要显示场景，请使用 QGraphicsView，它提供了一个用于可视化 QGraphicsScene 内容的部件。您可以通过缩放和滚动行为等设置属性。

```
cpp
Copy code
QGraphicsView *view = new QGraphicsView(scene);
view->setRenderHint(QPainter::Antialiasing);
view->show();
```

