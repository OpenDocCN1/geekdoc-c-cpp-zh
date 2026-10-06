If the user triggers this Properties action and a node is selected, invoke the Properties dialog. This allows us to change the node's text, position, and colors. Because PropertiesDialog operates directly on a Node pointer, we can simply execute it modally and let it take care of itself.

If a link is selected, we use Qt's built-in QDialog::getColor() static convenience function to pop up a color dialog. If the user chooses a color, we set that as the link's color.

If a node's properties or a link's color were changed, the changes are made through setter functions, and these call update() to ensure that the node or link is repainted with its new settings.

Users often want to cut, copy, and paste graphics items in this type of application, and one way to support this is to represent items textually, as we will see when we review the relevant content. We only handle nodes, because it would not make sense to copy or paste links, which only exist in relation to nodes.

```
void DiagramWindow::cut()
{
    Node *node = selectedNode();
    if (!node)
        return;

    copy();
    delete node;
}
```

The Cut action is a two-part process: Copy the selected item into the clipboard and delete the item. The copy is performed using the copy() slot associated with the Copy action, and the deletion uses C++'s standard delete operator, relying on any links that are connected to the node and remove the node from the scene.

```
void DiagramWindow::copy()
{
    Node *node = selectedNode();
    if (!node)
        return;

    QString str = QString("Node %1 %2 %3 %4")
        .arg(node->textColor().name())
        .arg(node->outlineColor().name())
        .arg(node->backgroundColor().name())
```