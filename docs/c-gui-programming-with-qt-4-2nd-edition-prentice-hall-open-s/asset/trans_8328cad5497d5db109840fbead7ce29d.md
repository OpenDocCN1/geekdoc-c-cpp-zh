
图 C.1. 除了窗口之外，Jambi Find 的外观和行为与我们在第 2 章中创建的查找工具完全相同。通过重用同一个示例，我们可以更容易看到 C++/Qt 与 QtJambi 编程之间的差异和相似之处。在审查代码时，我们将根据需要讨论 C++ 和 Java 之间的概念差异。

## 图 C.1. Jambi Find 对话框

![](img/5a524abdf0b0d58fa99d30abb4463611_993_0.png)

Jambi Find 程序的实现在名为 `FindDialog.java` 的单文件中完成。我们将逐部分审查该文件的内容，从 import 语句开始。

```
import com.trolltech.qt.core.*;
import com.trolltech.qt.gui.*;
```

这两个 import 语句使得所有的 Qt 核心类和 GUI 类对 Java 可用。可以通过 import 语句提供额外的类set（例如 `import com.trolltech.qt.opengl*`）。

```java
public class FindDialog extends QDialog {
```

`FindDialog` 类是 `QDialog` 的子类，就像 C++ 版本的示例一样。在 C++ 中，我们在头文件中声明信号，并使用 `moc` 生成支持代码。在 QtJambi 中，使用 Java 的内省机制来实现信号与槽机制。但我们需要某种声明信号的方法，这是通过 `SignalW` 类完成的：

```java
public Signal2<String, Qt.CaseSensitivity> findNext =
    new Signal2<String, Qt.CaseSensitivity>(),

public Signal2<String, Qt.CaseSensitivity> findPrevious =
    new Signal2<String, Qt.CaseSensitivity>(),
```

存在 `SignalW` 类——`Signal0`、`Signal1<T1>`， ..., `Signal9<T1, T9>`。名称中的数字表示它们接收的参数数量，`T1`、`T0` 指定参数的类型。在这里，我们声明了两个 `String`，接收两个参数。在这两种情况下，第一个参数是 Java `String`，第二个参数是 `Qt.CaseSensitivity` 类型（一个 Java 枚举）。在 Qt API 中需要 `QString` 的地方，在 QtJambi 中我们都用 `String` 代替。

与其他的 `SignalW` 类不同，`Signal0` 不是泛型类。要创建一个无参数的信号，我们这样使用 `Signal0`：

```java
public Signal0 somethingHappened = new Signal0();
```

创建了需要的信号后，我们现在准备好查看构造函数的实现了。该方法相当长，我们将分三部分来查看。

```java
public FindDialog(QWidget parent) {
  super(parent);

  label = new QLabel(tr("Find &what:"));
  lineEdit = new QLineEdit();
  label.setBuddy(lineEdit);

  caseCheckBox = new QCheckBox(tr("Match &case"));
  backwardCheckBox = new QCheckBox(tr("Search &backward"));

  findButton = new QPushButton(tr("&Find"));
  findButton.setDefault(true);
  findButton.setEnabled(false);

  closeButton = new QPushButton(tr("Close"));
}
```

在 Java 中创建小部件与 C++ 相比唯一区别在于语法上的细微差别。注意 `tr()` 返回的是 `String` 而不是 `QString`。

```java
lineEdit.textChanged.connect(this, "enableFindButton(String)");
findButton.clicked.connect(this, "findClicked()");
closeButton.clicked.connect(this, "reject()");
```

Qt Jambi 中信号与槽连接的语法与 C++/Qt 有些不同，但它仍然很短且简单。通常，语法为：

```java
sender.signalName.connect(receiver, "slotName(T1, ..., TN)");
```

在 C++/Qt 中，我们不需要为信号指定签名。如果信号的参数比它连接的槽多，则额外的参数将被忽略。此外，在 QtJambi 中，信号-槽机制不仅限于 `QObject` 的子类：任何继承 `QSignalEmitter` 的类都可以发射信号，并且该类的任何方法都可以作为槽。

```java
QHBoxLayout topLeftLayout = new QHBoxLayout();
topLeftLayout.addWidget(label);
topLeftLayout.addWidget(lineEdit);

QVBoxLayout leftLayout = new QVBoxLayout();
leftLayout.addWidget(caseCheckBox);
leftLayout.addWidget(backwardCheckBox);

QVBoxLayout rightLayout = new QVBoxLayout();
rightLayout.addWidget(findButton);
rightLayout.addWidget(closeButton);

QHBoxLayout mainLayout = new QHBoxLayout();
mainLayout.addLayout(leftLayout);
mainLayout.addLayout(rightLayout);
setLayout(mainLayout);
```
