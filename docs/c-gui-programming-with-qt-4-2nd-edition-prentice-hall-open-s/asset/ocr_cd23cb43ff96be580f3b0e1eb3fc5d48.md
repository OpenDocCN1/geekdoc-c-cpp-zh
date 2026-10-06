java.lang.Thread.

The Qt model/view architecture and the database API make use of all Java objects QVariant. Such a type isn't needed in Java because java.lang.Object as an ancestor, throughout Qt Jambi's API, QVariant is replaced by java.lang.Object. The extra methods that QVariant provide are available static methods in com.troll.qt.QVariant.

We have now finished reviewing a small Qt Jambi application, and we discussed many of the conceptual differences between Qt Jambi and C++/Qt programming. Building and running a Qt Jambi application is no different from any other Java application, except that the CLASPATH environment variable must specify the directory where Qt Jambi is installed. We must compile the class using a Java compiler and then we can execute the class using a Java interpreter.

```
export CLSPATH=$CLASSPATH:$HOME/qtjambi/qtjambi.jar:$PWD
avac FindDialog.java
java FindDialog
```

Here we have used the Bash shell to set the CLSPATH environment variable; other command-line interpreters may require a different syntax. We include the current directory in the CLSPATH so that the FindDialog class itself can be found. On Mac OS X, the command-line option -XStartOnFirstThread must be supplied to java to address a threading issue with Apple's Java virtual machine. On Windows, we execute the application like this:

```
set CLSPATH=%CLASSPATH%;%JAMBIPATH%\qtjambi.jar;%CD%
avac FindDialog.java
java FindDialog
```

Qt Jambi can also be used within an IDE. In the next section, we will look at how to edit, build, and test a Qt Jambi application using the popular Eclipse IDE.