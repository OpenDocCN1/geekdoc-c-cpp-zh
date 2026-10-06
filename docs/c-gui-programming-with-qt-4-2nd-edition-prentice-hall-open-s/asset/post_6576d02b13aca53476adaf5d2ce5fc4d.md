
```java
import com.trolltech.qt.*;
import com.trolltech.qt.gui.*;
```

```java
public class LabeledLineEdit extends QWidget {
```

The first import declaration is needed to access Qt Jambi's @PropertyReader() and @QtPropertyWriter() annotations, which let us export properties to Qt Designer.

```java
@PropertyReader(name="labelText")
public String labelText() { return label.text(); }
```

```java
@QtPropertyWriter(name="labelText")
public void setLabelText(String text) { label.setText(text); }
```

```java
@QtPropertyReader(name="editText")
public String getEditText() { return lineEdit.text(); }
```

```java
@QtPropertyWriter(name="editText")
public void setEditText(String text) { lineEdit.setText(text); }
```

For read-only properties, we can simply use the @QtPropertyReader() annotation and provide a getter method. Here we want to provide read-write properties, each has a getter and a setter. For this example, we could have omitted the annotations, since the accessor methods follow the Qt naming convention.

```java
public LabeledLineEdit(QWidget parent){
```

```java
super(parent);

label = new QLabel();
lineEdit = new QLineEdit();
label.setBuddy(lineEdit);

QHBoxLayout layout = new QHBoxLayout();
layout.addWidget(label);
layout.addWidget(lineEdit);
setLayout(layout);
}

private QLabel label;
private QLineEdit lineEdit;
```

The constructor is quite conventional. To use in the widget box, we must provide a constructor that takes a single QWidget argument.

```java
public static void main(String[] args) {
    QApplication.initialize(args);
    LabeledLineEdit testLineEdit = new LabeledLineEdit(null);
    testLineEdit.setText("Test");
    testLineEdit.show();
    QApplication.exec();
}
```

Eclipse generates the main() method automatically. We have passed null to the argument to the LabeledLineEdit constructor and added a line to set the label's text property.

Once we have a custom widget, we can add it to a project by copying its .java file into the project's src in the package explorer. We invoke the project's Properties dialog and click the Qt Designer Plugins page. This page lists all the suitable QWidget subclasses that are in the project. We just need to check the Enable checkbox for all of the subclasses that we want to appear in the widget box and click OK. The next time we edit a form using the integrated Qt Designer, the widgets we have added to the project as plugins will appear at the bottom of the widget box in a separate section.

This concludes our brief introduction to using Eclipse for Qt Jambi programming. Eclipse provides a powerful and functional IDE with many conveniences for software development. And with the Qt Jambi integration, it is possible to create Qt Jambi applications, including those that use Qt Designer, completely with the Eclipse environment. Trolltech also provides a C++/Qt Eclipse integration with most of the same benefits as the Qt Jambi one.

# Integrating C++ Components with Qt Jambi

Qt Jambi lets C++ programmers easily integrate their Qt code with Java. To make our own custom C++ components available to Qt Jambi, we can use the Qt Jambi Generator, which takes a set of C++ header files and an XML file that provides some information about the C++ classes that we want to wrap and produces Java bindings for our C++ components. The Qt Jambi API itself is created using the generator.

Figure C.4 illustrates the process. After running the generator, we obtain some Java files that we must compile using the Java compiler, and some .h and .cpp files that we must compile into a C++ shared library.

# Figure C.4. Making C++ classes available in Qt Jambi

![](img/5a524abdf0b0d58fa99d30abb4463611_1006_0.png)

To illustrate the process, we will provide bindings for the data-only PlotSettings class and for the Plotter widget that we developed in Chapter 5 (p. 121). We will then use the bindings in a Java application. Figure C.5 shows the application running.

# Figure C.5. The Jambi Plotter application

![](img/5a524abdf0b0d58fa99d30abb4463611_1007_0.png)

the header file we need must define (or include header files that define) all the classes necessary for the library we will build:

```cpp
#include <QtGui>
```

```cpp
#include "../plotter/plotter.h"
```

We assume that the Plotter example code lies in a directory parallel to the Qt Jambi wrapper. We also need an XML file to tell the generator what to wrap and how to wrap it. The file is called jambiplotter.xml:

```xml
<typesystem package="com.softwareinc.plotter">
  <default-superclass="com.trolltech.qt.QtJambiObject">
  <load-typesystem name="/trolltech/generator/typesystem_core.txt" generate="no">
  <load-typesystem name="/trolltech/generator/typesystem_gui.txt" generate="no">
  <object-type name="Plotter">
  <value-type name="PlotSettings" />
</typesystem>
```

In the outer tag, we specify a Java package name of com.softwareinc.plotter for the Plotter component. The <load-typesystem> tags import the information concerning the Qt and Jambi modules.

The <object-type> and <value-type> tags specify the two C++ classes we want have available. We have specified that the Plotter class is a C++ "object type"; this is suitable for objects that cannot be copied, such as widgets. In contrast, the PlotSettings class is treated as a C++ "value type".

To Qt Jambi, there is no obvious difference between the two. The distinction is important when the generator makes C++ APIs to Java APIs. For example, if a "value type" is returned from a method, the generator will ensure that a new independent object is returned (to avoid side effects), but if the returned type is an object type, a reference to the original object is returned.

We will need two environment variables, one specifying the path to Qt Jambi, the other to Java. Here is how we set them on Unix systems (using the Bash shell):

```bash
export JAMBIPATH=$HOME/qtjambi-linux3
export JAVA=/usr/lib/java/1.6
```

On Windows, we would write

```cmd
set JAMBIPATH=C:\QtJambi
set JAVA="C:\Program Files\Java\jdk1.6"
```

Naturally, the version numbers and directories may be different for your system. From now on, we will assume that JAMBIPATH and JAVA are available.

Once we have the header and XML files, we can run the generator:

```bash
$JAMBIPATH/bin/generator jambiplotter.h jambiplotter.xml
```

Now, on Windows, we can run the generator like:

```cmd
%JAMBIPATH%\bin\generator jambiplotter.h jambiplotter.xml
```

The code generation takes a few moments, and outputs some summary on the console. For our example, the generator produced the following files, in two parallel directories:

```text
../com/softwareinc/plotter/PlotSettings.java
../com/softwareinc/plotter/Plotter.java
../com/softwareinc/plotter/QtJambi_Initializer.java
../com/com_softwareinc_plotter/com_softwareinc_plotter.pri
../com/com_softwareinc_plotter/metainfo.cpp
../com/com_softwareinc_plotter/qtjambi_libraryinitializer.cpp
../com/com_softwareinc_plotter/qtjambish_PlotSettings.cpp
../com/com_softwareinc_plotter/qtjambish_PlotSettings.h
../com/com_softwareinc_plotter/qtjambish_Plotter.cpp
../com/com_softwareinc_plotter/qtjambish_Plotter.h
```

We must now compile both the Java and the C++ files, but before we do we should make sure that the CLSPATH environment variable is set correctly. For example, if we are using the Bash shell, we might do this:

```bash
export CLSPATH=$CLASSPATH:$JAMBIPATH/qtjambi.jar:$PWD:$PWD/.
```

Here we have extended the existing CLSPATH with the Qt Jambi .jar file, with the current directory, and with the current directory's parent directory. We need the parent directory so we can access the parallel com directory. On Windows, the syntax would be

```cmd
set CLSPATH=%CLASSPATH%;%JAMBIPATH%\qtjambi.jar;%CD%;%CD%\.
```

We can now compile the .java files into .class files:

```bash
cd ../com/softwareinc/plotter
javac *.java
```

After compiling the .java files, we must return to the jambiplotter directory. Here, the next step is to create the C++ shared library that provides the C++ code
