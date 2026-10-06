
QStyle 其实非常简单，只要我们已经开发了样式本身。我们都需要三个文件：一个与我们之前看到的完全不同的 .pro 文件，以及两个较小的 .h 和 .cpp 文件，用于提供一个 `QStylePlugin` 子类，该类作为样式的包装器。我们将从 .h 文件开始：

```
class BronzePlugin : public QStylePlugin
public:
    QStringList keys() const;
    QStyle *create(const QString &key);
};
```

所有插件至少提供一个 `keys()` 函数和一个 `create()` 函数。`keys()` 函数返回该插件可以创建的对象的列表。对于样式插件，键是不区分大小写的，因此 "mystyle" 和 "My" 被视为相同的。`create()` 函数根据键返回一个对象；该键必须与 `keys()` 返回的列表中的其中一个相同。

.cpp 文件几乎和 .h 文件一样小且简单。

```
QStringList BronzePlugin::keys() const
{
    return QStringList() << "Bronze";
}
```

`keys()` 函数返回插件提供的样式列表。在这里，我们只提供了一种名为 "Bronze" 的样式。

```cpp
QStyle *BronzePlugin::create(const QString &key)
{
    if (key.toLowerCase() == "bronze")
        return new BronzeStyle;
    return 0;
}
```

如果键是 "Bronze"（不区分大小写），我们就创建一个 `BronzeStyle` 对象并返回它。

在 .cpp 文件的末尾，我们必须添加以下宏来正确导出样式：

```
Q_EXPORT_PLUGIN2(bronzestyleplugin, BronzeStylePlugin)
```

`Q_EXPORT_PLUGIN2()` 的第一个参数是文本库的基名称，不包括任何扩展名、前缀或版本号。默认情况下，qmake 是目录中配置项的名称作为基名称；可以使用 .pro 文件中的 `TARGET` 来覆盖它。`Q_EXPORT_PLUGIN2()` 的第二个参数是插件的类名。

插件的 .pro 文件与应用程序不同，因此我们最后来看下 Bronze 样式的 .pro 文件：

```
TEMPLATE = lib
CONFIG += ../bronze/bronzestyle.h \
HEADERS = bronzestyleplugin.h
SOURCES = ../bronze/bronzestyle.cpp \
bronzestyleplugin.cpp
RESOURCES = ../bronze/bronzestyle.qrc
DESTDIR = $$[QT_INSTALL_PLUGINS]/styles
```

默认情况下，.pro 文件使用 app 模板，但在这里我们必须指定 lib 模板，因为插件是一个库，而不是一个独立的应用程序。`CONFIG` 行用于告诉 Qt 该库不仅仅是一个普通库，而是一个插件库。`DESTDIR` 指定插件应该存放的目录。所有插件必须进入 Qt 安装目录下的相应子目录；此路径是构建在 qmake 中的，并可以通过 `$$[QT_INSTALL_PLUGINS]` 变量获取。我们的插件提供新样式，我们将其放在 Qt 的 `plugins/styles` 目录。目录名称和插件名称的列表可以在 http://doc.troll.com/4.3/plugins-how.html 找到。

Qt 插件已经安装了，在 .pro 文件中指定使用哪一个是明智的——例如通过添加以下行：

```
CONFIG += release
```

一旦构建了 Bronze 样式插件，就可以使用了。应用程序可以通过在代码中指定来使用它。例如：

```
QApplication::setStyle("Bronze");
```

我们也可以在完全不更改应用程序源代码的情况下，通过带 `-style` 选项运行应用程序来使用样式。例如：
./spreadsheet -style bronze

运行 Qt Designer 时，它会自动查找插件。如果它找到了样式插件，它将提供在 `FormPreview` 菜单中预览样式的选项。

部署 Qt 插件的应用程序时，必须带有它们预定要使用的插件。Qt 插件必须放置在特定的子目录中（例如用于自定义样式的 `plugins/styles`）。Qt 应用程序会在其可执行文件所在目录的 `plugins` 目录中搜索插件。如果我们想在不同的目录中部署 Qt 插件，可以在启动时调用 `QCoreApplication::addLibraryPath()` 来扩展插件路径，或者在启动应用程序之前设置 `QT_PLUGIN_PATH` 环境变量。

现在我们已经看到了一个非常简单的插件，我们将处理一个更具挑战性的插件：用于 Windows 光标 (.cur) 文件的图像格式插件。（格式如图 21.2 所示。）Windows 光标文件可以包含多个不同尺寸的同一光标图像。一旦光标插件构建并安装，Qt 将能够读取 .cur 文件并访问单个光标（例如通过 `QImage`、`QReader` 或 `QMovie`），并且能够从 Qt 的任何其他图像格式（如 BMP、JPEG 和 PNG）写入光标。

# 图 21.2. .cur 文件格式

![](img/5a524abdf0b0d58fa99d30abb4463611_803_0.png)

新的图像格式插件包装器必须派自 `QImageIOPlugin` 并重新实现几个虚函数：

```
class CursorPlugin : public QImageIOPlugin
{
public:
    QStringList keys() const;
    Capabilities capabilities(QIODevice device,
const QByteArray &format) const;
    QIOHandler create(QIODevice *device,
const QByteArray &format) const;
};
```

`keys()` 函数返回支持的图像插件列表。`capabilities()` 函数的 `format` 参数返回该插件支持的功能。`create()` 函数根据设备和格式返回一个处理器。

```cpp
QStringList CursorPlugin::keys() const
{
    return QStringList() << "cur";
}
```

`keys()` 函数返回插件支持的图像格式列表。在这里，我们只提供了一种名为 "cur" 的格式。

```cpp
QImageIOPlugin::Capabilities CursorPlugin::capabilities(QIODevice *device,
const QByteArray &format) const
{
    if (format.toLowerCase() == "cur")
        return CanRead;
    return 0;
}
```

如果格式是 "cur"（不区分大小写），我们就创建一个 `CursorHandler` 对象并返回它。

```cpp
QIOHandler *CursorPlugin::create(QIODevice *device,
const QByteArray &format) const
{
    if (format.toLowerCase() == "cur")
        return new CursorHandler;
    return 0;
}
```

在 .cpp 文件的末尾，我们必须添加以下宏来正确导出插件：

```
Q_EXPORT_PLUGIN2(cursorplugin, CursorPlugin)
```
