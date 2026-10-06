![](bbox=[0.015, 0.005, 0.403, 0.335])

The corners indicated with dotted lines can belong to either of their two adjoining dock areas. For example, we could make the top-left corner belong to the left dock area by calling QMainWindow::setCorner(Qt::TopLeftCorner, Qt::LeftDockWidgetArea).

The following code snippet shows how to wrap an existing widget (in this case, a QTreeView) in a QDockWidget and insert it into the right dock area:

```
QDockWidget *shapesDockWidget = new QDockWidget(tr("Shapes"));
shapesDockWidget->setObjectName("shapesDockWidget");
shapesDockWidget->setWidget(treeWidget);
shapesDockWidget->setAllowedAreas(Qt::LeftDockWidgetArea | Qt::RightDockWidgetArea);
addDockWidget(Qt::RightDockWidgetArea, shapesDockWidget);
```

The setAreas() specifies constraints on which dock areas can accept the dock window. Here, we only allow the user to drag the dock window into the left and right dock areas, where there is enough vertical space for it to be displayed sensibly. If no allowed areas are explicitly set, the user can drag the dock window to any of the four areas.

Every QObject can be given an "object name". This name can be useful when debugging and is used by some tools. Normally we do not bother to give widget object names, but when we create dock windows and toolbars, doing so is necessary if we want to use QMainWindow::saveState() and QMainWindow::restoreState() to save and restore the dock window and toolbar geometries and states.