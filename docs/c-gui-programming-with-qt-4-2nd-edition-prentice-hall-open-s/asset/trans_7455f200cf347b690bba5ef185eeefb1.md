
```cpp
gradient.setColorAt(0, QColor("darkolivegreen"));
gradient.setColorAt(0.8, QColor("darkgreen"));
gradient.setColorAt(1.0, QColor("lightgreen"));
foreach (TextArtInterface interface, interfaces) {
  foreach (QString effect, interface->effects()) {
    QWidgetItem item = new QWidgetItem(effect,
        listWidget);
    QPixmap pixmap = interface->applyEffect(effect, text, iconSize, pen,
        gradient);
    item->setData(Qt::DecorationRole, pixmap);
  }
}
listWidget->setCurrentRow(0);
```

`populateListWidget()` 函数首先创建一些变量并传递给 `applyEffect()` 函数，特别是字体、画笔和线性渐变。随后，它遍历由 `loadPlugins()` 找到的每一个 `TextArtInterface`。对于每个接口提供的每个效果，它都会创建一个新的 `QTreeWidgetItem`，将其文本设置为接口名称，并使用 `applyEffect()` 创建一个 `QPixmap`。

在本节中，我们已经学习了如何在构造函数中通过调用 `loadPlugins()` 来加载插件，以及如何在 `populateListWidget()` 中使用它们。无论是没有提供 `TextArtInterfaces` 的插件、只有一个插件还是多个插件，代码都能良好地运行。此外，以后还可以添加额外的插件：每当应用程序启动时，它都会加载找到的任何提供所需接口的插件。这使得在不更改应用程序本身的情况下扩展应用程序的功能变得简单。

# 编写应用程序插件

应用程序插件是 `QObject` 以及它想要提供的接口的子类。本书附带的示例包含了用于前一节介绍的 Text Art 程序的两个插件，以展示应用程序如何正确处理多个插件。

在这里，我们将仅回顾其中一个插件——即基础效果（Basic Effects）插件的代码。我们假设插件的源代码位于名为 `basiceffectsplugin` 的目录，而 Text Art 应用程序位于并行的 `textart` 目录中。以下是插件类的声明：

```cpp
class BasicEffectsPlugin : public QObject, public TextArtInterface{
  Q_OBJECT
  Q_INTERFACES(TextArtInterface)
```

```cpp
public:
QStringList effects() const;
QPixmap applyEffect(const QString &effect, const QString &text,
const QFont &font, const QSize &size,
const QPen &pen, const QBrush &brush);
};
```

该插件仅实现了一个接口，`TextArtInterface`。除了 `Q_OBJECT` 之外，我们必须对每个子类接口使用 `Q_INTERFACES()` 宏，以确保 moc 和 `qobject_cast<T>` 之间的顺畅协作。

```cpp
QStringList BasicEffectsPlugin::effects() const{
  return QStringList() << "Plain" << "Outline" << "Shadow";
}
```

`effects()` 函数返回插件支持的效果列表。该插件支持三个效果，因此我们只需返回一个包含每个效果名称的列表。

```cpp
QPixmap BasicEffectsPlugin::applyEffect(const QString &effect,
const QString &text, const QFont &font, const QSize &size,
const QPen &pen, const QBrush &brush){
  QFont myFont = font;
```

```cpp
QFontMetrics metrics(myFont);
while ((metrics.width() > size.width())
|| metrics.height() > size.height())
&& myFont.pointSize() > 9) {
  myFont.setPointSize(myFont.pointSize() - 1);
  metrics = QFontMetrics(myFont);
}
```

我们希望确保在可能的情况下，给定文本能够适应指定的尺寸。因此，我们使用字体度量（metrics）检查文本是否过大无法容纳，如果是，我们将进入一个循环，减小字号，直到找到适合的尺寸，或者达到我们固定的最小尺寸 9 。

```cpp
QPixmap pixmap(size);

QPainter painter(&pixmap);
painter.setFont(myFont);
painter.setPen(pen);
painter.setBrush(brush);
painter.setRenderHint(QPainter::Antialiasing, true);
painter.setRenderHint(QPainter::TextAntialiasing, true);
painter.setRenderHint(QPainter::SmoothPixmapTransform, true);
painter.eraseRect(pixmap.rect());
```

我们创建了一个所需大小的 pixmap 和一个用于在 pixmap 上绘图的 painter。我们还设置了一些渲染提示以获得尽可能平滑的结果。调用 `eraseRect()` 会用背景色清除 pixmap。

```cpp
if (effect == "Plain") {
  painter.setPen(Qt::NoPen);
} else if (effect == "Outline") {
  QPen pen(Qt::black);
  pen.setWidthF(2.5);
  painter.setPen(pen);
} else if (effect == "Shadow") {
  QPainter path(Qt::darkGray);
  painter.setBrush(brush);
  path.addText((size.width() - metrics.width(text)) / 2 + 3,
  (size.height() - metrics.descent()) + 3, myFont,
  text);
  painter.drawPath(path);
  painter.setBrush(brush);
}
```

对于“Plain”效果，不需要轮廓。对于“Outline”效果，我们忽略原始画笔，并创建了一个宽度为 2.5 像素的自定义黑色画笔。对于“Shadow”效果，我们需要先画阴影，这样文本就可以画在上面。

```cpp
QPainterPath path;
path.addText((size.width() - metrics.width(text)) / 2,
              size.height()) - metrics.descent(), myFont, text);
    painter.drawPath(path);

    return pixmap;
}
```

现在我们已经为每个文本效果正确设置了画笔和画刷，在“Shadow”效果情况下我们已经画好了阴影。我们现在准备好渲染文本了。文本水平居中，并且绘制在距离 pixmap 底部足够的位置，为下降字母（descenders）留出空间。

```cpp
Q_EXPORT_PLUGIN2(basiceffectplugin, BasicEffectsPlugin)
```

在 .cpp 文件的末尾，我们使用 `Q_EXPORT_PLUGIN2()` 宏让插件对 Qt 可用。

.pro 文件与我们在本章之前用于青铜风格插件的使用的类似（第 493 页）：

```
TEMPLATE = lib
CONFIG += plugin
HEADERS = ../textart/textartinterface.h \
    basiceffectsplugin.h
SOURCES = basiceffectsplugin.cpp
DESTDIR = ../textart/plugins
```

如果本节激发了你对应用程序插件的兴趣，你可能会喜欢提供的 Plug & Paint 示例。该应用程序支持三种不同的接口，并包含一个列出可用插件和接口的有用插件对话框。

# 2 应用程序脚本

![](img/5a24abdf0b0d58fa99d30abb4463611_834_0.png)

 语言概述
- 使用脚本扩展 Qt
- 使用脚本实现 GUI

脚本是用解释型语言编写的程序，用于扩展现有系统的功能。某些脚本作为独立程序运行，而另一些则嵌入应用程序中执行。从 4.3 版本开始，Qt 包含了 QtScript 模块，它可以使用 ECMAScript（JavaScript 的标准化版本）来使 Qt 应用程序可脚本化。

在本章的第一节中，我们将快速回顾 ECMAScript 语言，并展示如何使用 Qt 运行 ECMAScript 代码。如果你已经熟悉 JavaScript 或任何其他基于 ECMAScript 的语言，可以直接跳过本节。

在第二节中，我们将介绍如何为 Qt 应用程序添加脚本支持。这使得用户能够在应用程序现有功能之外添加自己的功能。这种方法也经常用于便于支持用户；技术人员可以以脚本的形式提供错误修复和解决方案。

在第三节中，我们将展示如何通过结合 ECMAScript 代码和使用 Qt Designer 创建的表单来开发 GUI 前端。这种技术对于不喜欢 C++ 相关的“编译、链接、运行”循环的开发者来说非常有吸引力。它还让具有 JavaScript 经验的用户无需学习 C++ 就能设计功能完整的 GUI 界面。

