# 4. Use a splitter.

Another way of using multiple widgets together is to use a QSplitter. QSplitter arranges its child widgets horizontally or vertically, with splitter handles giving some sizing control to the user. Splitters can contain all kinds of widgets, including other splitters.

# 5. Use an MDI area.

If the application uses MDI, the central area is occupied by a QMdiArea, and each MDI window is a child of that widget.

Layouts, splitters, and MDI areas can be combined with standard Qt widgets or with custom widgets. Chapter 6 covers these classes in depth.

For the Spreadsheet application, a QTableWidget subclass is used as the central widget. The QWidget class already provides most of the spreadsheet capability we need, but it doesn't support clipboard operations and doesn't understand spreadsheet formulas such as "=A1+A2+A3". We will implement this missing functionality in the Spreadsheet class.