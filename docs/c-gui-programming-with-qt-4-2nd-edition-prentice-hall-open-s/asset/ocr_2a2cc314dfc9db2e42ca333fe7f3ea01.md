When the user adds a new node, we create a new instance of the Node class, give it a default text, and then pass the node to setupNode() to position and select it. We use a separate function for adding a node because we will need this functionality when implementing each other. paste().

```
void DiagramWindow::setNode(Node *node)
{
    node->setPos(QPoint(80 + (100 (seqNum % 5)),
                    80 + (50 ((seqNum / 5) % 7))));
    scene->addItem(node);
    ++seqNum;

    scene->clearSelection();
    node->setSelected(true);
    bringToFront();

}
```

This function positions a newly added or pasted node in the scene. The use of the sequence number ensures that new nodes are added in different positions rather than on top of each other. We clear the current selection and select just the newly added node. bringToFront() ensures all that the new node is further forward than any other node.

```
void DiagramWindow::bringToFront()
{
    ++maxZ;
    setZValue(maxZ);
}
void DiagramWindow::sendToBack()
{
    --minZ;
    setZValue(minZ);
}
void DiagramWindow::setZValue(int z)
{
    Node *node = selectedNode();
    if (node)
        node->setZValue(z);
}
```

The bringToFront() slot increments the maxZ value, and then sets the currently