
```java
}
g2.dispose();
}
```

为了监听来自关联组件或其任何子组件的事件，`LayerUI` 类必须设置图层的事件掩码。这应在 `installUI` 方法中完成，如下所示：

```java
class PanelLayer extends LayerUI<JPanel>
{
   public void installUI(JComponent c)
   {
      super.installUI(c);
      ((JLayer<?>) c).setLayerEventMask(AWTEvent.KEY_EVENT_MASK | AWTEvent.FOCUS_EVENT_MASK);
   }

   public void uninstallUI(JComponent c)
   {
      ((JLayer<?>) c).setLayerEventMask(0);
      super.uninstallUI(c);
   }
   . . .
}
```

现在，你将在名为 `processXxxEvent` 的方法中接收事件。例如，在我们的示例应用程序中，我们会在每次按键后重绘图层：

```java
public class PanelLayer extends LayerUI<JPanel>
{
   protected void processKeyEvent(KeyEvent e, JLayer<? extends JPanel> l)
   {
      l.repaint();
   }
}
```

我们的示例程序（清单 10.32）中有三个输入字段，用于设置颜色的 RGB 值。每当用户更改这些值时，颜色就会以透明的方式显示在面板上。我们还捕获焦点事件，并以粗体字体显示获得焦点的组件的文本。

### 清单 10.32：Layer/ColorFrame.java

```java
package layer;

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.plaf.*;

/**
 * A frame with three text fields to set the background color.
 */
public class ColorFrame extends JFrame
{
    private JPanel panel;
    private JTextField redField;
    private JTextField greenField;
    private JTextField blueField;

    public ColorFrame()
    {
        panel = new JPanel();

        panel.add(new JLabel("Red:"));
        redField = new JTextField("255", 3);
        panel.add(redField);

        panel.add(new JLabel("Green:"));
        greenField = new JTextField("255", 3);
        panel.add(greenField);

        panel.add(new JLabel("Blue:"));
        blueField = new JTextField("255", 3);
        panel.add(blueField);

        LayerUI<JPanel> layerUI = new PanelLayer();
        JLayer<JPanel> layer = new JLayer<JPanel>(panel, layerUI);

        add(layer);
        pack();
    }

    class PanelLayer extends LayerUI<JPanel>
    {
        public void installUI(JComponent c)
        {
            super.installUI(c);
            ((JLayer<?>) c).setLayerEventMask(AWTEvent.KEY_EVENT_MASK | AWTEvent.FOCUS_EVENT_MASK);
        }

        public void uninstallUI(JComponent c)
        {
            ((JLayer<?>) c).setLayerEventMask(0);
            super.uninstallUI(c);
        }

        protected void processKeyEvent(KeyEvent e, JLayer<? extends JPanel> l)
        {
            l.repaint();
        }

        protected void processFocusEvent(FocusEvent e, JLayer<? extends JPanel> l)
        {
            if (e.getID() == FocusEvent.FOCUS_GAINED)
            {
                Component c = e.getComponent();
                c.setFont(getFont().deriveFont(Font.BOLD));
            }
            if (e.getID() == FocusEvent.FOCUS_LOST)
            {
                Component c = e.getComponent();
                c.setFont(getFont().deriveFont(Font.PLAIN));
            }
        }

        public void paint(Graphics g, JComponent c)
        {
            super.paint(g, c);

            Graphics2D g2 = (Graphics2D) g.create();
            g2.setComposite(AlphaComposite.getInstance(AlphaComposite.SRC_OVER, .3f));
            int red = Integer.parseInt(redField.getText().trim());
            int green = Integer.parseInt(greenField.getText().trim());
            int blue = Integer.parseInt(blueField.getText().trim());
            g2.setPaint(new Color(red, green, blue));
            g2.fillRect(0, 0, c.getWidth(), c.getHeight());
            g2.dispose();
        }
    }
}
```

| API | 描述 |
|---|---|
| `javax.swing.JLayer<V extends Component>` | 7 |
| `JLayer(V view, LayerUI<V> ui)` | 在给定视图上构造一个图层，将绘制和事件处理委托给 UI 对象。 |

**javax.swing.JLayer\<V extends Component\> 7** *（续）*

- `void setLayerEventMask(long layerEventMask)`  
  启用将所有匹配事件（发送到关联组件或其任何后代）发送到关联的 LayerUI。对于事件掩码，组合以下任意常量：  
  `COMPONENT_EVENT_MASK` `KEY_EVENT_MASK`  
  `FOCUS_EVENT_MASK` `MOUSE_EVENT_MASK`  
  `HIERARCHY_BOUNDS_EVENT_MASK` `MOUSE_MOTION_EVENT_MASK`  
  `HIERARCHY_EVENT_MASK` `MOUSE_WHEEL_EVENT_MASK`  
  `INPUT_METHOD_EVENT_MASK`  
  来自 AWTEvent 类。

**javax.swing.plaf.LayerUI\<V extends Component\> 7**

- `void installUI(JComponent c)`  
- `void uninstallUI(JComponent c)`  
  当组件 c 的 LayerUI 被安装或卸载时调用。覆盖此方法以设置或清除图层事件掩码。
- `void paint(Graphics g, JComponent c)`  
  当装饰组件被绘制时调用。覆盖此方法以调用 `super.paint` 并绘制装饰。
- `void processComponentEvent(ComponentEvent e, JLayer<? extends V> l)`  
- `void processFocusEvent(FocusEvent e, JLayer<? extends V> l)`  
- `void processHierarchyBoundsEvent(HierarchyEvent e, JLayer<? extends V> l)`  
- `void processHierarchyEvent(HierarchyEvent e, JLayer<? extends V> l)`  
- `void processInputMethodEvent(InputMethodEvent e, JLayer<? extends V> l)`  
- `void processKeyEvent(KeyEvent e, JLayer<? extends V> l)`  
- `void processMouseEvent(MouseEvent e, JLayer<? extends V> l)`  
- `void processMouseMotionEvent(MouseEvent e, JLayer<? extends V> l)`  
- `void processMouseWheelEvent(MouseWheelEvent e, JLayer<? extends V> l)`  
  当指定事件被发送到此 LayerUI 时调用。

现在你已经了解了如何使用 Swing 框架提供的复杂组件。在下一章中，我们将转向高级 AWT 问题：复杂绘图操作、图像处理、打印以及与原生窗口系统的接口。

## 第 11 章：高级 AWT

**本章内容**

- 11.1 渲染管线，第 766 页
- 11.2 形状，第 769 页
- 11.3 区域，第 786 页
- 11.4 笔画，第 788 页
- 11.5 绘制，第 797 页
- 11.6 坐标变换，第 799 页
- 11.7 裁剪，第 805 页
- 11.8 透明与合成，第 807 页
- 11.9 渲染提示，第 817 页
- 11.10 图像的读写器，第 823 页
- 11.11 图像处理，第 834 页
- 11.12 打印，第 851 页
- 11.13 剪贴板，第 887 页
- 11.14 拖放，第 903 页
- 11.15 平台集成，第 921 页

你可以使用 `Graphics` 类的方法创建简单的绘图。这些方法对于简单的小程序和应用程序来说已经足够，但当你需要创建复杂形状或需要对图形外观进行完全控制时，它们就力不从心了。Java 2D API 是一个更复杂的类库，你可以用它来生成高质量的绘图。在本章中，我们将对该 API 进行概述。

接下来，我们将转向打印主题，并展示如何在程序中实现打印功能。

我们将介绍两种在程序之间传输数据的技术：系统剪贴板和拖放机制。你可以使用这些技术在两个 Java 应用程序之间或在 Java 应用程序与原生程序之间传输数据。最后，我们介绍使 Java 应用程序更接近原生应用程序的技术，例如提供启动画面和系统托盘图标。

### 11.1 渲染管线

最初的 JDK 1.0 有一个非常简单的绘制形状的机制。你可以选择颜色和绘制模式，并调用 `Graphics` 类的方法，如 `drawRect` 或 `fillOval`。Java 2D API 支持更多选项。

- 你可以轻松生成各种各样的*形状*。
- 你可以控制*笔画*——即绘制形状边界的画笔。
- 你可以使用纯色、不同色调和重复图案来*填充*形状。
- 你可以使用*变换*来移动、缩放、旋转或拉伸形状。
- 你可以*裁剪*形状，将它们限制在任意区域内。
- 你可以选择*合成规则*来描述如何将新形状的像素与现有像素组合。
- 你可以提供*渲染提示*以在速度和绘制质量之间进行权衡。

要绘制一个形状，请执行以下步骤：

1. 获取一个 `Graphics2D` 类的对象。该类是 `Graphics` 类的子类。自从 Java SE 1.2 以来，`paint` 和 `paintComponent` 等方法会自动接收一个 `Graphics2D` 类的对象。只需使用强制转换，如下所示：

```java
public void paintComponent(Graphics g)
{
    Graphics2D g2 = (Graphics2D) g;
    . . .
}
```

2. 使用 `setRenderingHints` 方法设置*渲染提示*——速度和绘制质量之间的权衡。
