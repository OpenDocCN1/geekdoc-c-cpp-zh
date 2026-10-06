```
view->setScene(scene);
view->setDragMode(QGraphicsView::RubberBandDrag);
view->setRenderHints(QPainter::Antialiasing| QPainter::TextAntialiasing);
view->setContextMenuPolicy(Qt::ActionsContextMenu);
setCentralWidget(view);
```

```
minZ = 0;
maxZ = 0;
seqNumber = 0;
```

```
createActions();
createMenus();
createToolBars();
```

```
connect(scene, SIGNAL(selectionChanged()),
this, SLOT(updateActions()));
```

```
setWindowTitle(tr("Diagram"));
updateActions();
```

We begin by creating a graphics scene, with an origin of (0, 0), a width of 600, and a height of 500. We then create a graphics view to visualize the scene. In the next example, instead of using QGraphicsView directly, we will subclass it to customize its behavior.

Selectable items can be selected by clicking them. To select more than one item at a time, the user can click the items while pressing Ctrl. Setting the drag mode to QGraphicsView::RubberBandDrag means that the user can also select items by dragging a rubber band over them.

the minZ and maxZ numbers are used by the sendToBack() and bringToFront() functions. The sequence number is used to give a unique initial text to each node the user adds.

The signal-slot connection ensures that when the scene's selection changes, we enable or disable the application's functions so that only actions that make sense are available. We call updateActions() to set the actions' initial enabled states.

```
void DiagramWindow::addNode() {
  Node *node = new Node;
  node->setText(tr("Node %1").arg(seqNumber + 1));
  setupNode(node);
}
```