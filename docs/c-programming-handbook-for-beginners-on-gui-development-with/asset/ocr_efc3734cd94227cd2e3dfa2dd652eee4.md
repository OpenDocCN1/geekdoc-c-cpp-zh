# Creating a Scene:

A scene is an instance of QGraphicsScene that holds graphical items. You can add items such as shapes, images, and text to the scene.

```
cpp
Copy code
QGraphicsScene *scene = new QGraphicsScene();
scene->setSceneRect(0, 0, 400, 300);
```

# Adding Items:

To add items to the scene, create instances of QGraphicsItem or its subclasses (e.g., QGraphicsRectItem, QGraphicsEllipseItem) and add them to the scene.

```
cpp
Copy code
QGraphicsRectItem *rectItem = scene->addRect(10, 10, 100, 100, QPen(Qt::blue), QBrush(Qt::green));
QGraphicsEllipseItem *ellipseItem = scene->addEllipse(150, 10, 100, 100, QPen(Qt::red), QBrush(Qt::yellow));
```

# Displaying the Scene:

To display the scene, use a QGraphicsView, which provides a widget for visualizing the contents of a QGraphicsScene. You can set properties such as scaling and scrolling behavior.

```
cpp
Copy code
QGraphicsView *view = new QGraphicsView(scene);
view->setRenderHint(QPainter::Antialiasing);
view->show();
```