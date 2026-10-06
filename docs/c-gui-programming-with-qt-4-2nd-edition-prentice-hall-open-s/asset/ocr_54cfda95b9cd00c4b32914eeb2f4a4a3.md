# Integrating C++ Components with Qt Jambi

Qt Jambi lets C++ programmers easily integrate their Qt code with Java. To make our own custom C++ components available to Qt Jambi, we can use the Qt Jambi Generator, which takes a set of C++ header files and an XML file that provides some information about the C++ classes that we want to wrap and produces Java bindings for our C++ components. The Qt Jambi API itself is created using the generator.

Figure C.4 illustrates the process. After running the generator, we obtain some Java files that we must compile using the Java compiler, and some .h and .cpp files that we must compile into a C++ shared library.

# Figure C.4. Making C++ classes available in Qt Jambi

![](bbox=[0.11, 0.306, 0.689, 0.693])

To illustrate the process, we will provide bindings for the data-only PlotSettings class and for the Plotter widget that we developed in Chapter 5 (p. 121). We will then use the bindings in a Java application. Figure C.5 shows the application running.

# Figure C.5. The Jambi Plotter application