```
spreadsheet.qrc
qt/QtGui
qt/QtCore ;
```

The first line pulls in the Qt 4 support, and we must provide the Qt 4 installation path. Next, we specify that we want to build an executable called spreadsheet and that it depends on the files listed. For header files, Boost.Build is smart enough to figure out the dependencies for itself, so normally we don't need to list them. However, .h files that define Q_OBJECT classes must be processed by moc, so we must include them in the file. The clean up up, the last two lines specify the Qt libraries we want to use.

Assuming that the bjam executable is in the path, we can build the application using the following command:

```
bjam release
```

This tells Boost.Build to build the application specified in the current directory's Jamroot file using a release build. (If you installed only Qt's debug libraries, this will produce errors; run bjam debug in that case.) moc, uic, and rcc tools will be run as necessary. To clean up, run bjam clean release.

# SCons: Software Construction Tool

The SCons tool, available at http://www.scons.org/, is an open source Python-based build tool that is meant to replace make. It has built-in support for Qt 3, and an add-on to support Qt 4 is available from David García Garzón http://www.iua.upf.edu/~dgarcia/Coders/sconstools.html. There is one file to download from that site, qt4.py, and this should be in the same directory as the application. Qt4 extension is expected to be included in the official SCons release in course.

Once qt4.py is in place, we can create SConstruct file where where we specify our build:

Code View:

```
#!/usr/bin/env python

import os

QT4_PATH = "."
QTDIR = "homekathy/opt/qt432"
```