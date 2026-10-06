
Now build the application, and run it. If you click Quit, or press Space (which presses the button), the application will terminate.

## Laying Out Widgets

In this section, we will create a small example application that demonstrates how to use layouts to manage the geometry of widgets in a window and how to use signals and slots to synchronize widgets. The application—shown in Figure 1.4—asks for the user's age, which the user can enter by manipulating either a spin box or a slider.

### Figure 1.4. The Age application

![](img/5a524abdf0b0d58fa99d30abb4463611_33_0.png)

The application consists of three widgets: a QSpinBox, a QSlider, and a QWidget. The QWidget is the application's main window. The QSpinBox and QSlider are rendered inside the QWidget; they are children of QWidget. Alternatively, we can say that the QWidget is the parent of the QSpinBox and QSlider. The QWidget has no parent itself because it is being used as a top-level window. The constructors for QWidget and all of its subclasses take a QWidget * parameter that specifies the parent widget.

Here's the source code:

Code View:

```
1 #include <Application>
2 #include <QBoxLayout>
3 #include <QSlider>
4 #include <QSpinBox>

5 int main(int argc, char *argv[])
6 {
7 QApplication app(argc, argv);

8 QWidget *window = new QWidget;
9 window->setWindowTitle("Enter Your Age");

10 QSpinBox *spinBox = new QSpinBox;
11 QSlider *slider = new QSlider(Qt::Horizontal);
12 spinBox->setRange(0, 130);
13 slider->setRange(0, 130);

14 QObject::connect(spinBox, SIGNAL(valueChanged(int)),
15 slider, SLOT(setValue(int)));
16 QObject::connect(slider, SIGNAL(valueChanged(int)),
17 spinBox, SLOT(setValue(int)));
18 spinBox->setValue(35);

19 QHBoxLayout *layout = new QHBoxLayout();
20 layout->addWidget(spinBox);
21 layout->addWidget(slider);
22 window->setLayout(layout);

23 window->show();

24 return app.exec();
25 }
```

Lines 8 and 9 set up the QWidget that will serve as the application's main window.
We call setTitle() to set the text displayed in the window's title bar.

Lines 10 and 11 create a QSpinBox and a QSlider, and lines 12 and 13 set their valid ranges. We can safely ensure that the user is at most 130 years old. We could pass window to QSpinBox and QSlider constructors, specifying that these widgets should have window as their parent, but it isn't necessary because the layout system will figure this out by itself and automatically set the parent of the spin box and the slider, as we will see shortly.

The two QObject::connect() calls in lines 14 to 17 ensure that the spin box and the slider are synchronized so that they always showed the same value. Whenever the value of one widget changes, its valueChanged(int) signal is emitted, and the setValue(int) slot of the other widget is called with the new value.

Line 18 sets the spin box value to 35. When this happens, the QSpinBox emits the valueChanged(int) with int argument of 35. This argument is passed to the QSlider's setValue(int) slot, which sets the slider value to 35. The slider emits the valueChanged(int) signal because its own value changed, triggering the spin box's setValue(int) slot. At this point, setValue(int) doesn't emit any signal, since the spin box value is already 35. This prevents infinite recursion. Figure 1.5 summarizes the situation.

### Figure 1.5. Changing one widget's value changes both

1. 0: setValue(35)
2. 35: valueChanged(35), setValue(35)
3. 35: valueChanged(35), setValue(35)
4. 35:

In lines 19 to 22, we lay out the spin box and slider widgets using a layout manager. A layout manager is an object that sets the size and position of the widgets that lie under its responsibility. Qt has three main layout manager classes:

- QHBoxLayout lays out widgets horizontally from left to right (right to left for some cultures).
- QVBoxLayout lays out widgets vertically from top to bottom.

![](img/5a524abdf0b0d58fa99d30abb4463611_35_0.png)

## Widget Styles

The screenshots we have seen so far have been taken on Linux, but Qt applications look native on every supported platform. Qt achieves this by emulating the platform's look and feel, rather than wrapping a particular platform or toolkit's widget set. Predefined styles

![](img/5a524abdf0b0d58fa99d30abb4463611_36_0.png)

The Plastique style is the default style for Qt/X11 applications running under KDE. Unlike the other styles, Windows XP, Vista, and Mac styles are available only on their platforms, as they rely on their native engines. To launch the application using the Motif style, simply use the following command-line option:

```
./age -style motif
```

The links in the "API Reference" section on the home page provide different ways of navigating Qt classes. The "All Classes" page lists every class in Qt's API. The "Main Classes" page lists only the most commonly used Qt classes. As an exercise, you might want to look up the classes and functions that we have used in this chapter.

- QGridLayout lays out widgets in a grid.

### Figure 1.7. The Age application's widgets and layout

![](img/5a524abdf0b0d58fa99d30abb4463611_37_0.png)

Even though we didn't set the position or size of any widget explicitly, the QSpinBox and Slider appear nicely laid out side by side. This is because QHBoxLayout automatically assigns reasonable positions and sizes to the widgets for which it is responsible, based on their needs. Layout managers free us from the chore of hard-coding screen positions in our applications and ensure that windows resize smoothly.

Qt's approach to building user interfaces is simple to understand and very flexible. The most common pattern that Qt programmers use is to instantiate the required widgets and then set their properties as necessary. Program add the widgets to layouts, which automatically take care of sizing and positioning. User interface behavior is managed by connecting widgets together using Qt's signals and slots.

## Using the Reference Documentation

Qt's reference documentation is an essential tool for Qt developer, since it covers every class and function in Qt. This book makes use of many classes and functions, but it does not cover all of them, nor does it provide detail of those mentioned. To get the most benefit from Qt, you should familiarize yourself with the Qt reference documentation as quickly as possible.

The documentation is available in HTML format in Qt's doc/html directory and can be read using any web browser. You can also use Qt Assistant, the Qt help browser, which has powerful searching and indexing features that make it quicker and easier to use than a web browser. To launch Qt Assistant, click Qt Trolltech v4.x.y Assistant in the Start menu on Windows, type assistant on the command line, or double-click Assistant on the Mac OS X Finder.

### Figure 1.8. Qt's documentation in Qt Assistant on Windows Vista

![](img/5a524abdf0b0d58fa99d30abb4463611_38_0.png)

Note that inherited functions are documented in the base class; for example, QPushButton has no show() function of its own, but it inherits one from QWidget.

Figure 1.9 shows how the classes we have seen so far relate to each other.
