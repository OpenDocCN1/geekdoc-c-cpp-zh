Qt Jambi is fully aware of Java's resource system, unlike many of Java's standard classes. Java resources are identified by a classpath prefix. Anywhere a file name can be used in the Qt Jambi API, a Java resource can be specified instead. For example:

```
QIcon icon = new QIcon("classpath:/images/icon.png");
if (!icon.isNull()) {
  ...
}
```

To find the icon, Qt Jambi will look in every images directory of every directory or a .jar file specified in the CLASSPATH environment variable. As soon as an image file called icon.png is found, the search stops and the file is used.

No exception is raised if the file isn't found. In the above example, if icon.png is not found, icon.isNull() will return true. Classes like UIImage and QPixmap, which have constructors that take a file name argument, have an isNull() method that can be tested to see if the file was read successfully. In the case of QFile, we can check QFile.error() to see if the file was read.

Qt Jambi makes full use of Java's garbage-collection functionality, unlike the last reference to a top-level window is deleted, the window will be scheduled for garbage collection, and no explicit call to dispose() is necessary. This approach is very convenient and works the same as in C++/Qt. The main caveat is for SDI (single document interface) applications, we must keep a reference to each top-level window that is created, to prevent them from being garbage-collected. In C++/Qt, applications normally use the Qt::WA_DeleteOnClose attribute to prevent memory leaks.

```
public static void main(String[] args) {
  QApplication.initialize(args);
  FindDialog dialog = new FindDialog(null);
  dialog.show();
  QApplication.exec();
}
```