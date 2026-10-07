
# 314 ► 第8章

```java
Thread.sleep(200);
} catch (InterruptedException e) {}

System.out.println("CancelTicket now waiting to lock on train...");

// 锁定火车

synchronized(train) {

    System.out.println("CancelTicket locked on train");

}

}
}
```

```java
class Deadlock {

    public static void main(String args[]) {

        Object train = new Object();

        Object comp = new Object();

        BookTicket b1 = new BookTicket(train, comp);

        CancelTicket c1 = new CancelTicket(train, comp);

        b1.start();

        c1.start();

    }

}
```

```java
# 314 ► 第8章

class DeadLock {

    public static void main(String[] args) throws Exception {

        //火车、车厢作为Object的对象

        Object train = new Object();

        Object compartment = new Object();

        //为BookTicket, CancelTicket类创建对象

        BookTicket obj1 = new BookTicket(train,compartment);

        CancelTicket obj2 = new CancelTicket(train,compartment);

        //将两个线程绑定到这些对象

        Thread t1= new Thread(obj1);

        Thread t2= new Thread(obj2);

        //在对象上运行线程

        t1.start();

        t2.start();

    }

}
```

输出：
`BookTicket locked on train`
`CancelTicket locked on compartment`
`BookTicket now waiting to lock on compartment...`
`CancelTicket now waiting to lock on train...`

# 09 带有GUI操作

## 目标

- 学习抽象窗口工具包 (AWT)
- 学习如何使用 AWT 窗口 (Frames)
- 探索小程序 (Applet) 及其生命周期
- 学习图形类 (Graphics Class)
- 学习颜色类 (Color Class)

到为止，你一直在学习基于控制台的 Java 程序。在如今，人们更倾向于使用基于图形用户界面 (GUI) 的应用程序，因为前者是具交互性的用户界面。基于 GUI 的应用程序是用户通过各种组件（如文本字段和按钮）进行交互的应用程序。Java 抽象窗口工具包 (AWT) 和 Swing 应用程序编程接口 (API) 来创建交互式 GUI 应用程序。你可以使用 `java.awt` 和 `javax.swing` 包，它们包含了各种类、接口和方法，用于创建基于 GUI 的应用程序。你将探索 awt 包中重要的类和接口。

在本章中，你将学习另一种允许我们与 Web 世界通信的 Java 程序。这类程序被称为小程序 (applet)。小程序是一种用 Java 编程语言编写的基于 Internet 的程序，任何计算机都可以下载。它通常嵌入网站的 HTML 页面中，并可以从浏览器执行。用户允许对小程序进行个性化，因为它作为一个菜单工作，通过使用它的各种设置，然后你可以从此菜单中选择任何选项来加载相应的页面。页面包含一个可以用 Java 类编写的小程序，例如 Internet Explorer。小程序可以使用 awt 包中的各种类，如 Graphic、Font 和 Color，来执行各种任务，如绘制矩形和弧、选择字体编写消息以及在矩形中填充颜色。`Graphics` 类在小程序中创建各种形状，如线条和矩形。`Color` 类向形状中填充或设置颜色，而 `Font` 类设置用于在小程序中编写文本的字体。

让我们从下一节开始学习 AWT。

## 9.1 介绍 AWT

AWT 是一个由 API 提供的工具包，有助于创建基于 GUI 的（Windows）应用程序。AWT API 提供了存储在 `java.awt` 包中的各种类，用于在应用程序中创建 GUI 组件。使用 `java.awt` 包，你可以创建并显示按钮、标签、复选框、文本字段以及你想在 Windows 应用程序中显示的其他用户界面组件。表 1 列出了 `java.awt` 包中提供的重要类，它们帮助你创建基于 GUI 的应用程序：

# 316 ► 第9章

| 表 1：AWT 包中重要类的说明 |
| :--- | :--- |
| Component | 作为各种 AWT 组件（如按钮和复选框）的抽象父类。 |
| Container | 包含 AWT 组件，如按钮和复选框。 |
| Panel | 为 Windows 应用程序创建一个面板。 |
| Window | 提供一个容器，Windows 应用程序可以在其中附加其他组件，包括其他面板。Window 类是 Component类的子类。 |
| Frame | 为 Windows 应用程序创建一个框架。 |

现在现在让我们在接下来的小节中详细地描述这些类。

### 探索 Component 类
`Component` 是 `java.awt` 包的基类，所有视觉组件都基于它。例如，`Button` 类直接派生自 `Component` 类。`Component` 类包含许多用于创建 GUI 应用程序的方法。表 2 列出了 `Component` 类中提供的重要方法。

| 表 2：Component 类重要方法的讨论 |
| :--- | :--- |
| getFont() | 返回组件文本的字体。 |
| void setFont(Font ft) | 为组件的文本设置指定的字体。 |
| Color getColor() | 返回组件的前景色。 |
| void setForeground(Color c) | 设置组件的前景色。 |
| Color getBackground(Color c) | 返回组件的背景色。 |
| void setBackground(Color c) | 设置组件的背景色。 |
| String getName() | 返回组件的名称。 |
| void setName(String name) | 为组件设置新名称。 |
| int getHeight() | 以整数值返回组件的像素高度。 |
| int getWidth() | 以整数值返回组件的像素宽度。 |
| Dimension getSize() | 返回组件的大小。 |
| int getX() | 返回组件的当前 x 坐标。 |
| int getY() | 返回组件的当前 y 坐标。 |
| Point getLocation() | 返回组件的位置。 |
| void setLocation(int x, int y) | 根据 x y 坐标设置组件的位置。 |
| void setSize(int width, int height) | 根据宽度和高度设置组件的大小。 |

GUI 317

| 表 2：Component 类重要方法的讨论 |
| :--- | :--- |
| void setVisible(boolean b) | 设置组件的可见性，如果 b 为真则显示，否则隐藏。 |
| void setEnabled(boolean b) | 如果 b 为真则启用组件，否则禁用。 |
| void setBounds(int x, int y, int w, int h) | 设置组件的矩形边界。x 和 y |

### 探索 Container 类
AWT 对象表示一个能够持有其他组件的组件。容器中组件的跟踪是通过列表实现的。该列表有助于定义放置的顺序。请注意，如果没有为它们定义索引，则将添加到列表末尾。`Container` 类是一个抽象类，无法实例化，其某些方法必须由其子类实现。表 3 列出了 `Container` 类的重要方法：

| 表 3：Container 类重要方法的说明 |
| :--- | :--- |
| Component add(Component comp) | 将传递的组件添加到容器的末尾。 |
| Component add(Component comp, int index) | 将传递的组件添加到容器的指定位置。 |
| Component getComponentAt(int x, int y) | 获取 x y 坐标处的组件。 |
| void remove(int index) | 移除容器中的给定组件。 |
| LayoutManager getLayout() | 获取容器的布局管理器。 |
| void setFont(Font f) | 为容器的文本设置字体。 |
| void setLayout(LayoutManager l) | 为容器设置布局。 |
| void update(Graphics g) | 更新容器。 |

### 探索 Panel 类
`Panel` 是 `Container` 类的子类，也是 `Applet` 类的父类。面板作为附加其他组件或面板的容器。你可以为面板窗口添加标题栏和边框。当小程序的屏幕输出在浏览器中显示时，屏幕输出出现在应用程序的 `Panel` 对象上。由于缺少标题栏、菜单栏或边框，当你看时就看不到这些项目

# 第 9 章

`applet` 在浏览器中运行。然而，当你使用 `applet viewer`（applet 查看器）运行 `applet` 时，`applet viewer` 会显示标题栏和复选框。你可以使用 `add()` 方法向 `Panel` 对象添加其他组件，例如按钮和复选框。在添加这些组件后，你可以使用 `Component` 类的各种方法（如 `setLocation()`、`setSize()` 或 `setBounds()`）对它们进行定位和调整大小。

## 探索 Window 类

`Window` 类是 `Container` 类的子类。`Window` 类的对象表示一个没有菜单栏或边框的顶层窗口。`WindowAdapter` 类响应 `Window` 对象的事件，例如 `WINDOW_OPENED` 和 `WINDOW_CLOSED`。你应该创建一个 `Frame` 类对象，而不是创建一个 `Window` 类实例。`Frame` 类是 `Window` 类的子类，`Frame` 类提供了带有标题栏的普通窗口。

## 探索 Frame 类

由于 `Frame` 类是 `Window` 类的子类且包含标题栏和边界，当你在 `applet` 中创建 `Frame` 对象时，执行期间会显示警告消息。

窗口的默认布局是 `BorderLayout`。`Frame` 窗口会产生事件，如 `WINDOW_OPENED`、`WINDOW_CLOSED`、`WINDOW_ACTIVATED` 和 `WINDOW_DEACTIVATED`。

既然你已经熟悉了 `java.awt` 包中的各种类，让我们学习如何创建一个帧窗口及其用于显示、隐藏和关闭窗口的各种属性。

## 9.2 使用 AWT Frame

在本节中，你将学习如何通过 AWT API 创建帧窗口。根据用户的需求，Windows 应用可能由多个组件组成，例如窗口、文本框、复选框和按钮。所有 AWT 组件都可以添加到窗口中。

现在，让我们使用 `java.awt` 包在 Windows中创建一个 Frame。为了实现这一点，执行以下主要步骤：

- 创建 Frame 窗口
- 隐藏和显示 Frame 窗口
- 设置 Frame 窗口的标题
- 关闭 Frame 窗口

现在，让我们逐一执行这些步骤。

### 创建 Frame 窗口

帧窗口是通过扩展 `Frame` 类的功能创建的。此窗口具有标题栏、菜单栏、边界以及调整大小选项（如最小化、最大化和关闭）。在创建帧窗口之前，让我们列出帮助创建帧窗口的 `Frame` 类中值得注意的构造函数，如表 4 所示：

#### 表 4：Frame 类值得注意的构造函数

| 构造函数 | 说明 |
|---|---|
| `Frame()` | 创建无标题的帧窗口。 |
| `Frame(String)` | 创建带有指定标题的帧窗口。 |

#### 表 5：Frame 类值得注意的方法描述

| 方法 | 说明 |
|---|---|
| `String getTitle()` | 返回帧窗口的标题。 |
| `boolean isResizable()` | 如果帧窗口可以调整大小，则返回 true；否则返回 false。默认情况下，所有帧窗口都是可调整大小的。 |
| `void setState(int w, int h)` | 根据传递的参数为帧窗口指定新大小。 |
| `void remove(Component m)` | 从帧窗口移除指定的菜单组件。 |
| `void setMenuBar(MenuBar m)` | 为帧窗口设置菜单栏。 |
| `void setResizable(boolean resize)` | 根据 `resize` 参数将值设置为 true 或 false。如果参数设置为 true，则用户可以调整帧窗口的大小；否则不能。 |
| `void setTitle(String title)` | 为帧窗口设置标题。 |
| `void setVisible(boolean vb)` | 根据 `vb` 参数将值设置为 true 或 false。如果 `vb` 参数设置为 true，则帧窗口可见；否则，不可见。 |

列表 1 显示了 `DemoFrame.java` 文件中帧窗口的示例（你可以在 Chapter9 文件夹的 CD 上找到 `DemoFrame.java` 文件）：

### ▶ 列表 1：创建 Frame 窗口

```java
import java.awt.*;

class DemoFrame extends Frame {

    public static void main(String[] args[]) {

        DemoFrame f = new DemoFrame();

        f.setSize(300,300);

    }

}
```

在列表 1 中，首先导入 `java.awt` 包以使用它的类和方法，然后创建 `DemoFrame` 类，它扩展了 `Frame` 类以使用其功能。在 `main()` 方法中，你创建一个 `Frame` 类对象并使用 `setSize()` 方法设置帧窗口的大小。图 1 显示了列表 1 的输出：

![](img/d3faa7f55d3d14bb5bf2778690d333_png)
图 1：执行 Frame 类

图 1 显示帧窗口已编译并成功运行，这意味着窗口已经创建。然而，问题是，如果窗口已经创建了，为什么你无法看到它呢？答案在下一节中。

### 隐藏和显示 Frame 窗口

在上一节中，你创建了一个帧窗口，但没有查看它。这是因为你没有使用显示方法。你必须使用 `setVisible()` 方法来显示或隐藏窗口。如果 `setVisible()` 方法设置为 true，则帧窗口可见；否则，它被隐藏。列表 2 显示了 `DemoFrame.java` 文件中的帧窗口示例（你可以在 Chapter9 文件夹的 CD 上找到 `DemoFrame.java`）：

### 列表 2：显示 Frame 窗口

```java
import java.awt.*;

class DemoFrame extends Frame {

    public static void main(String[] args[]) {

        DemoFrame f = new DemoFrame();

        f.setSize(300,300);

        f.setVisible(true);

    }
}
```
