

```java
import com.trolltech.qt.*;
import com.trolltech.qt.gui.*;
```

```java
public class LabeledLineEdit extends QWidget {
```

第一个 import 声明用于访问 Qt Jambi 的 @PropertyReader() 和 @QtPropertyWriter() 注解，这些注解允许我们把属性导出到 Qt Designer。

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

对于只读属性，我们可以直接使用 @QtPropertyReader() 注解并提供一个 getter 方法。在这里，我们想要提供读写属性，每个属性都有一个 getter 和 setter。在这个示例中，我们可以省略这些注解，因为访问器方法符合 Qt 的命名规范。

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

该构造函数是非常常规的。为了要在控件框中使用，我们必须提供一个接受单个 QWidget 参数的构造函数。

```java
public static void main(String[] args) {
    QApplication.initialize(args);
    LabeledLineEdit testLineEdit = new LabeledLineEdit(null);
    testLineEdit.setText("Test");
    testLineEdit.show();
    QApplication.exec();
}
```

Eclipse 会自动生成 main() 方法。我们向 LabeledLineEdit 构造函数传递了 null，并添加了一行来设置标签的文本属性。

一旦我们有了自定义控件，就可以通过将其 .java 文件复制到包管理器中的项目 src 目录将其添加到项目中。我们调用项目的属性（Properties）对话框，并点击 Qt Designer 插件（Plugins）页面。此页面列出了项目中所有合适的 QWidget 子类。我们只需要为所有想要出现在控件框中的子类勾选“启用”（Enable）复选框，并点击确定。下次我们使用集成的 Qt Designer 编辑表单时，我们作为插件添加到项目的控件将出现在控件框底部的独立区域。

到此，我们结束了对使用 Eclipse 进行 Qt Jambi 编程的简要介绍。Eclipse 提供了一个强大且功能齐全的 IDE，为软件开发提供了许多便利。通过 Qt Jambi 集成，完全可以在 Eclipse 环境中创建 Qt Jambi 应用程序，包括使用 Qt Designer 的应用程序。Trolltech 还提供了 C++/Qt 的 Eclipse 集成，具有与 Qt Jambi 大多数相同的优势。

# 将 C++ 组件集成到 Qt Jambi

Qt Jambi 让 C++ 程序员能够轻松将他们的 Qt 代码与 Java 集成。为了让我们自定义的 C++ 组件对 Qt Jambi可用，我们可以使用 Qt Jambi 生成器，它接受一组 C++ 头文件和一个提供有关我们想要封装的 C++ 类信息的 XML 文件，并为我们的 C++ 组件生成 Java 绑定（bindings）。Qt Jambi API 本身就是使用该生成器创建的。

图 C.4 描述了这一过程。运行生成器后，我们获得了一些必须使用 Java 编译器编译的 Java 文件，以及一些必须编译成 C++ 共享库的 .h 和 .cpp 文件。

# 图 C.4. 在 Qt Jambi 中使 C++ 类可用

![](img/5a524abdf0b0d58fa99d30abb4463611_1006_0.png)

为了阐明这一过程，我们将为第 5 章（第 121 页）中开发的纯数据 PlotSettings 类和 Plotter 控件提供绑定。然后我们将在 Java 应用程序中使用这些绑定。图 C.5 显示了应用程序的运行情况。

# 图 C.5. Jambi Plotter 应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_1007_0.png)

我们需要头文件必须定义（或包含定义了）构建要构建的库所需的全部类头文件：

```cpp
#include <QtGui>
```

```cpp
#include "../plotter/plotter.h"
```

我们假设 Plotter 示例代码位于与 Qt Jambi 包装器并行的目录下。我们还需要一个 XML 文件告诉生成器封装什么以及如何封装。该文件名为 jambiplotter.xml：

```xml
<typesystem package="com.softwareinc.plotter">
  <default-superclass="com.trolltech.qt.QtJambiObject">
  <load-typesystem name="/trolltech/generator/typesystem_core.txt" generate="no">
  <load-typesystem name="/trolltech/generator/typesystem_gui.txt" generate="no">
  <object-type name="Plotter">
  <value-type name="PlotSettings" />
</typesystem>
```

在外部标签中，我们为 Plotter 组件指定了 Java 包名 com.softwareinc.plotter。 <load-typesystem> 标签导入了关于 Qt 和 Jambi 模块的相关信息。

<object-type> 和 <value-type> 标签指定了我们希望提供的可用的两个 C++ 类。我们指定了 Plotter 类是一个 C++ “对象类型”（object type）；这适用于无法复制的对象，例如控件。相比之下，PlotSettings 类被处理为 C++ “值类型”（value type）。

对于 Qt Jambi 来说，这两者之间没有明显区别。当生成器将 C++ API 转换为 Java API 时，这种区别变得非常重要。例如，如果从方法返回一个“值类型”，生成器将确保返回一个新的独立的对象（以避免副作用），但如果返回的类型是对象类型，则返回原始对象的引用。

我们需要两个环境变量，一个指定 Qt Jambi 的路径，另一个指定 Java 的路径。以下是我们在 Unix 系统上设置它们的方法（使用 Bash 壳）：

```bash
export JAMBIPATH=$HOME/qtjambi-linux3
export JAVA=/usr/lib/java/1.6
```

在 Windows 上，我们将写道

```cmd
set JAMBIPATH=C:\QtJambi
set JAVA="C:\Program Files\Java\jdk6"
```

当然，版本号和目录可能会根据你的系统而异。从现在起我们假设 JAMBIPATH 和 JAVA 是可用的。

一旦有了头文件和 XML 文件，我们就可以运行生成器：

```bash
$JAMBIPATH/bin/generator jambiplotter.h jambiplotter.xml
```

现在，在 Windows 上，我们可以这样运行生成器：

```cmd
%JAMBIPATH%\bin\generator jambiplotter.h jambiplotter.xml
```

代码生成需要一段时间，并在控制台上输出摘要。对于我们的示例，生成器产生了以下文件，位于两个并行目录：

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

我们现在必须编译 Java 和 C++ 文件，但在此之前，我们应该确保 CLSPATH 环境变量设置正确。例如，如果我们使用 Bash 壳，我们可能会这样做：

```bash
export CLSPATH=$CLASSPATH:$JAMBIPATH/qtjambi.jar:$PWD:$PWD/.
```

在这里我们扩展了现有的 CLSPATH，包含了 Qt Jambi 的 jar 文件、当前目录以及当前目录的父目录。我们需要父目录以便访问并行的 com 目录。在 Windows 上，语法将

```cmd
set CLSPATH=%CLASSPATH%;%JAMBIPATH%\qtjambi.jar;%CD%;%CD%\.
```

我们现在可以将 .java 文件编译为 .class 文件：

```bash
cd ../com/softwareinc/plotter
javac *.java
```

编译 .java 文件后，我们必须返回 jambiplotter 目录。在这里，下一步是创建一个提供 C++ 代码的 C++ 共享库

