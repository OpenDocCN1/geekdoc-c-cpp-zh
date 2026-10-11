
Preferred（首选）和 Expanding（扩展）的方式是相同的。当同时包含 Preferred 和 Expanding 的表单被调整大时，额外的空间会分配给 Expanding 组件，而 Preferred 组件将保持其尺寸提示值（size hint）。

还有另外两种尺寸策略：MinimumExpanding（最小扩展）和 Ignored（忽略）。前者在 Qt 的某些版本中于少数情况下是必要的，但现在已经不再需要；推荐的方法是使用 Expanding 并重写 `minimumSizeHint()`。后者与 Expanding 类似，区别在于它忽略了组件的尺寸提示值和最小尺寸提示。

除了尺寸策略的水平和垂直分量外，`QSizePolicy` 类还存储了一个水平和一个垂直拉伸因子（stretch factor）。这些拉伸因子可以用于指示当表单扩展时，不同的子组件以不同的速率增长。例如，如果我们在 `QTextEdit` 上方有一个 `QTree`，并且希望 `QTextEdit` 的高度是 `QTree` 的两倍，我们可以将 `QTextEdit` 的垂直拉伸因子设置为 2，将 `QTree` 的垂直拉伸因子设置为 1。

影响布局的另一种方法是在子组件上设置最小尺寸、最大尺寸或固定尺寸。布局管理器在布局组件时会遵守这些约束。如果这还不够，我们始终可以派生子组件类并重写 `sizeHint()` 来获取所需的尺寸提示值。

## 堆叠布局 (StackedLayouts)

`QStackedLayout` 类布局一组子组件（或“页面”），一次只显示一个，向用户隐藏其他页面。`QStackedLayout` 本身是不可见的，没有为用户提供切换页面的内在方法。图 6.5 中的小箭头和灰色框架是由 Q Designer 提供的，以便于设计。为了方便起见，Qt 还包含了 `QStackedWidget`，它提供了一个内置了 `QStackedLayout` 的 `QWidget`。

### 图 6.5. QStackedLayout

![](img/5a524abdf0b0d58fa99d30abb4463611_241_0.png)

页面从 0 开始编号。要使特定的子组件可见，我们可以带页码调用 `setCurrentIndex()`。可以使用 `indexOf()` 获取子组件的页码。

图 6.6 显示的偏好对话框（Preferences）是一个使用 `QStackedLayout` 的示例。该对话框由左侧的 `QListWidget` 和右侧的 `QStackedLayout` 组成。`QListWidget` 中的每个项目对应于 `QStackedLayout` 中的不同页面。以下是对话框构造函数的相关代码：

```
PreferenceDialog::PreferenceDialog(QWidget *parent)
 : QDialog(parent)
{
  listWidget = new QListWidget;
  listWidget->addItem(tr("Appearance"));
  listWidget->addItem(tr("Web Browser"));
  listWidget->addItem(tr("Mail & News"));
  listWidget->addItem(tr("Advanced"));

  stackedLayout = new QStackedLayout;
  stackedLayout->addWidget(appearancePage);
  stackedLayout->addWidget(webPage);
  stackedLayout->addWidget(mailAndNewsPage);
  stackedLayout->addWidget(advancedPage);
  connect(listWidget, SIGNAL(currentRowChanged(int)),
         stackedLayout, SLOT(setCurrentIndex(int)));

  ... listWidget->setCurrentRow(0);
```

### 图 6.6. 偏好对话框的两个页面

[查看全尺寸图像]

![](img/5a524abdf0b0d58fa99d30abb4463611_242_0.png)

我们创建了一个 `QListWidget` 并填充了页面名称。然后我们创建了一个 `QStackedLayout` 并为每个页面调用 `addWidget()`。我们将列表组件的 `currentRowChanged(int)` 信号连接到堆叠布局的 `setCurrentIndex(int)` 槽，以实现页面切换，并在构造函数的结束处在列表组件上调用 `setCurrentRow()` 以从第 0 页开始。

使用 Qt Designer 也可以很容易创建此类表单：

1. template（模板）。
2. 向表单添加一个 `QListWidget` 和一个 `QStackedWidget`。
3. （要创建新页面，右键点击并选择“插入页面”；点击 `QStackedWidget` 右上角的微左或右箭头）。
4. 使用水平布局将组件并排排列。
5. 将列表组件的 `currentRowChanged(int)` 信号连接到堆叠组件的 `setCurrentIndex(int)` 槽。
6. 将列表组件的 `currentRow` 属性值设置为 0。

由于我们使用了预定义的信号和槽实现了页面切换，因此对话框在 Qt Designer 中预览时将表现出正确的行为。

对于页面较少且可能保持较少的情况，使用 `QStackedWidget` 和 `QListWidget` 的简单替代方案是使用 `QTabWidget`。

## 分割器 (Splitters)

`QSplitter` 是一个包含其他组件的组件。分割器中的组件通过分割器手柄隔开。用户可以通过拖动手柄来更改子组件的大小。分割器通常可以作为布局管理器的替代方案，以给用户更多的控制权。

`QSplitter` 的子组件按照它们创建的顺序自动并排（上下）排列，相邻组件之间有分割条。创建图 6.7 所示窗口的代码如下：

```
int main(int argc, char argv[]){
QApplication app(argc, argv);

QTextEdit editor1 = new QTextEdit;
QTextEdit editor2 = new QTextEdit;
QTextEdit editor3 = new QTextEdit;

QSplitter splitter(Qt::Horizontal);
splitter.addWidget(editor1);
splitter.addWidget(editor2);
splitter.addWidget(editor3);
...
splitter.show();
return app.exec();
}
```

### 图 6.7. 分割器应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_244_0.png)

该示例由 `QSplitter` 组件水平布局的三个 `QTextEdit` 组成——如图 6.8 所示。与仅布局表单子组件且没有视觉表示的布局管理器不同，`QSplitter` 派生自 `QWidget` 并可以像其他组件一样使用。

### 图 6.8. 分割器的组件

可以通过嵌套水平和垂直分割器来实现复杂的布局。例如，图 6.9 所示的邮件客户端包含一个水平分割器，其右侧包含一个垂直分割器。布局如图6.10 所示。

### 图 6.9. 邮件客户端

[查看全尺寸图像]

![](img/5a524abdf0b0d58fa99d30abb4463611_245_0.png)

## 图 6.10. 邮件客户端布局

![](img/5a524abdf0b0d58fa99d30abb4463611_245_1.png)

以下是邮件客户端应用程序构造函数中的代码

## MailClient::MailClient()

```
{
    rightSplitter = new QSplitter(Qt::Vertical);
    rightSplitter->addWidget(messagesTreeWidget);
    rightSplitter->addWidget(editText);
    rightSplitter->setStretchFactor(1, 1);

    mainSplitter = new QSplitter(Qt::Horizontal);
    mainSplitter->addWidget(foldersTreeWidget);
    mainSplitter->addWidget(rightSplitter);
    mainSplitter->setStretchFactor(1, 1);
    setCentralWidget(mainSplitter);

    setWindowTitle(tr("Mail Client"));
    readSettings();
}
```

`writeSettings()` 函数保存邮件客户端的设置：

```cpp
void MailClient::writeSettings() {
    QSettings settings("Software Inc.", "Mail Client");
    settings.beginGroup("mainWindow");
    settings.setValue("geometry", saveGeometry());
    settings.setValue("mainSplitter", mainSplitter->saveState());
    settings.setValue("rightSplitter", rightSplitter->saveState());
    settings.endGroup();
}
```

这是对应的 `readSettings()` 函数：

```cpp
void MailClient::readSettings() {
    QSettings settings("Software Inc.", "Mail Client");
    settings.beginGroup("mainWindow");
    restoreGeometry(settings.value("geometry").toByteArray());
    mainSplitter->restoreState(settings.value("mainSplitter").toByteArray());
    rightSplitter->restoreState(settings.value("rightSplitter").toByteArray());
    settings.endGroup();
}
```

Qt Designer 完全支持 QSplitter。要将控件放入拆分器中，只需将子控件放置在大致所需的位置，选择它们，然后点击“表单|在拆分器中水平布局”或“表单|在拆分器中垂直布局”。

## 滚动区域

`QScrollArea` 类提供了一个可滚动的视口和两个滚动条。如果我们想为控件添加滚动条，使用 `QScrollArea` 比我们自己实例化 `QScrollBar` 并手动实现滚动功能要简单得多。

使用 `QScrollArea` 的方法是调用 `setWidget()` 并传入我们想要添加滚动条的控件。如果该控件尚是，`QScrollArea` 会自动将其重新父化为视口（通过 `QScrollArea::viewport()` 访问）的子。例如，如果我们像第 5 节图 6.11 所示对 `IconEditor` 控件进行滚动，可以这样写：

```cpp
int main(int argc, char argv[])
{
  QApplication app(argc, argv);
  IconEditor iconEditor = new IconEditor;
  iconEditor->setIconImage(QImage(":images/mouse.png"));

  QScrollArea scrollArea;
  scrollArea.setWidget(iconEditor);
  scrollArea.viewport()->setBackgroundRole(QPalette::Dark);
  scrollArea.viewport()->setAutoFillBackground(true);
  scrollArea.setWindowTitle(QObject::tr("Icon Editor"));

  scrollArea.show();
  return app.exec();
}
```

### 图 6.11. 调整 QScrollArea 的大小

![](img/5a524abdf0b0d58fa99d30abb4463611_248_0.png)

`QScrollArea`（图 6.12 示意所示）按当前大小显示控件，或者在控件未调整大小时使用其尺寸。通过设置 `setWidgetResizable(true)`，我们可以告诉 `QScrollArea` 自动调整控件的大小，以利用其尺寸提示之外的额外空间。

## 图 6.12. QScrollArea 的组成控件

![](img/5a524abdf0b0d58fa99d30abb4463611_249_0.png)

默认情况下，只有当视口小于子控件时才会显示滚动条。我们可以通过设置滚动条策略强制始终显示滚动条：

```cpp
scrollArea.setHorizontalScrollBarPolicy(Qt::ScrollBarAlwaysOn);
scrollArea.setVerticalScrollBarPolicy(Qt::ScrollBarAlwaysOn);
```

`QScrollArea` 继承了 `QAbstractScrollArea` 的大部分功能。如 `QTextEdit` 和 `QAbstractItemView`（Qt 类的基类）派自 `QAbstractScrollArea`，因此我们不需要将它们封装在 `QScrollArea` 中即可获得滚动条。

停靠窗口（Dock windows）是可以停靠在 `QMainWindow` 内部或作为独立窗口浮动的窗口。`QMainWindow` 提供了四个停靠区域：中心控件上方、下方、左侧和右侧。像 Microsoft Visual Studio 和 Qt Linguist 等应用程序大量使用停靠窗口来提供非常灵活的用户界面。在 Qt 中，停靠窗口是 `QDockWidget` 的实例。图 6.13 显示了一个带有工具栏和停靠窗口的 Qt 应用程序。

## 图 6.13. 带有停靠窗口的 QMainWindow

![](img/5a524abdf0b0d58fa99d30abb4463611_250_0.png)

每个停靠窗口都有自己的标题栏，即使在停靠时也是如此。用户可以通过拖动标题栏将停靠窗口从一个区域移动到另一个区域。他们还可以通过将停靠窗口拖到任何区域之外，将其从区域中分离并使其作为独立窗口浮动。浮动的停靠窗口始终“在”主窗口之上。用户可以通过点击窗口标题栏中的关闭按钮来关闭 `QDockWidget`。这些功能的任何组合都可以通过调用 `QDockWidget::setFeatures()` 来禁用。

在 Qt 的早期版本中，工具栏被视为类似停靠窗口并共享相同的停靠区域。从 Qt 4 开始，工具栏占据中心控件周围的区域（如图 6.14 所示）且不能被停靠。如果需要浮动工具栏，我们可以简单地将其放入 `QDockWidget` 中。

## 图 6.14. QMainWindow 的停靠区域和工具栏区域

![](img/5a524abdf0b0d58fa99d30abb4463611_251_0.png)

该应用程序由 `MainWindow` 和 `Editor` 两个类组成。代码随书中示例提供，由于大部分代码与第一部分中的电子表格应用程序相同或相似，我们将只展示与 MDI 相关的代码。

让我们从 `MainWindow` 开始。

```cpp
MainWindow::MainWindow()
{
    mdiArea = new QMdiArea();
    setCentralWidget(mdiArea);
    connect(mdiArea, SIGNAL(subWindowActivated(QMdiSubWindow*)),
           this, SLOT(updateActions()));

    createActions();
    createMenus();
    createToolBars();
    createStatusBar();

    setWindowIcon(QPixmap(":images/icon.png"));
    setWindowTitle(tr("MDI Editor"));
    QTimer::singleShot(0, SLOT(loadFiles()));
}
```

在 `MainWindow` 构造函数中，我们创建了一个 `QMdiArea` 小部件并将其设置为中心部件。我们将 `QMdiArea` 的 `subWindowActivated()` 信号连接到我们将用于创建窗口菜单更新的槽函数，并确保这些操作根据应用程序的状态被启用或禁用。

在构造函数的末尾，我们设置了一个间隔为 0 毫秒的单次计时器来调用 `loadFiles()` 函数。这种计时器会在事件循环空闲时立即超时。在实践中，这意味着构造函数将完成，并在主窗口显示后将调用 `loadFiles()`。如果我们这样做，并且有很多大文件需要加载，构造函数将等到所有文件加载完毕才能完成，在此期间用户在屏幕上看不到任何内容，可能会认为应用程序启动失败。
