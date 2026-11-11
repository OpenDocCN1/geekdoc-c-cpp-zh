
## 代码清单 10.6 `mouse/MouseComponent.java`

```java
package mouse;

import java.awt.*;
import java.awt.event.*;
import java.awt.geom.*;
import java.util.*;
import javax.swing.*;

/**
 * A component with mouse operations for adding and removing
 * squares.
 */
public class MouseComponent extends JComponent
{
    private static final int DEFAULT_WIDTH = 300;
    private static final int DEFAULT_HEIGHT = 200;

    private static final int SIDELENGTH = 10;
    private ArrayList<Rectangle2D> squares;
    private Rectangle2D current; // the square containing the mouse cursor

    public MouseComponent()
    {
        squares = new ArrayList<>();
        current = null;

        addMouseListener(new MouseHandler());
        addMouseMotionListener(new MouseMotionHandler());
    }

    public Dimension getPreferredSize()
    {
        return new Dimension(DEFAULT_WIDTH, DEFAULT_HEIGHT);
    }

    public void paintComponent(Graphics g)
    {
        var g2 = (Graphics2D) g;

        // draw all squares
        for (Rectangle2D r : squares)
            g2.draw(r);
    }

    /**
     * Finds the first square containing a point.
     * @param p a point
     * @return the first square that contains p
     */
    public Rectangle2D find(Point2D p)
    {
        for (Rectangle2D r : squares)
        {
            if (r.contains(p)) return r;
        }
        return null;
    }

    /**
     * Adds a square to the collection.
     * @param p the center of the square
     */
    public void add(Point2D p)
    {
        double x = p.getX();
        double y = p.getY();

        current = new Rectangle2D.Double(x - SIDELENGTH / 2, y - SIDELENGTH / 2,
            SIDELENGTH, SIDELENGTH);
        squares.add(current);
        repaint();
    }

    /**
     * Removes a square from the collection.
     * @param s the square to remove
     */
    public void remove(Rectangle2D s)
    {
        if (s == null) return;
        if (s == current) current = null;
        squares.remove(s);
        repaint();
    }

    private class MouseHandler extends MouseAdapter
    {
        public void mousePressed(MouseEvent event)
        {
            // add a new square if the cursor isn't inside a square
            current = find(event.getPoint());
            if (current == null) add(event.getPoint());
        }

        public void mouseClicked(MouseEvent event)
        {
            // remove the current square if double clicked
            current = find(event.getPoint());
            if (current != null && event.getClickCount() >= 2)
                remove(current);
        }
    }

    private class MouseMotionHandler implements MouseMotionListener
    {
        public void mouseMoved(MouseEvent event)
        {
            // set the mouse cursor to cross hairs if it is inside a rectangle
            if (find(event.getPoint()) == null)
                setCursor(Cursor.getDefaultCursor());
            else
                setCursor(Cursor.getPredefinedCursor(Cursor.CROSSHAIR_CURSOR));
        }

        public void mouseDragged(MouseEvent event)
        {
            if (current != null)
            {
                int x = event.getX();
                int y = event.getY();

                // drag the current rectangle to center it at (x, y)
                current.setFrame(x - SIDELENGTH / 2, y - SIDELENGTH / 2, SIDELENGTH, SIDELENGTH);
                repaint();
            }
        }
    }
}
```

### java.awt.event.MouseEvent 1.1

- `int getX()`
- `int getY()`
- `Point getPoint()`
  
  返回事件发生点的 x（水平）和 y（垂直）坐标，从作为事件源的组件的左上角开始度量。
- `int getClickCount()`
  
  返回与此事件关联的连续鼠标单击次数。（“连续”的时间间隔取决于系统。）

### java.awt.Component 1.0

- `public void setCursor(Cursor cursor)` 1.1
  
  将光标图像设置为指定的光标。

## 10.4.7 AWT 事件层次结构

`EventObject` 类有一个子类 `AWTEvent`，它是所有 AWT 事件类的父类。[图 10.17](#) 展示了 AWT 事件的继承图。

![](img/0e7b74ef51a065c077b42cd87b362288_897_0.png)

图 10.17 AWT 事件类的继承图

一些 Swing 组件会生成更多事件类型的事件对象；这些对象直接扩展 `EventObject`，而不是 `AWTEvent`。

事件对象封装了事件源向其监听器传达的事件信息。必要时，你可以随后分析传递给监听器对象的事件对象，就像我们在按钮示例中使用 `getSource` 和 `getActionCommand` 方法所做的那样。

有些 AWT 事件类对 Java 程序员没有实际用途。例如，AWT 会将 `PaintEvent` 对象插入事件队列，但这些对象不会传递给监听器。Java 程序员不会监听绘制事件；相反，他们会重写 `paintComponent` 方法来控制重绘。AWT 还会生成一些只有系统程序员才需要的事件，用于为表意文字语言提供输入系统、自动化测试机器人等。

AWT 对*低层*事件和*语义*事件做了有用的区分。语义事件表达用户正在做什么，例如“单击那个按钮”；`ActionEvent` 就是一种语义事件。低层事件则是实现这一操作的事件。就按钮单击而言，这包括鼠标按下、一系列鼠标移动和鼠标释放（但仅当鼠标释放在按钮区域内时）。也可能是一次击键，即用户用 Tab 键选择按钮，然后用空格键激活它时发生。类似地，调整滚动条是语义事件，而拖动鼠标是低层事件。

以下是 `java.awt.event` 包中最常用的语义事件类：

- `ActionEvent`（用于按钮单击、菜单选择、选择列表项，或在文本字段中键入 Enter）
- `AdjustmentEvent`（用户调整了滚动条）
- `ItemEvent`（用户从一组复选框或列表项中做出选择）

常用的低层事件类有五个：

- `KeyEvent`（按下或释放了某个键）
- `MouseEvent`（鼠标按钮被按下、释放、移动或拖动）
- `MouseWheelEvent`（鼠标滚轮被旋转）
- `FocusEvent`（组件获得或失去焦点）
- `WindowEvent`（窗口状态改变）

表 10.4 列出了最重要的 AWT 监听器接口、事件和事件源。

### 表 10.4 事件处理摘要

| 接口 | 方法 | 参数/访问器 | 生成事件的组件 |
|---|---|---|---|
| `ActionListener` | `actionPerformed` | `ActionEvent`<br>• `getActionCommand`<br>• `getModifiers` | `AbstractButton`<br>`JComboBox`<br>`JTextField`<br>`Timer` |
| `AdjustmentListener` | `adjustmentValueChanged` | `AdjustmentEvent`<br>• `getAdjustable`<br>• `getAdjustmentType`<br>• `getValue` | `JScrollbar` |
| `ItemListener` | `itemStateChanged` | `ItemEvent`<br>• `getItem`<br>• `getItemSelectable`<br>• `getStateChange` | `AbstractButton`<br>`JComboBox` |
| `FocusListener` | `focusGained`<br>`focusLost` | `FocusEvent`<br>• `isTemporary` | `Component` |
| `KeyListener` | `keyPressed`<br>`keyReleased`<br>`keyTyped` | `KeyEvent`<br>• `getKeyChar`<br>• `getKeyCode`<br>• `getKeyModifiersText`<br>• `getKeyText`<br>• `isActionKey` | `Component` |
| `MouseListener` | `mousePressed`<br>`mouseReleased`<br>`mouseEntered`<br>`mouseExited`<br>`mouseClicked` | `MouseEvent`<br>• `getClickCount`<br>• `getX`<br>• `getY`<br>• `getPoint`<br>• `translatePoint` | `Component` |
| `MouseMotionListener` | `mouseDragged`<br>`mouseMoved` | `MouseEvent` | `Component` |
| `MouseWheelListener` | `mouseWheelMoved` | `MouseWheelEvent`<br>• `getWheelRotation`<br>• `getScrollAmount` | `Component` |
| `WindowListener` | `windowClosing`<br>`windowOpened`<br>`windowIconified`<br>`windowDeiconified`<br>`windowClosed`<br>`windowActivated`<br>`windowDeactivated` | `WindowEvent`<br>• `getWindow` | `Window` |
| `WindowFocusListener` | `windowGainedFocus`<br>`windowLostFocus` | `WindowEvent`<br>• `getOppositeWindow` | `Window` |
| `WindowStateListener` | `windowStateChanged` | `WindowEvent`<br>• `getOldState`<br>• `getNewState` | `Window` |

