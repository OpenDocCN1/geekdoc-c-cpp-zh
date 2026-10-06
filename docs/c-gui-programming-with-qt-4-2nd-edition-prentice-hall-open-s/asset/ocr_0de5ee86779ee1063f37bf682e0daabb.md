```
setFocusPolicy(Qt::StrongFocus);
rubberBandIsShown = false;

zoomInButton = new QToolButton(this);
zoomInButton->setIcon(QIcon(":/images/zoomin.png"));
zoomInButton->adjustSize();
connect(zoomInButton, SIGNAL(clicked()), this, SLOT(zoomIn()));

zoomOutButton = new QToolButton(this);
zoomOutButton->setIcon(QIcon(":/images/zoomout.png"));
zoomOutButton->adjustSize();
connect(zoomOutButton, SIGNAL(clicked()), this, SLOT(zoomOut()));

setPaletteSettings(setPaletteSettings());
}
```

The setBackgroundRole() calls QWidget to use the "dark" component of the palette as for erasing the color It gives Qt a default color it can use to fill any newly revealed pixels when the widget is resized to a larger size, before paintEvent() even has the chance to paint the pixels. We also need to call setAutoFillBackground(true) to enable this mechanism. (By default, widgets inherit the background from their parent widget.)

The setSizePolicy() calls the widget's size policy to QSizePolicy::Expanding in both directions. This tells any layout manager that is responsible for the widget that the widget is especially willing to grow, but can also shrink. This setting is typical for widgets that can take up a lot of screen space. The default is QSizePolicy::Preferred in both directions, which means the widget prefers to be of its size hint, but it can be shrunk to its minimum size or expanded indefinitely if necessary.

The setFocusPolicy(Qt::StrongFocus) calls makes the widget accept focus by clicking or pressing Tab. When the Plotter has focus, it will receive events for key presses. The Plotter understands a few keys: + to zoom in; - to zoom out; and the arrow keys to scroll up, down, left, and right.

# Figure 5.9. Scrolling the Plotter widget