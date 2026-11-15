# 6.20 Handling graphical output

# 6.20.1 Introduction

EMBOSS can produce two types of graphics output. First are the ‘drawn’ graphics. They allow a user to draw in a graphics window using primitives for (e.g.) line and dot plotting. The other, more commonly used, graphic is the ‘graph’ plot. Several functions are provided to take the sting out of displaying graphs, for example the automatic drawing of axes and the ability to set titles for them. The graphics are currently produced using wrapper functions to PLplot. At the time development of EMBOSS began, PLplot was the only multi-platform C graphics library available with the LGPL licence.

Graph objects are created through ACD datatypes. The library calls provide an interface to the PLplot library which manages output to the screen or to files. PLplot defines a graphics viewport to work within. The viewport dimensions depend on the definitions in the PLplot drivers for each device and are not identical in size or proportion. Where the application needs to manipulate the scale of objects (for example EMBOSS application cirdna) it is recommended to work in units of millimetres (or 4 pixels) rather than arbitrary units which fail to scale when used on a different device.

General features of the graphics output include:

+   • Graphics functions can define colours, line styles, titles and axis labels and plot scaling factors.
+   • The objects plotted can be lines, shapes or text.
+   • Functions are available to calculate scaled character sizes, polar coordinates and distances between plot coordinates.
+   • The most useful internal data is PLplot scaling information including current scaling factors and the plot dimensions in millimetres.
+   • Where plot output is to a file, there are functions to control the directory and output file names.
+   • The PLplot library has general settings that are independent of any single plot. For this reason you should avoid using more than one active graph object in any EMBOSS application.

# 6.20.2 AJAX library files

AJAX library files for handling graphics are listed in the table below. Library file documentation, including a complete description of datatypes and functions, is available at: http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
|---|---|
| ajgraph | General graph handling functions |
| ajgraphstruct | Data structures for use with graphs |
| ajgraphxml | Graph XML file object and functions for manipulating it |
| ajhist | Histograms. |
| ajcall | Graphics package access |
| ajdom | Document Object Model library calls |