
![](img/5a24abdf0b0d58fa99d30abb4463611_313_1.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_2.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_3.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_4.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_5.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_6.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_7.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_8.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_9.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_10.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_11.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_12.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_13.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_14.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_15.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_16.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_17.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_18.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_19.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_20.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_21.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_22.png)

![](img/5a24abdf0b0d58fa99d30abb4463611_313_23.png)

## 基于 Graphics View 的渲染

使用 `QPainter` 绘制对于自定义小部件和绘制少量项目是理想的。对于需要处理从少数几个到数千个项目的图形，并且我们希望用户能够点击、拖拽和选择项目时，Qt 的图形视图类类提供了所需的解决方案。

图形架构由由 `QGraphicsScene` 类表示的场景（scene）以及场景中的项目（由 `QGraphicsItem` 子类表示）组成。场景（及其项目）通过由 `QGraphicsView` 类表示的视图（view）显示给用户。同一个场景可以在多个视图中显示——例如，显示大型场景的不同部分，或者在不同的变换下显示场景。图 8.14 示意性地说明了这一点。

### 图 8.14. 一个场景可以用于多个视图

![](img/5a524abdf0b0d58fa99d30abb4463611_314_0.png)

提供了几个预定义的 `QGraphicsItem` 子类，包括 `QGraphicsLineItem`、`QGraphicsPixmapItem`、`QGraphicsSimpleTextItem`（用于样式化纯文本）和 `QGraphicsTextItem`（用于富文本）；见图 8.15。我们也可以创建自定义的 `QGraphicsItem` 子类，正如我们在本节后面看到的的那样。

> [* Qt 4.4 预计支持将部件添加到图形场景中，就像图形项目一样，包括对它们应用变换的能力。

## 图 8.15. Qt 4.3 可用的图形视图项目

# 出售猫

它是灰色的，长发，留着小鼻子。

`GraphicsScene` 持有一组图形项目。场景有三层：背景层、项目层和前景层。背景和前景通常由 `QBrush` 指定，但也可以通过重新实现 `drawBackground()` 或 `drawForeground()` 来进行完全控制。如果我们想使用位图（pixmap）作为背景，可以简单地基于该位图创建一个 `QBrush`。前景画刷可以设置为半透明白色以产生淡化效果，或者设置为交叉线模式以提供网格覆盖。

场景可以告诉我们哪些项目发生了碰撞，哪些项目被选中，以及哪些项目位于特定点或特定区域。场景的图形项目要么是顶级的（场景是它们的父级），要么是子级的（它们的父级是另一个项目）。应用到项目的任何变换会自动应用到其子项目。

图形视图架构提供了两种分组项目的方法。一种是简单的让一个项目成为另一个项目的项目。另一种方法是使用 `QGraphicsItemGroup`。将项目添加到组中不会导致其发生任何变换；这些组方便于将多个项目像单个项目一样进行处理。

`GraphicsView` 是一个呈现场景的小部件，在需要时提供滚动条，并能够应用影响场景渲染的变换。这对于支持缩放和旋转等查看场景的功能非常有用。

默认情况下，`GraphicsView` 使用 Qt 内置的 2D 绘制引擎渲染，但在构造后可以通过 `viewport()` 更改为使用 OpenGL 小部件。打印场景或其部分也很容易，我们将在下一节中讨论，在那里看到使用 Qt 打印的几种技术。

该架构使用了三种不同的坐标系——视口坐标、场景坐标和项目坐标——并提供了它们之间映射的函数。视口坐标位于 `QGraphicsView` 内部。场景坐标用于在场景上定位顶级项目的逻辑坐标。项目坐标是每个项目特定的，并以项目本地的 (0, 0) 点为中心；当我们在场景上移动项目时，这些坐标保持不变。在实践中，我们通常关心场景坐标（用于定位顶级项目）和项目坐标（用于定位项目和绘制项目）。根据每个项目自身的本地坐标系绘制每个项目，意味着我们不需要担心项目在场景中的位置或对它应用了什么变换。

图形视图类易于使用并提供了丰富的功能。为了介绍使用它们可以做的一些工作，我们将回顾两个示例。第一个示例是一个简单的图表编辑器，它将展示如何创建项目以及如何处理用户交互。第二个示例是一个注释地图程序，它展示了如何处理大量的图形对象以及如何在不同的缩放级别高效地渲染它们。

图 8.16 所示的 `Diagram` 应用程序允许用户创建节点和链接。节点是在圆角矩形内显示纯文本的图形项目，而链接是连接对节点的线。被选中的节点将用比平时粗的画的虚线轮廓显示。我们将从链接开始，因为它们最简单，然后是节点，最后我们将看到它们是如何在上下文使用的。

### 图 8.16. Diagram 应用程序

[查看完整图像]

![](img/5a524abdf0b0d58fa99d30abb4463611_316_0.png)

```
class Link : public QGraphicsLineItem
```

```cpp
public:
    Link(Node fromNode, Node toNode);
    ~Link();

    Node fromNode() const;
    Node toNode() const;

    void setColor(const QColor &color);
    QColor color() const;

    void trackNodes();

private:
    Node myFromNode;
    Node myToNode;
```

`Link` 类派生自 `QGraphicsLineItem`，它表示 `QGraphicsScene` 中的一条线。线有三个主要属性：它连接的两个节点和用于绘制它的颜色。我们不需要一个 `Color` 成员变量来存储颜色，原因很快就会清楚。`QGraphicsItem` 不是 `Q` 子类，但如果我们想向 `Link` 中添加信号和槽，没有什么能阻止我们使用 `QObject` 进行多重继承。

`trackNodes()` 函数用于当用户将连接的节点拖到不同位置时，更新线的端点。

```cpp
Link::Link(Node fromNode, Node toNode)
{
    myFromNode = fromNode;
    myToNode = toNode;

    myFromNode->addLink(this);
    myToNode->addLink(this);

    setFlags(QGraphicsItem::ItemSelectable);
    setZValue(-1);

    setColor(Qt::darkRed);
    trackNodes();
}
```

当链接被构造时，它将自己添加到它连接的节点中。图形项目有几个标志，但在这种情况下我们只希望链接是可选的，这样用户就可以选择和。

```cpp
Link::~Link()
{
    myFromNode->removeLink(this);
    myToNode->removeLink(this);
}
```

当链接被销毁时，它从它连接的节点中移除自己。

```cpp
void Link::setColor(const QColor &color)
{
    setPen(QPen(color, 1.0));
}
```

当设置链接的颜色时，我们只需更改它的画笔，使用给定的颜色和为 1 的线宽。`setPen()` 函数继承自 `QGraphicsLineItem`。`color()` 直接返回画笔的颜色。

```cpp
void Link::trackNodes()
{
    setLine(QLineF(myFromNode->pos(), myToNode->pos()));
}
```

`QGraphicsItem::pos()` 函数返回图形项目相对于场景（对于顶级项目）或相对于父项目（对于子项目）的位置。

对于 `Link` 类，我们依赖它的基类来处理绘制：`QGraphicsItem` 在场景中的两个点之间画一条线。

对于 `Node` 类，我们将自己处理所有的图形。回顾 `Node` 声明时的另一个区别，将其分成几部分，因为它很长。我们将从

```cpp
class Node : public QGraphicsItem
{
    Q_DECLARE_FUNCTIONS(Node)
}
```

public:

    Node();

```

对于 `Node` 类，我们使用 `QGraphicsItem` 作为基类。`Q_DECLARE_FUNCTIONS()` 宏用于向此类添加一个 `tr()` 函数，即使它不是 `QObject` 子类。这仅仅是为了方便，允许我们使用 `tr()` 而不是静态的 `QObject::tr()` 或 `QCoreApplication::translate()`。

```cpp

void setText(const QString &text);

    QString text() const;

void setTextColor(const QColor &color);

    QColor text() const;

void setOutlineColor(const QColor &color);

    QColor outline() const;

void setBackgroundColor(const QColor &color);

    QColor background() const;

```

这些函数仅仅是私有成员的 getter 和 setter。我们提供了对文本颜色、节点轮廓和节点背景的控制。

```cpp

void addLink(Link link);

    void removeLink(Link link);

```

正如我们之前看到的，这些函数由 `Link` 类调用以从节点中添加或移除自己。

```cpp

QRectF boundingRect() const;

    QPainterPath shape() const;

void paint(const QStyleOptionGraphicsItem option, QWidget *widget);

```





在我们想要手动绘制的 `QGraphicsItem` 子类中，通常会重新实现 `boundingRect()` 和 `paint()`。如果我们没有重新实现 `shape()`，基类的实现将回退到使用 `boundingRect()`。在这种情况下，我们重新实现了 `shape()`，以返回一个更准确的形状，该形状考虑了节点的角。

图形架构使用边界矩形（bounding rectangle）来确定项目是否需要绘制。这使得 `QGraphicsView` 能够非常地显示任意大的场景，因为在任何时刻只有一部分项目是可见的。`shape` 用于判断一个点是否在项目内部，或者两个项目是否发生碰撞。

protected:

```

void mouseDoubleClickEvent(QGraphicsSceneMouseEvent *event);

QVariant itemChange(GraphicsItemChange change,

const QVariant &value);

```

在 Diagram 程序中，我们将提供一个属性对话框，用于编辑节点的位置、颜色和文本。作为额外的便利，我们将允许用户通过双击节点来更改文本。

如果节点被移动，我们会确保任何相关的链接都随之相应更新。我们重新实现了 `itemChange()` 处理程序来处理这件事；每当节点的属性（包括其位置）发生变化时，它就会被调用。我们之所以不为此目的使用 `mouseMouseEvent()`，是因为当节点通过程序代码移动时，该函数不会被调用。

private:

```

QRect outlineRect() const;

int roundness(double size) const;

QSet<Link *> myLinks;

QString myText;

QColor myTextColor;

QColor myBackgroundColor;

QColor myOutlineColor;

```

私有函数 `outlineRect()` 返回节点绘制的矩形，而 `roundness()` 则根据矩形的宽度或高度返回合适的圆角系数。

就像 `Link` 跟踪它连接的节点一样，`Node` 也会跟踪它的链接。当节点被删除时，与该节点相关的所有链接也会被删除。

我们现在准备好查看 Node 的实现，像照常一样从这里开始：

```

Node::Node()

{

    myTextColor = Qt::darkGreen;

    myOutlineColor = Qt::darkBlue;

    myBackgroundColor = Qt::white;

    setFlags(ItemIsMovable | ItemIsSelectable);

}

```

我们初始化了颜色，并使节点变为可移动和可选的。z 值将默认值为 0，我们将节点在场景中的位置留给调用者设置。

```

Node::~Node()

{

    foreach (Link *link, myLinks)

    delete link;

}

```

析构函数删除了节点的所有链接。每当一个链接被销毁时，它会从它连接的节点中移除自己。我们遍历链接集的（副本）而不是使用 `qDeleteAll()`，以避免产生副作用，因为链接集会间接被 `Link` 的析构函数访问。

```

void Node::setText(const QString &text)

{

    prepareGeometryChange();

    myText = text;

    update();

```

每当我们以影响其外观的方式更改图形项目时，我们必须调用 `update()` 来调度重绘。在像这样的项目边界矩形可能会变化的情况下（新文本可能比当前文本短或长），我们必须在执行任何影响项目边界矩形的操作之前，立即调用 `prepareGeometryChange()`。

我们将跳过 `text()`、`textColor()`、`outlineColor()` 和 `backgroundColor()` 器，因为它们仍然返回各自对应的私有成员。

```

void Node::setTextColor(const QColor &color)

{

    myTextColor = color;

    update();

}

```

当我们设置文本颜色时，我们必须调用 `update()` 来调度重绘，以便项目用新颜色进行绘制。我们不需要调用 `prepareGeometryChange()`，因为项目的大小不受颜色更改的影响。我们将省略轮廓和背景颜色的设置器，因为它们在结构上与这个设置器相同。

```

void Node::addLink(Link link)

{

    myLinks.insert(link);

}

```

```

void Node::removeLink(Link link)

{

    myLinks.remove(link);

}

```

在这里，我们简单地将给定的链接添加到或从节点的链接集中移除。

```cpp

QRectF Node::outlineRect() const

{

    const int Padding = 8;

    QFontMetricsF metrics = qApp->font();

    QRectF rect = metrics.boundingRect(myText);
