
Plotter 和 PlotSettings，以及生成器产生的 C++ 包装代码。我们首先创建一个 .pro 文件：

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

`TEMPLATE` 变量必须设置为 `lib`，因为我们想要创建一个共享库而不是应用程序。`TARGET` 变量指定了 Java 包名（使用下划线代替点），`DLLDESTDIR` 指定了共享库（或 DLL）应该放置的位置。`INCLUDEPATH` 变量必须扩展到源目录（在这种情况下，它不是当前目录）、Qt Jacobi 包含路径、Qt SDK 的包含路径以及 SDK 特定于平台的路径（我们在附录 B 中了 unix 和 win32 语法）。我们还必须包含 Qt Jacobi 库本身，我们在 `LIBS` 条目中实现了。结尾的 `include()` 指令用于访问生成器产生的 C++ 文件。一旦有了 .pro 文件，我们就可以运行 `qmake` 和 `make` 来构建库。

现在我们已经有了共享库和合适的 Java 包装代码，准备好在应用程序中使用它们了。Jacobi Plot 应用程序创建一个 `PlotSettings` 和 `Plotter` 对象，并使用它们显示一些随机数据。关键点在于，它们的使用方式与任何其他 Java 或 Qt Jacobi 类一样。整个应用程序非常小，我们将完整展示它：

代码视图：

```
import java.lang.Math;
import java.util.ArrayList;
import com.trolltech.qt.core.*;
```

```
import com.trolltech.qt.*;
import com.softwareinc.plotter.Plotter;
import com.softwareinc.plotter.PlotSettings;

public class JambiPlotter {
    public static void main(String[] args) {
        QApplication.initialize(args);

        PlotSettings settings = new PlotSettings();
        settings.setMinX(0.0);
        settings.setMaxX(100.0);
        settings.setMinY(0.0);
        settings.setMaxY(100.0);

        int numPoints = 100;
        ArrayList<QPointF> points0 = new ArrayList<QPointF>();
        ArrayList<QPointF> points1 = new ArrayList<QPointF>();
        for (int x = 0; x < numPoints; i++) {
            points0.add(new QPointF(x, Math.random() * 100));
            points1.add(new QPointF(x, Math.random() * 100));
        }

        Plotter plotter = new Plotter();
        plotter.setWindowTitle(plotter.tr("Jambi Plotter"));
        plotter.setPlotSettings(settings);
        plotter.setCurveData(0, points0);
        plotter.setCurveData(1, points1);
        plotter.show();

        QApplication.exec();
    }
```

我们导入了 Java 的标准库和需要的 Qt Jacobi 库，以及 `PlotSettings` 和 `Plotter` 类。我们可以很容易地写下 `import com.softwareinc.plotter.*`。在初始化 `QApplication` 对象后，我们创建一个 `PlotSettings` 对象并设置某些值。该类的 C++ 版本具有 `minX`、`maxX`、`minY` 和 `maxY` 变量。除非另有说明，Qt Jacobi 生成器使用 Qt 命名约定生成访问方法（例如 `minX()` 和 `setMinX()`）。一旦有了合适的设置，我们就生成两条具有 100 个点的曲线。在 C++ 中，每条曲线的点是 `QVector<QPointF>`；在 Qt Jacobi 中，我们使用 `ArrayList<QPointF>`，并依靠 Jacobi 根据需要进行转换。

有了设置和曲线数据，我们创建一个没有父对象的 `Plotter` 对象（使其成为顶层窗口）。然后我们为 plotter 提供设置和两条曲线的数据，并调用 `show()` 使 plotter 可见。最后，我们调用 `QApplication::exec()` 启动事件循环。

编译应用程序时，必须小心不仅包含普通的 `CLASSPATH`，还要包含 `com.softwareinc.plotter` 包的路径。为了运行应用程序，还必须设置几个额外的环境变量以找到 Qt Jacobi 和我们的绑定。在 Windows 上，必须如下设置 PATH：

```
set PATH=%PATH%;%CD
```

在 Unix 上，必须设置 `LD_LIBRARY_PATH`：

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$lib:$PWD
```

在 Mac OS 上，环境变量名为 `DYLD_LIBRARY_PATH`。此外，在三个平台上，都必须设置 `QT_PLUGIN_PATH` 以包含 Qt Jacobi 的 plugins 目录。例如：

```
set QT_PLUGIN_PATH=%QT_PLUGIN_PATH%;%plugins
```

由于我们对 `CLASSPATH` 的添加，可以在所有平台上编译并运行 Jambi：我们现在完成了这个示例，并展示了如何在 Qt Jacobi 中使用 C++ 组件。事实上，让 C++ 组件供 Qt Jacobi 使用的生成器提供了比简要介绍更多的功能。虽然生成器只支持 C++ 的子集，但该子集包含了所有常见的 C++ 结构，包括多继承和运算符重载。生成器的完整文档位于 http://doc.trolltech.com/qtjambi-4.3.2_01/com/trolltech/qt/jambi-generator.html。我们将简要提到一些我们没有提到的功能。

影响生成器的关键在于我们给它的 XML 文件中的内容。例如，如果在 C++ 中有多继承，在 Qt Jacobi 中处理此的一种简单方法是识别基类。也可以提供更自然的签名。例如，与其使用 `ArrayList<QPointF>` 传递点，不如传递 `QPoint` 数组更好。这涉及到修改 `jambiplotter.xml` 文件。我们最初是这样声明 C++ `Plotter` ：

```
<object-type name="Plotter" />
```

我们将用一个更复杂的版本替换前面的行：

```
<object-type name="Plotter">
  <modify-function
    signature="curveData(int,Vector&lt;QPoint&gt;)"
    access="private"
    rename-to="curveData_private" />
  </modify-function>
  <inject-code>
    public final void curveData(int id, com.trolltech.qt.core.QPoint points[]) {
      curveData_private(id, java.util.Arrays.asList(points));
    }
  </inject-code>
</object-type>
```

在 `<modify-function>`元素中，我们将 C++ `curveData()` 方法重命名为 `curveData_private()` 并将其访问限定符改为 `private`，从而防止从类之外访问它。注意我们必须在签名属性中转义 XML 的特殊字符 `<`、`>` 和 `&`。

在 `<inject-code>`元素中，我们在 Java 中实现了一个自定义的 `curveData()` 方法。该方法接受 `QPoint[]` 参数并简单调用私有的 `curveData_private()` 方法，将数组转换为 C++ 方法期望的列表。

```
QPointF[] points0 = new QPointF[numPoints];
QPointF[] points1 = new QPointF[numPoints];
for (int x = 0; x < numPoints; x++) {
  points0[x] = new QPointF(x, Math.random() * 100);
  points1[x] = new QPointF(x, Math.random() * 100);
}
```

代码其余部分与之前相同。

在某些情况下，当类被包装时，生成器产生使用 `QNativePointer` 的代码。这种类型是 C++ “值类型”的包装器，同时适用于指针和数组。`mjb_nativepointer_api.log` 文件指定了任何使用 `QNativePointer` 的生成代码。Qt Jambi 文档建议替换任何使用 `QNativePointer` 的代码，并提供了如何执行此的步骤说明。

有时我们需要在 .java 文件中包含额外的导入声明。这可以使用 `<extra-includes>` 标签轻松实现，并在 http://doc.trolltech.com/qtjambi-4.3.2_01/com/trolltech/qt/qtjambi-typesystem.html 中有详细描述。

Qt Jambi 生成器是一个强大且多功能的工具，可以让 C++/Qt 类无缝地供 Java 程序员使用，并使得在单个项目中结合 C++ 和 Java 的优势成为可能。

