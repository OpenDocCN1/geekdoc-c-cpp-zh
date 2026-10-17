
```cpp
while (i < context->argumentCount()) {

    QScriptValue qsArg = context->argument(i);

    if (unaryFunc.isValid()) {

      QScriptList qsList;

      qsList << qsArg;

      qsArg = unaryFunc.call(QScriptValue(), qsList);

    }

    result += qsArg.toNumber();

    ++i;

  }

  return QScriptValue(interpreter, result);
```

`sum()`函数可以通过两种不同的方式调用。简单的方法是不带任何参数调用它；此时`unaryFunc`将是一个无效的`QScriptValue`，执行的操作将仅仅是对数字求和并返回结果。更微妙的方法是将 ECMAScript 函数作为第一个参数调用函数，后面跟着任意数量的数字参数。在这种情况下，每个数字都会调用一次给函数，并对结果进行累加后返回。我们在本章第一节的 ECMAScript 中（第 514 页）也使用了同一个函数。使用 C++ 而不是 ECMAScript 实现底层功能有时可以带来显著的性能提升。

在从脚本调用 C++ 函数之前，我们必须使用`newFunction()`和`setProperty()`让这些函数对解释器可用：

```cpp
QScriptValue qsSquare = interpreter.newFunction(square);
interpreter.globalObject().setProperty("square", qsSquare);
```

```cpp
QScriptValue qsSum = interpreter.newFunction(sum);
interpreter.globalObject().setProperty("sum", qsSum);
```

我们已经将`square()`和`sum()`作为全局函数提供给解释器。现在我们可以在脚本中使用它们，如下所示代码所示：

```javascript
interpreter.evaluate("print(sum(1, 2, 3, 4, 5, 6));");
interpreter.evaluate("print(sum(square, 1, 2, 3, 4, 5, 6));");
```

到此，我们结束了关于使用 Qt 模块使 Qt 应用程序脚本化的介绍。该模块提供了丰富的文档，包括广泛的概述，以及它所提供的类的详细描述，包括`QScriptContext`、`QScriptEngine`、`QScriptValue`和`QScriptable`，所有内容都值得阅读。

## 2. 平台特定特性

![](img/5a524abdf0b0d58fa99d30abb4463611_891_0.png)

- 与原生 API 接口接
- 在 Windows 上使用 ActiveX
- 处理 X11 会话管理

在本章中，我们将回顾 Qt 程序员可用的某些平台特定选项。我们首先查看如何访问原生 API，例如 Windows 上的 Win32 API、Mac OS X 上的 Carbon 以及 X11 上的 Xlib。然后我们将探索 ActiveX 扩展，展示如何在 Qt/Windows 应用程序中使用 ActiveX 控件，以及如何创建作为 ActiveX 服务器的应用程序。在最后的一节中，我们将解释如何让 Qt 应用程序在 X11 下与会话管理器协作。

除了这里介绍的功能外，Trolltech 还提供了多个平台特定的 Qt 解决方案，包括 Qt/Motif 和 Qt/MFC。

- `Q_OS_CYGWIN`
- `Q_OS_DGUX`
- `Q_OS_DYNIX`
- `Q_OS_FREEBSD`
- `Q_OS_HPUX`
- `Q_OS_HURD`
- `Q_OS_IRIX`
- `Q_OS_LINUX`
- `Q_OS_LYNX`
- `Q_OS_MAC`
- `Q_OS_NETBSD`
- `Q_OS_OPENBSDD`
- `Q_OS_OS2EMX`
- `Q_OS_OSF`
- `Q_OS_QNX6`
- `Q_OS_QNX`
- `Q_OS_RELIANT`
- `Q_OS_SCO`
- `Q_OS_SOLARIS`
- `Q_OS_ULTRIX`
- `Q_OS_UNIXWARE`
- `Q_OS_WIN32`
- `Q_OS_WIN64`

我们可以假设这些宏中最多只有一个会被定义。为了方便起见，当检测到 Win32 或 Win64 时，Qt 会定义`Q_OS_WIN`；当检测到任何基于 Unix 的操作系统（包括 Linux 和 Mac OS）时，定义`Q_OS_UN`。在运行时，我们可以通过`QInfo::Version`或`QInfo::MacintoshVersion`来区分不同的 Windows 版本（2000, Me）或 Mac OS 版本（10.2, 10.3 等）。

在操作系统和窗口系统宏中，还存在一组编译器宏。例如，如果编译器是 Microsoft C++，则存在`Q_CC_MSVC`。这对于绕过编译器 Bug 非常有用。

Qt 的几个 GUI 相关的类提供了平台特定的函数，用于返回底层对象的低级句柄（handles）。这些函数列于图 23.2。

### 图 23.2. 用于访问低级句柄的平台特定函数

| Mac OS X | Windows |
| :--- | :--- |
| ATSFormatRef | QFont::handle() |
| HCURSOR | Cursor::handle() |
| CGImageRef | Qpixmap::macCGHandle() |
| HDC | QPaintEngine::getDC() |
| GWPtr | Qpixmap::macQDAlphaHandle() |
| HDC | QPrintEngine::getPrinterDC() |
| GWPtr | Qpixmap::macQDHandle() |
| HFONT | QFont::handle() |
| RgnHandle | QRegion::handle() |
| HPALETTE | QColormap::hPal() |
| HIVViewRef | QWidget::winId() |
| HRGN | QRegion::handle() |
| | HWND | QWidget::winId() |

| X11 | |
| :--- | :--- |
| Cursor | Cursor::handle() |
| Font | QFont::handle() |
| Picture | Qpixmap::x11PictureHandle() |
| Picture | QWidget::x11PictureHandle() |
| Pixmap | Qpixmap::handle() |
| QX11Info | Qpixmap::x11Info() |

| QX11Info | QWidget::Info() |
| :--- | :--- |
| Region | QRegion::handle() |
| Screen | QCursor::x11Screen() |
| SmConn | QSessionManager::handle() |
| Window | QWidget::handle() |
| Window | QWidget::winId() |

在 X11 上，`QPixmap::x11Info()`和`QWidget::x11Info()`返回一个`QX11 Info`，它提供了各种指针或句柄，如`display()`、`screen()`、`colormap()`和`visual()`。例如，我们可以使用这些在 QPixmap 或 QWidget 上设置 X11 图形上下文。

需要与其他工具包或库交互的 Qt 通常需要在事件转换为`QEvent`之前访问低级事件（X11 上的`XEvent`、Windows 上的`MSGs`、Mac OS 上的`EventRef`以及 QWS 上的`QWEvents`）。我们可以通过子类`QApplication`并重实现相关的平台特定事件过滤器（`x11EventFilter()`、`winEventFilter()`、`macEventFilter()`或`qwsEventFilter()`之一）来实现。或者，我们可以通过重实现`x11Event()`、`winEvent()`、`macEvent()`或`qwsEvent()`之一，在给定的 QWidget 上访问它们。这对于处理 Qt 通常忽略的某些类型的事件（如摇杆杆事件）非常有用。

有关事件类型和平台特定问题（包括如何在不同平台上部署 Qt 应用）的更多信息，请参见 http://doc.trolltech.com/4.3/winsystem.html。

## 2. 平台特定特性

![](img/5a524abdf0b0d58fa99d30abb4463611_897_0.png)

- 与原生 API 接口
- 在 Windows 上使用 ActiveX
- 处理 X11 会话管理

在本章中，我们将回顾 Qt 程序员可以使用的某些平台特定选项。我们首先查看如何访问原生 API，例如 Windows 上的 Win32 API、Mac OS X 上的 Carbon 以及 X11 上的 Xlib。然后探索 ActiveQt 扩展，展示如何在 Qt/Windows 应用程序中使用 ActiveX 控件以及如何创建作为 ActiveX 服务器的应用程序。在最后一节中，我们将解释如何让 Qt 应用程序在 X11 下配合会话管理器。

除了这里介绍的功能外，Trolltech 还提供了几个平台特定的 Qt Solution，包括 Qt/Motif 和 Qt/MFC 框架，以确保 Motif/Xt 和 MFC 应用程序迁移到 Qt。froglogic 提供了针对 Tcl/Tk 的类似扩展，Klarär 提供了 Microsoft Windows 资源转换器。请访问以下网页获取详细信息：
- http://doc.trolltech.com/4.3/winsystem.html
- http://doc.trolltech.com/4.3/qt/
- http://www.trolltech.com/qt/

Qt 提供的某些功能是以平台无关的方式实现的。但在某些情况下，我们可能需要使用原生 API。

## 与原生 API 交互

Qt 提供了许多功能以满足各种需求。在本节中，我们将展示如何使用原生 API，例如 Windows 上的 Win32 API、Mac OS X 上的 Carbon 以及 X11 上的 Xlib。

在 X11 上，使用`QWidget::winId()`可以获取窗口特定的 ID。`QX11 Info`提供了各种指针或句柄。

```cpp
// 在 X11 上，如何修改窗口属性
#ifdef Q_WS_X11
Atom atom = XInternAtom(QX11Info::display(), "MY_PROPERTY", False);
long data = 1;
XChangeProperty(QX11Info::display(), winID(), atom, 32, PropReplace, reinterpret_cast<uchar*>(&data));
#endif
```

混合 QPainter 和 GDI 会导致奇怪的结果，特别是在 GDI 调用之后进行 QPainter 调用：

```cpp
void MyWidget::paintEvent(QPaintEvent *event)
{
  QPainter painter(this);
  QRect rect = rect();
  painter.fillRect(rect.adjusted(20, 20, -20, -20), Qt::red);
#ifdef Q_WS_WIN
  HDC hdc = painter.paintEngine()->getDC();
  Rectangle(hdc, 40, 40, width() - 40, height() - 40);
#endif
}
```

图 23.1. 带标题栏的 Mac OS 窗口
![](img/5a524abdf0b0d58fa99d30abb4463611_897_0.png)

在操作系统和窗口系统宏中，还有一组编译器宏。例如，如果编译器是 Microsoft C++，则存在`Q_CC_MSVC`。这对于规避编译器 Bug 非常有用。

Qt 的几个 GUI 相关的类提供了平台特定的函数，可以返回底层对象的低句柄。这些函数列于图 23.2。

## 图 23.2. 访问底层句柄的平台特定函数

| Mac OS X |
| :--- | :--- |
| ATSFormatRef | QFont::handle() |
| CGImageRef | Qpixmap::macCGHandle() |
| GWPtr | Qpixmap::macQDAlphaHandle() |
| GWPtr | Qpixmap::macQDHandle() |
| RgnHandle | QRegion::handle() |
| HIVViewRef | QWidget::winId() |

| Windows |
| :--- | :--- |
| HCURSOR | Cursor::handle() |
| HDC | QPaintEngine::getDC() |
| HDC | QPrintEngine::getPrinterDC() |
| HFONT | QFont::handle() |
| HPALETTE | QColormap::hPal() |
| HRGN | QRegion::handle() |
| HWND | QWidget::winId() |

| X11 |
| :--- | :--- |
| Cursor | Cursor::handle() |
| Font | QFont::handle() |
| Picture | Qpixmap::x11PictureHandle() |
| Picture | QWidget::x11PictureHandle() |
| Pixmap | Qpixmap::handle() |
| QX11Info | Qpixmap::x11Info() |

| QX11Info | QWidget::Info() |
| Region | QRegion::handle() |
| Screen | QCursor::x11Screen() |
| SmConn | QSessionManager::handle() |
| Window | QWidget::handle() |
| Window | QWidget::winId() |

在 X11 上，`QPixmap::x11Info()`和`QWidget::x11Info()`返回一个`QX11Info`，它提供了各种指针或句柄，如`display()`、`screen()`、`colormap()`和`visual()`。例如，我们可以使用这些在`QPixmap`或`QWidget`上设置 X11 图形上下文。

需要与其他工具包或库接口的 Qt 应用程序经常需要在事件转换为`QEvent`之前访问低级事件（X11 上的`XEvent`、Windows 上的`MSG`、Mac OS X 上的`EventRef`以及 QWS 上的`QWEvents`）。我们可以通过子类`QApplication`并重新实现相关的平台特定事件过滤器`x11EventFilter()`、`winEventFilter()`、`macEventFilter()`和`qwsEventFilter()`。或者，我们可以通过重新实现`x11Event()`、`winEvent()`、`macEvent()`或`qwsEvent()`在给定的`QWidget`上访问它们。这对于处理 Qt 忽略的某些类型的事件非常有用。

关于平台特定问题类型以及如何在不同平台上部署 Qt 应用程序的更多信息，请参见 http://doc.qt.com/development/windows.html。

## Windows 上的 Microsoft ActiveX

Microsoft ActiveX 技术允许应用程序整合其他应用程序或库提供的用户界面组件。它构建在 Microsoft COM 之上，为使用组件的应用程序定义了一组接口，并为提供组件的应用程序和库定义了另一组接口。

Qt/Windows Desktop 版提供了 ActiveQt 框架来无缝结合 ActiveX 和 Qt。ActiveQt 包含两个模块：

- `QAContainer`模块允许我们使用 COM 对象并在 Qt 中嵌入 ActiveX 。
- `QAServer`模块允许我们使用 Qt 导出自定义 COM 对象和 ActiveX 。

我们的第一个示例将使用`QAContainer`模块在 Qt 应用程序中嵌入 Windows Media Player（见图 23.3）。该 Qt 应用程序为 Windows Media Player ActiveX 添加了一个播放/暂停按钮、停止按钮和一个滑动块。

### 图 23.3. 播放器应用程序

![](img/5a24abdf0b0d58fa99d0abb463611903.png)

应用程序的主窗口类型为`PlayerWindow`：

```cpp
class PlayerWindow : public QWidget
{
    Q_OBJECT
    Q_ENUM(ReadyState)
public:
    enum State { Stopped = 0, Paused = 1, Playing = 2 };
```
