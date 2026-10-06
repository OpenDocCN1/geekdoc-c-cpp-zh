# Making Applications Plugin-Aware

An application plugin is a dynamic library that implements one or more interfaces. An interface is a class that consists exclusively of pure virtual functions. The communication between the application and the plugins is done through the interface's virtual table. In this section, we will focus on how to use a plugin in a Qt application through its interfaces, and in the next section we will show how to implement a plugin.

To provide a concrete example, we will create the simple Text Art application shown in Figure 21.3. The text effects are provided by plugins; the application retrieves the list of text effects provided by each plugin and iterates over them to show each as an item in a QListWidget.

# Figure 21.3. The Text Art application

![](bbox=[0.0, 0.345, 0.595, 0.655])

The Text Art application defines one interface:

```
class TextArtInterface{
public:
    virtual ~TextArtInterface() { {}
    virtual QStringList effects() const = 0;
    virtual QPixmap applyEffect(const QString &effect, const QString &text, const QFont &font, const QSize &size, const QPen &pen, const QBrush &brush) = 0;
```