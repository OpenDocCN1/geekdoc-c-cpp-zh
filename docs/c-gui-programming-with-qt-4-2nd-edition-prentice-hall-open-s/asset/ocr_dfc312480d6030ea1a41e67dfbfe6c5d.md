We are now ready to look at Node's implementation, starting as usual with the

```
Node::Node()
{
    myTextColor = Qt::darkGreen;
    myOutlineColor = Qt::darkBlue;
    myBackgroundColor = Qt::white;

    setFlags(ItemIsMovable | ItemIsSelectable);
}
```

We initialize the colors, and make node items both movable and selectable. The z
value will default to 0, and we leave the node's position in the scene to be set by
the caller.

```
Node::~Node()
{
    foreach (Link *link, myLinks)
    delete link;
}
```

The destructor deletes all the node's links. Whenever a link is destroyed, it
removes itself from the nodes it is connected to. We iterate over (a copy) of the set
links rather than use qDeleteAll() to avoid side effects, since the set of links is
indirectly accessed by the Link destructor.

```
void Node::setText(const QString &text)
{
    prepareGeometryChange();
    myText = text;
    update();
```

Whenever we change a graphics item in a way that affects its appearance, we
must call update() to schedule a repaint. And in cases such as this where the item
bounding rectangle might change (the new text might be shorter
or longer than the current text), we must call prepareGeometryChange()
immediately before doing anything that will affect the item's bounding rectangle.

We will skip the text(), textColor(), outlineColor(), and backgroundColor()
getters since they still return their corresponding private member.