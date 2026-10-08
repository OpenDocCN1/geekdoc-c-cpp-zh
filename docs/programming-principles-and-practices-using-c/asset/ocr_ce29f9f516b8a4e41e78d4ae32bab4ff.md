+   13.1 Overview of graphics classes

+   13.2 Point and Line

+   13.3 Lines

+   13.4 Color

+   13.5 Line_style

+   13.6 Open_polyline

+   13.7 Closed_polyline

+   13.8 Polygon

+   13.9 Rectangle

+   13.10 Managing unnamed objects

+   13.11 Text

+   13.12 Circle

+   13.13 Ellipse

+   13.14 Marked_polyline

+   13.15 Marks

+   13.16 Mark

+   13.17 Images

# 13.1 Overview of graphics classes

Graphics and GUI libraries provide lots of facilities. By “lots” we mean hundreds of classes, often with dozens of functions applying to each. Reading a description, manual, or documentation is a bit like looking at an old-fashioned botany textbook listing details of thousands of plants organized according to obscure classifying traits. It is daunting! It can also be exciting – looking at the facilities of a modern graphics/GUI library can make you feel like a child in a candy store, but it can be hard to figure out where to start and what is really good for you.

One purpose of our interface library is to reduce the shock delivered by the complexity of a full-blown graphics/GUI library. We present just two dozen classes with hardly any operations. Yet they allow you to produce useful graphical output. A closely related goal is to introduce key graphics and GUI concepts through those classes. Already, you can write programs displaying results as simple graphics. After this chapter, your range of graphics programs will have increased to exceed most people’s initial requirements. After Chapter 14, you’ll understand most of the design techniques and ideas involved so that you can deepen your understanding and extend your range of graphical expression as needed. You can do so either by adding to the facilities described here or by adopting another C++ graphics/GUI library.

The key interface classes are:

| Graphics interface classes |
| :--- |
| Color | used for lines, text, and filling shapes |
| Line_style | used to draw lines |
| Point | used to express locations on a screen and within a Window |