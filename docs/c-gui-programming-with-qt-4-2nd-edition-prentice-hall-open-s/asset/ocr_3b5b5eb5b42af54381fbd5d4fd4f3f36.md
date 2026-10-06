Plotter and PlotSettings, as well as the C++ wrapper code produced by the generator. We begin by creating a .pro file:

```
TEMPLATE = lib
TARGET = com_softwareinc_plotter
DLLDESTDIR = .
HEADERS = ../plotter/plotter.h
SOURCES = ../plotter/plotter.cpp
RESOURCES = ../plotter/plotter.qrc
INCLUDEPATH += ../plotter \
    $$(JAMBIPATH)/include \
    $$(JAVA)/include
unix {
INCLUDEPATH += $(JAVA)/include/linux
}
win32 {
INCLUDEPATH += $(JAVA)/include/win32
}
LIBS += -L$(JAMBIPATH)/lib -lqtjambi
include(../cpp/com_softwareinc_plotter/com_softwareinc_plotter.pri)
```

The TEMPLATE variable must be set to lib since we want to create a shared library rather than an application. The TARGET variable specifies the name of the Java package with underscores instead of periods, and DLLDESTDIR specifies where the shared library (or DLL) should be put. The INCLUDEPATH variable must be extended to the source directory (since it is not the current directory in this case), the Qt Jacobi include path, the Qt SDK's include path, and the SDK's platform-specific path. We cover the unix and win32 syntaxes in Appendix B.). We must also include the Qt Jacobi library itself, which we do in the LIBS entry. The include() directive at the end is used to access the C+ files the generator produced. Once we have the .pro file, we can run qmake and make to build the library.

Now that we have the shared library and suitable Java wrapper code, we are ready to make use of them in an application. The Jacobi Plot application creates a PlotSettings and a Plotter object and uses them to display some random data. The important point is that they are used just like any other Java or Qt Jacobi class. The whole application is quite small, so we will show it in full:

Code View:

```
import java.lang.Math;
import java.util.ArrayList;
import com.trolltech.qt.core.*;
```