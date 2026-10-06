

## 通过脚本实现任务自动化

有时，我们使用 GUI 应用程序以相同的方式处理数据集。如果这些操作涉及调用许多菜单选项，或与对话框进行交互，这不仅会变得枯燥，而且在某些情况下可能会漏掉某些步骤，或者调换几个步骤的顺序——并且可能没有意识到发生了错误。让用户操作更方便的一种方法是允许他们编写脚本来自动执行一系列操作。

在本节中，我们使用 `-script` 命令，它允许用户指定要执行的脚本。该应用程序将启动、执行脚本并终止，期间完全不会出现 GUI。

我们将用于说明这种技术的应用程序称为 Gas Pump（加油泵）。它运行在由卡车司机加油站油泵记录的交易列表中，并以表格形式显示数据，如图 22.5 所示。

## 图 22.5. Gas Pump 应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_877_0.png)

每笔交易都按日期和时间、油泵编号、加油数量、卡车司机公司 ID 和用户 ID 以及交易状态进行记录。Gas Pump 应用程序可以以非常复杂的方式处理数据，如排序、过滤、计算总和以及在升和加仑之间转换。

Gas Pump 应用程序支持两种格式的交易数据：“Pump 2000”（扩展名为为 `.p20` 的纯文本格式）和“XML Gas Pump”（扩展名为为 `.gpx` 的 XML 格式）。该应用程序可以加载和保存这两种格式，因此只需加载一种格式并保存为另一种格式，即可在它们之间进行转换。

应用程序提供了四个标准脚本：

- `-onlyok.js` 删除所有状态不为 "OK" 的交易。
- `-p20togpx.js` 将 Pump 2000 文件转换为 XML Gas Pump 文件格式。
- `-tohtml.js` 生成 HTML 格式的报告。
- `-toliters.js` 将单位从加仑转换为升。

使用 `-script` 命令行选项，其后紧跟脚本脚本名以及要操作的文件名来调用脚本。例如：

`gaspump -script scripts/toliters.js data/2008q2.p20`

在这里，我们从 `scripts` 子目录运行 `toliters.js` 脚本，处理 `data` 子目录下的 `2008q2.p20` Pump 2000 数据文件。脚本将所有数量值从加仑转换为升，并进行修改。

Gas 应用程序的编写就像任何其他 C++/Qt 应用程序一样。事实上，它的代码与第 3 和第 4 章中的 Spreadsheet 示例非常相似。应用程序有一个 `QMainWindow` 子类 `PumpWindow`，它提供了应用程序的框架，包括其操作和菜单。（菜单如图 22.6 所示。）有一个自定义的 `QTableWidget` 类 `PumpSpreadsheet` 用于显示数据。有一个 `QDialog` 子类 `FilterDialog`（如图 22.7 所示），因为有很多过滤选项，这些选项存储在一个名为 `PumpFilter` 的类中，用户可以使用该类来指定他们的过滤选项。我们将简要回顾这些类，然后将如何为应用程序添加脚本支持。

代码视图：

```cpp
class PumpSpreadsheet : public QTableWidget
{
    Q_OBJECT
    Q_ENUMS(Format Column)
public:
    enum Format { Pump2000, GasPumpXml };
    enum Column { Date, Time, Pump, Company, User, Quantity, Status, ColumnCount };

    PumpSpreadsheet(QWidget *parent = 0);

slots:
    void clearData();
    void addData(const QString &fileName, FileFormat format);
    void saveData(const QString &fileName, FileFormat format);
    void sortByColumn(Column column, Qt::SortOrder order = Qt::AscendingOrder);
    void applyFilter(const PumpFilter &filter);
    void convertUnits(double factor);
    void computeTotals(Column column);
    void setText(int row, int column, const QString &text);
    QString text(int row, int column) const;

private:

}; // ...
```

## 图 22.6. Gas Pump 应用程序的菜单

![](img/5a524abdf0b0d58fa99d30abb4463611_879_0.png)

## 图 22.7. 过滤对话框

![](img/5a524abdf0b0d58fa99d30abb4463611_879_1.png)

`PumpSpreadsheet` 持有数据并提供了用户可以操作数据的函数（我们已将其制为槽）。这些槽可以通过用户界面访问，也可以用于脚本编写。`Q_ENUMS()` 宏用于生成关于 `FileFormat` 和 `Column` 枚举类型的元信息；我们稍后会回到这一点。

`QMainWindow` 子类 `PumpWindow` 有一个 `loadData()` 函数，它利用了一些 `PumpSpread` 槽。

```cpp
void PumpWindow::loadData() {
    QString fileName = QFileDialog::getOpenName(this,
        tr("Open Data File"), ".",
        fileFilters);
    if (!fileName.isEmpty()) {
        spreadsheet->clearData();
        spreadsheet->addData(fileName, fileFormat(fileName));
    }
}
```

