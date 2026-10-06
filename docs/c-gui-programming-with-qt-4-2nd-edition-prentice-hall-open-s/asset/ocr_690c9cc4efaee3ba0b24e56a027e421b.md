Qt call ::setLayout() on line 22 installs the layout manager on the window. Behind the scenes, the QSpinBox and QSlider are "reparented" to be children of the widget on which the layout is installed, and for reason we don't need to specify an explicit parent when we construct a widget that will be put in a layout.

# Figure 1.7. The Age application's widgets and layout

![](bbox=[0.015, 0.173, 0.508, 0.253])

Even though we didn't set the position or size of any widget explicitly, the QSpinBox and QSlider appear nicely laid out side by side. This is because QHBoxLayout automatically assigns reasonable positions and sizes to the widgets for which it is responsible, based on their needs. The layout managers free us from the chore of hard-coding screen positions in our applications and ensure that windows resize smoothly.

Qt's approach to building user interfaces is simple to understand and very flexible. The most common pattern that Qt programmers use is to instantiate the required widgets and then set their properties as necessary. Program add the widgets to layouts, which automatically take care of sizing and positioning. User interface behavior is managed by connecting widgets together using Qt's signals and slots mechanism.