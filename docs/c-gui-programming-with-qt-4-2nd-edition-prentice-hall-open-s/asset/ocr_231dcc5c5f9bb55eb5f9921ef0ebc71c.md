# Subclassing QWidget

Many custom widgets are simply a combination of existing widgets, whether they are built-in Qt widgets or other custom widgets as HexSpinBox. Custom widgets that are built by composing existing widgets can usually be developed in Qt Designer:

+   * Create a new form using the "Widget" template.
* Add the necessary widgets to the form, and lay them out.
* Set up the signals and slots connections.
* If behavior beyond what can be achieved through signals and slots is required, write the necessary code in a class that is derived from both QWidget and the uic-generated class.

Naturally, combining existing widgets can also be done entirely in code. Whichever approach is taken, the resulting class is a QWidget subclass.

If the widget has no signals and slots of its own and doesn't implement any virtual functions, it is even possible to simply assemble the widget by combining existing widgets without a subclass. That's the approach we used in Chapter 1 to create the Age application, with a QWidget, QSpinBox, and a QSlider. Even so, we could just have subclassed QWidget and created the QSpinBox and QSlider in the subclass's constructor.

When one of Qt's widgets are suitable for the task at hand, and when there is no way to combine or adapt existing widgets to obtain the desired result, we can create the widget. This is achieved by subclassing QWidget and reimplementing a few event handlers to paint the widget and to respond to mouse clicks. This approach gives us complete freedom to define and control both the appearance and the behavior of our widget. Qt's built-in widgets, such as QLabel, QPushButton, and QText, are implemented this way. If they didn't exist in Qt, it would still be possible to create them ourselves using the public functions provided by QWidget in a completely platform-independent manner.

To demonstrate how to write a custom widget using this approach, we will create the IconEditor widget shown in Figure 5.2. The IconEditor is a widget that could be used in an icon editing program.

# Figure 5.2. The IconEditor widget