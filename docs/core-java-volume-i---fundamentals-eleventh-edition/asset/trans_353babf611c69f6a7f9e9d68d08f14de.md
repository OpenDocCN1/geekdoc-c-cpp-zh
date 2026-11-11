
## 代码清单 10.5 button/ButtonFrame.java

```java
package button;

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

/**
 * A frame with a button panel.
 */
public class ButtonFrame extends JFrame
{
   private JPanel buttonPanel;
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 200;

   public ButtonFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // create buttons
      var yellowButton = new JButton("Yellow");
      var blueButton = new JButton("Blue");
      var redButton = new JButton("Red");

      buttonPanel = new JPanel();

      // add buttons to panel
      buttonPanel.add(yellowButton);
      buttonPanel.add(blueButton);
      buttonPanel.add(redButton);

      // add panel to frame
      add(buttonPanel);

      // create button actions
      var yellowAction = new ColorAction(Color.YELLOW);
      var blueAction = new ColorAction(Color.BLUE);
      var redAction = new ColorAction(Color.RED);

      // associate actions with buttons
      yellowButton.addActionListener(yellowAction);
      blueButton.addActionListener(blueAction);
      redButton.addActionListener(redAction);
   }

   /**
    * An action listener that sets the panel's background color.
    */
   private class ColorAction implements ActionListener
   {
      private Color backgroundColor;

      public ColorAction(Color c)
      {
         backgroundColor = c;
      }

      public void actionPerformed(ActionEvent event)
      {
         buttonPanel.setBackground(backgroundColor);
      }
   }
}
```

- **javax.swing.JButton 1.2**
  - `JButton(String label)`
  - `JButton(Icon icon)`
  - `JButton(String label, Icon icon)` —— 构造一个按钮。标签字符串可以是纯文本或 HTML；例如，`"<html><b>Ok</b></html>"`。

- **java.awt.Container 1.0**
  - `Component add(Component c)` —— 将组件 c 添加到此容器中。

### 10.4.3 简洁地指定监听器

在上一节中，我们为事件监听器定义了一个类，并构造了该类的三个对象。一个监听器类有多个实例并不那么常见。最常见的是，每个监听器执行单独的动作。在这种情况下，没有必要创建单独的类。只需使用 lambda 表达式：

```java
exitButton.addActionListener(event -> System.exit(0));
```

现在考虑有多个相关动作的情况，例如上一节的彩色按钮。在这种情况下，实现一个辅助方法：

```java
public void makeButton(String name, Color backgroundColor)
{
    var button = new JButton(name);
    buttonPanel.add(button);
    button.addActionListener(event ->
        buttonPanel.setBackground(backgroundColor));
}
```

注意，lambda 表达式引用了参数变量 `backgroundColor`。

然后我们只需调用

```java
makeButton("yellow", Color.YELLOW);
makeButton("blue", Color.BLUE);
makeButton("red", Color.RED);
```

这里，我们构造了三个监听器对象，每种颜色一个，而没有显式定义类。每次调用辅助方法时，它都会创建一个实现 ActionListener 接口的类的实例。其 actionPerformed 动作引用了 backgroundColor 值，而该值实际上存储在监听器对象中。然而，所有这些都无需你显式定义监听器类、实例变量或设置它们的构造器。

> **注意：** 在较旧的代码中，你经常会看到使用匿名类：
>
> ```java
> exitButton.addActionListener(new ActionListener()
> {
>     public void actionPerformed(ActionEvent event)
>     {
>         System.exit(0);
>     }
> });
> ```
>
> 当然，这种相当冗长的代码已不再必要。使用 lambda 表达式更简单、更清晰。

### 10.4.4 适配器类

并非所有事件都像按钮点击那样容易处理。假设你想监视用户何时尝试关闭主框架，以便弹出一个对话框，并且仅在用户同意时才退出程序。

当用户尝试关闭窗口时，JFrame 对象是 WindowEvent 的源。如果你想捕获该事件，必须有一个合适的监听器对象，并将其添加到框架的窗口监听器列表中。

```java
WindowListener listener = . . .;
frame.addWindowListener(listener);
```

窗口监听器必须是实现 WindowListener 接口的类的对象。WindowListener 接口实际上有七个方法。框架会调用它们，作为对窗口可能发生的七种不同事件的响应。这些名称不言自明，只是“iconified”在 Windows 下通常称为“minimized”。以下是完整的 WindowListener 接口：

```java
public interface WindowListener
{
   void windowOpened(WindowEvent e);
   void windowClosing(WindowEvent e);
   void windowClosed(WindowEvent e);
   void windowIconified(WindowEvent e);
   void windowDeiconified(WindowEvent e);
   void windowActivated(WindowEvent e);
   void windowDeactivated(WindowEvent e);
}
```

当然，我们可以定义一个实现该接口的类，在 windowClosing 方法中添加对 System.exit(0) 的调用，并为其他六个方法编写什么都不做的函数。然而，为六个什么都不做的方法输入代码是那种没人喜欢的乏味杂活。为简化这项任务，每个具有多个方法的 AWT 监听器接口都附带一个配套的适配器类，它实现接口中的所有方法，但不对它们做任何事。例如，WindowAdapter 类有七个什么都不做的方法。你扩展适配器类，以指定对接口中某些（但不是全部）事件类型的期望反应。（像 ActionListener 这样只有一个方法的接口不需要适配器类。）

下面是我们如何定义一个重写 windowClosing 方法的窗口监听器：

```java
class Terminator extends WindowAdapter
{
   public void windowClosing(WindowEvent e)
   {
      if (user agrees)
         System.exit(0);
   }
}
```

现在你可以将 Terminator 类型的对象注册为事件监听器：

```java
var listener = new Terminator();
frame.addWindowListener(listener);
```

> **注意：** 如今，人们会将 `WindowListener` 接口的空方法实现为默认方法。然而，Swing 的发明比默认方法的出现早很多年。

### java.awt.event.WindowListener 1.1

- `void windowOpened(WindowEvent e)` —— 在窗口已打开之后调用。
- `void windowClosing(WindowEvent e)` —— 当用户发出窗口管理器命令关闭窗口时调用。注意，只有当调用窗口的 hide 或 dispose 方法时，窗口才会关闭。
- `void windowClosed(WindowEvent e)` —— 在窗口已关闭之后调用。
- `void windowIconified(WindowEvent e)` —— 在窗口已图标化之后调用。
- `void windowDeiconified(WindowEvent e)` —— 在窗口已取消图标化之后调用。
- `void windowActivated(WindowEvent e)` —— 在窗口已变为活动状态之后调用。只有框架或对话框可以处于活动状态。通常，窗口管理器会装饰活动窗口——例如，高亮标题栏。
- `void windowDeactivated(WindowEvent e)` —— 在窗口已变为非活动状态之后调用。

### java.awt.event.WindowStateListener 1.4

- `void windowStateChanged(WindowEvent event)` —— 在窗口已最大化、图标化或恢复为正常大小后调用。

### 10.4.5 动作

同一条命令通常有多种激活方式。用户可以通过菜单、按键或工具栏上的按钮选择某个功能。在 AWT 事件模型中，这很容易实现：将所有事件链接到同一个监听器。例如，假设 Action 是一个动作监听器，其 actionPerformed 方法将背景色改为蓝色。你可以将同一个对象作为监听器附加到多个事件源：

- 一个标有“Blue”的工具栏按钮
- 一个标有“Blue”的菜单项
- 一次按键 Ctrl+B

现在，无论颜色更改命令是由按钮点击、菜单选择还是按键引起的，它都会以统一的方式处理。

Swing 包提供了一种非常有用的机制来封装命令并将其附加到多个事件源：Action 接口。一个*动作*是封装以下内容的对象：

- 命令的描述（作为文本字符串和可选图标）；以及
- 执行命令所必需的参数（例如我们示例中请求的颜色）。

Action 接口具有以下方法：

```java
void actionPerformed(ActionEvent event);
void setEnabled(boolean b);
boolean isEnabled();
void putValue(String key, Object value);
Object getValue(String key);
void addPropertyChangeListener(PropertyChangeListener listener);
void removePropertyChangeListener(PropertyChangeListener listener);
```

第一个方法是 ActionListener 接口中熟悉的方法；事实上，Action 接口扩展了 ActionListener 接口。因此，凡是需要 ActionListener 对象的地方，都可以使用 Action 对象。

接下来的两个方法让你启用或禁用动作，并检查动作当前是否已启用。当动作附加到菜单或工具栏且该动作被禁用时，该选项会变灰。

putValue 和 getValue 方法让你在动作对象中存储和检索任意名称/值对。几个重要的预定义字符串，即 Action.NAME 和 Action.SMALL_ICON，将动作名称和图标存储到动作对象中：
