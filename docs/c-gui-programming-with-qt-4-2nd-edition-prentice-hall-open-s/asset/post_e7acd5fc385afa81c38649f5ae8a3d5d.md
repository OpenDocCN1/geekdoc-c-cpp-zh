
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

The populateListWidget() function begins by creating some variables to pass to the applyEffect() function, in particular a font, a pen, and a linear gradient. For it iterates over every TextArtInterface that was found by loadPlugins(). For each effect provided by each interface, a new QTreeWidgetItem is created with its text set to the name of the interface, and with a QPixmap created using applyEffect().

In this section, we have seen how to load plugins by calling loadPlugins() in the constructor, and how to use of them in populateListWidget(). The code copes gracefully whether there are no plugins providing TextArtInterfaces or one, or more. Furthermore, additional plugins could be added later: Every time the application starts up, it loads whatever plugins it finds that provide the interfaces it wants. This makes it easy to extend the application's functionality without changing the application itself.

# Writing Application Plugins

An application plugin is a subclass of QObject and of the interfaces it wants to provide. The examples that accompany this book includes two plugins for the Text Art application presented in the preceding section, to show that the application correctly handles multiple plugins.

Here, we will review the code for only one of them, the Basic Effects plugin. We will assume that the plugin's source code is located in a directory called basiceffectsplugin and that the Text Art application is located in a parallel directory called textart. Here's the declaration of the plugin class:

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

The plugin implements only one interface, TextArtInterface. In addition to Q_OBJECT, we must use the Q_INTERFACES() macro for each interface that is subclassed to ensure smooth cooperation between moc and qobject_cast<T>).

```cpp
QStringList BasicEffectsPlugin::effects() const{
  return QStringList() << "Plain" << "Outline" << "Shadow";
}
```

The effects() function returns a list of text effects supported by the plugin. This plugin supports three effects, so we just return a list containing the name of each one.

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

We want to ensure that the given text will fit in the specified size, if possible. For this reason, we use the font's metrics to see whether the text is too large to fit, and if it is, we enter a loop where we reduce the point size until we find a size that will fit, or until we reach 9 points, our fixed minimum size.

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

We create a pixmap of the required size and a painter to paint onto the pixmap. We also set some render hints for the smoothest possible results. The call to eraseRect() clears the pixmap with the background color.

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

For the "Plain" effect, no outline is required. For the "Outline" effect, we ignore the original pen and create our own black pen with a 2.5-pixel width. For the "Shadow" effect, we need to draw the shadow first so that the text can be painted on top of it.

```cpp
QPainterPath path;
path.addText((size.width() - metrics.width(text)) / 2,
              size.height()) - metrics.descent(), myFont, text);
    painter.drawPath(path);

    return pixmap;
}
```

We now have the pen and brushes set appropriately for each text effect, and in the "Shadow" effect case we have drawn the shadow. We are now ready to render the text. The text is horizontally centered and drawn far enough above the bottom of the pixmap to allow room for descenders.

```cpp
Q_EXPORT_PLUGIN2(basiceffectplugin, BasicEffectsPlugin)
```

At the end of the .cpp file, we use the Q_EXPORT_PLUGIN2() macro to make the plugin available to Qt.

The .pro file is similar to the one we used for the Bronze style plugin earlier in this chapter (p. 493):

```
TEMPLATE = lib
CONFIG += plugin
HEADERS = ../textart/textartinterface.h \
    basiceffectsplugin.h
SOURCES = basiceffectsplugin.cpp
DESTDIR = ../textart/plugins
```

If this chapter has whetted your appetite for application plugins, you might like to study the more advanced Plug & Paint example provided with Qt. The application supports three different interfaces and includes a useful Plugin Information dialog that lists the plugins and interfaces that are available to the application.

# 2. Application Scripting

![](img/5a524abdf0b0d58fa99d30abb4463611_834_0.png)

- Overview of the ECMAScript Language
- Extending Qt Applications with Scripts
- Implementing GUI Extensions Using Scripts
- Automating Tasks through Scripting

Scripts are programs written in an interpreted language that extend the facilities of an existing system. Some scripts are run as stand-alone applications, whereas others execute embedded in applications. Starting with version 4.3, Qt includes QtScript, a module that can be used to make Qt applications scriptable using ECMAScript, the standardized version of JavaScript. This module is a complete rewrite of the earlier Trollicht product Qt for Applications (QSA) and provides full support for ECMAScript Edition 3.

ECMAScript is the official name of the language standardized by Ecma International. It forms the basis of JavaScript (Mozilla), JScript (Microsoft), and ActionScript (Adobe). Although the language's syntax is superficially similar to C++ and Java, the underlying concepts are radically different and set it apart from many other object-oriented programming languages. In the first section of this chapter, we will quickly review the ECMAScript language and show how to run ECMAScript code using Qt. If you already know JavaScript or any other ECMAScript-based language, you can just skip this section.

In the second section, we will see how to add scripting support to a Qt application. This makes it possible for users to add their own functionality in addition to what the application already provides. This approach is also frequently used to make it easier to support users; technical staff can supply bug fixes and workarounds in the form of scripts.

In the third section, we will show how to develop GUI front-ends by combining ECMAScript code and forms created using Qt Designer. This technique is appealing to developers who dislike the "compile, link, run" cycle associated with C++ and prefer the scripting approach. It also enables users with JavaScript experience to design fully functional GUI interfaces without having to learn C++.
