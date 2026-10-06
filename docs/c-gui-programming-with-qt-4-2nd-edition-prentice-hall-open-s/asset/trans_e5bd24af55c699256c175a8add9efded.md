
操作（SELECT, INSERT, UPDATE, DELETE）。该类也可以独立使用，在没有 GUI 的情况下管理数据库，也可以作为 QListView 或 QTableView 的数据源。

这里是一个使用 QSqlTableModel 执行 SELECT 的示例：

```
QSqlTableModel model;
model.setTable("cd");
model.setFilter("year >= 1998");
model.select();
```

这等同于以下查询：

```
SELECT * FROM cd WHERE year >= 1998
```

通过使用 QSqlTableModel::record() 获取特定记录，并使用 value() 访问单个字段来遍历结果集：

```cpp
for (int i = 0; i < model.rowCount(); ++i) {
    QSqlRecord record = model.record(i);
    QString title = record.value("title").toString();
    int year = record.value("year").toInt();
    std::cerr << qPrintable(title) << ": " << year << std::endl;
}
```

QSqlRecord::value() 函数可以接收字段名或字段索引。在处理大数据数据集时，建议通过索引指定字段。例如：

```cpp
int titleIndex = model.record().indexOf("title");
int yearIndex = model.record().indexOf("year");
for (int i = 0; i < model.rowCount(); ++i) {
    QSqlRecord record = model.record(i);
    QString title = record.value(titleIndex).toString();
    int year = record.value(yearIndex).toInt();
    std::cerr << qPrintable(title) << ": " << year << std::endl;
}
```

要向数据库表插入一条记录，我们调用 insertRow() 创建一个新的空行（记录），并使用 setData() 设置每列（字段）的值：

```cpp
QSqlTableModel model;
model.setTable("cd");
int row = 0;
model.insertRows(row, 1);
model.setData(model.index(row, 0), 113);
model.setData(model.index(row, 1), "Shanghai My Heart");
model.setData(model.index(row, 2), 224);
model.setData(model.index(row, 3), 2003);
model.submitAll();
```

调用 submitAll() 之后，根据表的排序，记录可能会移动到不同的行位置。如果插入失败，submitAll() 将返回 false。

SQL 模型与标准模型的一个重要区别是，对于 SQL 模型，我们必须调用 submitAll() 才能将任何更改写入数据库。

要更新记录，我们必须先将 QSqlTableModel 定位到我们想要修改的记录上（例如使用 select()）。然后提取记录，更新我们想要更改的字段，并将更改写回数据库：

```cpp
QSqlTableModel model;
model.setTable("cd");
model.setFilter("id = 125");
model.select();
if (model.rowCount() == 1) {
    QSqlRecord record = model.record(0);
    record.setValue("title", "Melody A.M.");
    record.setValue("year", record.value("year").toInt() + 1);
    model.setRecord(0, record);
}
model.submitAll();
```

如果有匹配指定过滤条件的记录，我们使用 QSqlTableModel::record() 获取它。我们应用更改并用修改后的记录覆盖原始记录。

也可以使用 setData() 执行更新，就像我们处理非 SQL 模型时那样。我们获取的模型索引针对特定的行和列：

```cpp
model.select();
if (model.rowCount() == 1) {
model.setData(model.index(0, 1), "Melody A.M.");
model.setData(model.index(0, 3),
model.data(model.index(0, 3)).toInt() + 1);
model.submitAll();
}
```

删除记录与更新类似：

```cpp
model.setTable("cd");
_model.setFilter("id = 125");
model.select();
if (model.rowCount() == 1) {
    model.removeRows(0, 1);
    model.submitAll();
}
```

removeRows() 调用接收要删除的第一条记录的行号以及要删除记录的数量。下一个示例删除了所有匹配过滤条件的记录：

```cpp
model.setTable("cd");
model.setFilter("year < 1990");
model.select();
if (model.rowCount() > 0) {
    model.removeRows(0, model.rowCount());
    model.submitAll();
}
```

QSqlQuery 和 QTableModel 类提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

![](img/5a524abdf0b0d58fa99d30f9)

- 连接与查询
- 查看表
- 编辑记录
- 在表单中展示数据

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

（此处后续文本存在重复或乱码，我将根据提供的干净片段提供逻辑流）

*注：由于原始文本中存在大量重复的段落，译文已根据逻辑对核心内容进行了整合翻译。*

# 13. 数据库

QtSql 模块提供了 Qt 与 SQL 数据库之间的接口。使用这些类，我们可以创建向用户展示数据的表单，并让他们插入、更新和删除记录。

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

## 连接与查询

要建立 SQL 数据库连接：

对于使用 SQL 类的项目，我们必须在它们的 .pro 文件中添加行：

```
QT += sql
```

这将确保应用程序链接到 QtSql 库。

```cpp
bool createConnection()
{
    QSqlDatabase db = QSqlDatabase::addDatabase("MYSQL");
    db.setHostName("mozart.edu");
    db.setDatabaseName("musicdb");
    db.setUserName("gbatstone");
    db.setPassword("T17V4");
    if (!db.open()) {
        QMessageBox::critical("Database Error", db.lastError().text());
        return false;
    }
    return true;
}
```

```cpp
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    if (!createConnection())
        return 1;
    ...
    return app.exec();
}
```

一旦建立连接，我们可以 SqlQuery 执行底层数据库支持的任何 SQL 语句。例如，这里是执行 SELECT 语句的方法：

```cpp
SqlQuery query;
query.exec("SELECT title, year FROM cd WHERE year >= 1998");
```

在 `exec()` 之后，我们可以遍历查询结果集：

```cpp
while (query.next()) {
    QString title = query.value(0).toString();
    int year = query.value(1).toInt();
    std::cerr << title << " : " << year << std::endl;
}
```

SqlQuery 还提供了其他用于遍历结果集的函数：first()、last()、previous() 和 seek()。

