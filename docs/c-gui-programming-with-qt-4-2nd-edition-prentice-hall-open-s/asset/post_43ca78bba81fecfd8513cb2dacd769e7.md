
The Java syntax referring to enum values is a bit more verbose than C++, but it is easy to understand. To emit a signal, we call the emit() method on a Signal object, passing arguments of the correct types. The type-checking is done when the program is compiled.

```
private void enableFindButton(String text) {
    findButton.setEnabled(text.length() == 0);
}
```

The enableFindButton() method is essentially the same as the C++ original.

```java
private QLabel label;
private QLineEdit lineEdit;
private QCheckBox caseCheckBox;
private QCheckBox backwardCheckBox;
private QPushButton findButton;
private QPushButton closeButton;
```

In keeping with the code in the rest of the book, we have declared all the widgets as private fields of the class. This is purely a matter of style; there is nothing stopping us from declaring in the constructor itself those widgets that are referred to only in the constructor. For example, we could have declared label and closeButton in the constructor since they are not referred to anywhere else, and they would not be garbage-collected when the constructor finishes. This works because Qt Jambi uses the same parent-child ownership mechanism as C++/Qt, so once the label and closeButton are laid out, the FindDialog form takes ownership of them, and behind the scenes it keeps a reference to keep them alive. Qt Jambi deletes widgets recursively, so if a top-level window is deleted, the window in turn deletes all its child widgets and layouts, which delete theirs, and so on, until cleanup is complete.

![](img/5a524abdf0b0d58fa99d30abb4463611_988_0.png)

Qt Jambi is fully aware of Java's resource system, unlike many of Java's standard classes. Java resources are identified by a classpath prefix. Anywhere a file name can be used in the Qt Jambi API, a Java resource can be specified instead. For example:

```java
QIcon icon = new QIcon("classpath:/images/icon.png");
if (!icon.isNull()) {
  ...
}
```

To find the icon, Qt Jambi will look in every images directory of every directory or a .jar file specified in the CLASSPATH environment variable. As soon as an image file called icon.png is found, the search stops and the file is used.

No exception is raised if the file isn't found. In the above example, if icon.png is not found, icon.isNull() will return true. Classes like UIImage and QPixmap, which have constructors that take a file name argument, have an isNull() method that can be tested to see if the file was read successfully. In the case of QFile, we can check QFile.error() to see if the file was read.

Qt Jambi makes full use of Java's garbage-collection functionality, unlike the last reference to a top-level window is deleted, the window will be scheduled for garbage collection, and no explicit call to dispose() is necessary. This approach is very convenient and works the same as in C++/Qt. The main caveat is for SDI (single document interface) applications, we must keep a reference to each top-level window that is created, to prevent them from being garbage-collected. In C++/Qt, applications normally use the Qt::WA_DeleteOnClose attribute to prevent memory leaks.

```java
public static void main(String[] args) {
  QApplication.initialize(args);
  FindDialog dialog = new FindDialog(null);
  dialog.show();
  QApplication.exec();
}
```

For convenience, we have provided the FindDialog with a main() method that instantiates a dialog and pops it up. The import com.tolltech.qt.* ensures a static QApplication object is created. When Qt Jambi application starts, we must call QApplication::initialize() and pass it the command-line arguments. This allows the QApplication object to handle the arguments it recognizes, such as -font and -style.

When we create the FindDialog, null as parent to signify that the dialog is a top-level window. Once addition the main() method is finished, the dialog will go out of scope and garbage-collected. The call to QApplication::exec() starts off the event loop, and returns control to the main() method when the user closes the dialog.

The Qt Jambi API is very similar to the C++/Qt API, but there are some differences. For example, in C++, the QWidget::mapTo() member function has the following signature:

```cpp
QPoint mapTo(QWidget *widget, const QPoint &point) const;
```

The QWidget is passed as a non-const pointer, whereas the QPoint is passed as a constant reference. In Qt Jambi, the equivalent method has the signature

```java
public final QPoint mapTo(QWidget widget, QPoint point) { ... }
```

Because Java does not have pointers, there is no visual distinction in method signatures to indicate whether an object passed to a method can be modified by the method. In theory, the mapTo() method could alter either parameter since they are both references, but Qt Jambi promises not to alter the QPoint argument, in C++ it is passed as a constant reference. In the context, it is clear which parameters are alterable and which are not. In case of doubt, we can refer to the documentation to clarify the situation.

In addition to altering arguments that are passed by value or as constant references in C++, Qt Jambi also promises that the return value of any-void method, which in C++ would be returned as a value or a constant reference, is an independent copy, so altering it will not lead to any side effects.

We mentioned earlier in Qt Jambi, whenever a QString is used. This kind of correspondence also applies to the QChar class, which has Java equivalents: char and java.lang.Character. There are similar correspondences regarding some of Qt's containers classes: QHash is replaced by java.util.HashMap, QList and QVector by java.util.List, and QMap by java.util.SortedMap. In addition, QThread is replaced by java.lang.Thread.

The Qt model/view architecture and the database API make use of all Java objects QVariant. Such a type isn't needed in Java because java.lang.Object as an ancestor, throughout Qt Jambi's API, QVariant is replaced by java.lang.Object. The extra methods that QVariant provide are available static methods in com.troll.qt.QVariant.

We have now finished reviewing a small Qt Jambi application, and we discussed many of the conceptual differences between Qt Jambi and C++/Qt programming. Building and running a Qt Jambi application is no different from any other Java application, except that the CLASPATH environment variable must specify the directory where Qt Jambi is installed. We must compile the class using a Java compiler and then we can execute the class using a Java interpreter.

```bash
export CLSPATH=$CLASSPATH:$HOME/qtjambi/qtjambi.jar:$PWD
avac FindDialog.java
java FindDialog
```

Here we have used the Bash shell to set the CLSPATH environment variable; other command-line interpreters may require a different syntax. We include the current directory in the CLSPATH so that the FindDialog class itself can be found. On Mac OS X, the command-line option -XStartOnFirstThread must be supplied to java to address a threading issue with Apple's Java virtual machine. On Windows, we execute the application like this:

```cmd
set CLSPATH=%CLASSPATH%;%JAMBIPATH%\qtjambi.jar;%CD%
avac FindDialog.java
java FindDialog
```

Qt Jambi can also be used within an IDE. In the next section, we will look at how to edit, build, and test a Qt Jambi application using the popular Eclipse IDE.

# Introduction to Qt Jambi

- Getting Started with Qt Jambi
- Using Qt Jambi in the IDE
- Integrating C++ Components with Qt Jambi

Qt Jambi is the Java edition of the application development framework. At the heart of Qt Jambi are the C++ libraries that form Qt, made available to Java programmers through the Native Interface (JNI). Although considerable effort has gone into making Qt Jambi integrate smoothly with Java and to make its API natural to Java programmers, C++/Qt programmers will still find the API familiar and predictable. All the classes are documented using Javadoc http://www.trolltech.com/qtjambi.

Now until, Java programmers had to make do with AWT, Swing, SWT, and similar class libraries, none of which are as convenient or as powerful as Qt. For example, in the traditional GUI libraries, connecting a user action, such as clicking a button, to a corresponding method involves writing an event listener class; in Qt Jambi, only one line of code is required to achieve the same thing. Qt's layout managers are much easier to use than Swing's BoxLayout GridLayout, and they produce better-looking results.

Qt Jambi applications can have main windows with menu bars, toolbars, dock windows, and a status bar, just like Qt applications written in C++. They also have the native look and feel of the platform they are running on, and they respect the user's preferences regarding themes, colors, fonts, and so on. With the full power of Qt under the hood, Qt Jambi applications can take advantage of Qt's powerful 2D graphics architecture (notably the graphics framework) and of extensions such as OpenGL.

The benefits of Qt Jambi are not limited to Java programmers. In particular, C++ programmers can make their custom Qt components available to Java programmers using the same generator tool that Trolltech uses to make the Qt API available in Qt Jambi.

In this appendix, we will show how Java programmers can start using Qt Jambi to create GUI applications. Then we will show how to make use of Qt Jambi in Eclipse, and finally we will show how to make custom C++ components available to Qt Jambi programmers. This appendix assumes that you are familiar with C++/Qt programming and with Java. Qt Jambi requires Java 1.5 or later.

## Getting Started with Qt Jambi

In this section, we will develop a small Java application that presents the window
