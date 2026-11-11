
## 清单 10.31（续）

```java
iframe.addVetoableChangeListener(event ->
{
    String name = event.getPropertyName();
    Object value = event.getNewValue();

    // we only want to check attempts to close a frame
    if (name.equals("closed") && value.equals(true))
    {
        // ask user if it is ok to close
        int result = JOptionPane.showInternalConfirmDialog(iframe, "OK to close?",
            "Select an Option", JOptionPane.YES_NO_OPTION);

        // if the user doesn't agree, veto the close
        if (result != JOptionPane.YES_OPTION)
            throw new PropertyVetoException("User canceled close", event);
    }
});

// position frame
int width = desktop.getWidth() / 2;
int height = desktop.getHeight() / 2;
iframe.reshape(nextFrameX, nextFrameY, width, height);

iframe.show();

// select the frame--might be vetoed
try
{
    iframe.setSelected(true);
}
catch (PropertyVetoException ex)
{
}

frameDistance = iframe.getHeight() - iframe.getContentPane().getHeight();

// compute placement for next frame

nextFrameX += frameDistance;
nextFrameY += frameDistance;
if (nextFrameX + width > desktop.getWidth()) nextFrameX = 0;
if (nextFrameY + height > desktop.getHeight()) nextFrameY = 0;
}

/**
 * Cascades the noniconified internal frames of the desktop.
 */
public void cascadeWindows()
{
    int x = 0;
    int y = 0;
    int width = desktop.getWidth() / 2;
    int height = desktop.getHeight() / 2;

    for (JInternalFrame frame : desktop.getAllFrames())
    {
        if (!frame.isIcon())
        {
            try
            {
                // try to make maximized frames resizable; this might be vetoed
                frame.setMaximum(false);
                frame.reshape(x, y, width, height);

                x += frameDistance;
                y += frameDistance;
                // wrap around the desktop edge
                if (x + width > desktop.getWidth()) x = 0;
                if (y + height > desktop.getHeight()) y = 0;
            }
            catch (PropertyVetoException ex)
            {
            }
        }
    }
}

/**
 * Tiles the noniconified internal frames of the desktop.
 */
public void tileWindows()
{
    // count frames that aren't iconized
    int frameCount = 0;
    for (JInternalFrame frame : desktop.getAllFrames())
        if (!frame.isIcon()) frameCount++;
    if (frameCount == 0) return;

    int rows = (int) Math.sqrt(frameCount);
    int cols = frameCount / rows;
    int extra = frameCount % rows;
    // number of columns with an extra row

    int width = desktop.getWidth() / cols;
    int height = desktop.getHeight() / rows;
    int r = 0;
    int c = 0;
    for (JInternalFrame frame : desktop.getAllFrames())
    {
        if (!frame.isIcon())
        {
            try
            {
                frame.setMaximum(false);
                frame.reshape(c * width, r * height, width, height);
                r++;
                if (r == rows)
                {
                    r = 0;
                    c++;
                    if (c == cols - extra)
                    {
                        // start adding an extra row
                        rows++;
                        height = desktop.getHeight() / rows;
                    }
                }
            }
            catch (PropertyVetoException ex)
            {
            }
        }
    }
}

/**
 * Brings the next noniconified internal frame to the front.
 */
public void selectNextWindow()
{
    JInternalFrame[] frames = desktop.getAllFrames();
    for (int i = 0; i < frames.length; i++)
    {
        if (frames[i].isSelected())
        {
            // find next frame that isn't an icon and can be selected
            int next = (i + 1) % frames.length;
            while (next != i)
            {
                if (!frames[next].isIcon())
                {
                    try
                    {
                        // all other frames are icons or veto selection
                        frames[next].setSelected(true);
                        frames[next].toFront();
                        frames[i].toBack();
                        return;
                    }
                    catch (PropertyVetoException ex)
                    {
                    }
                }
                next = (next + 1) % frames.length;
            }
        }
    }
}
```

- **javax.swing.JDesktopPane 1.2**
  - `JInternalFrame[] getAllFrames()` — 获取此桌面窗格中的所有内部框架。
  - `void setDragMode(int mode)` — 将拖动模式设置为实时拖动模式或轮廓拖动模式。
    - *参数：* `mode` — `JDesktopPane.LIVE_DRAG_MODE` 或 `JDesktopPane.OUTLINE_DRAG_MODE` 之一

- **javax.swing.JInternalFrame 1.2**
  - `JInternalFrame()`
  - `JInternalFrame(String title)`
  - `JInternalFrame(String title, boolean resizable)`
  - `JInternalFrame(String title, boolean resizable, boolean closable)`
  - `JInternalFrame(String title, boolean resizable, boolean closable, boolean maximizable)`
  - `JInternalFrame(String title, boolean resizable, boolean closable, boolean maximizable, boolean iconifiable)`
  - 构造一个新的内部框架。
  - *参数：*
    - `title` — 标题栏中显示的字符串
    - `resizable` — 如果框架可以调整大小，则为 true
    - `closable` — 如果框架可以关闭，则为 true
    - `maximizable` — 如果框架可以最大化，则为 true
    - `iconifiable` — 如果框架可以图标化，则为 true

**javax.swing.JInternalFrame 1.2（续）**

| API | 描述 |
|---|---|
| `JDesktopPane getDesktopPane()` | 获取此内部框架的桌面窗格。 |
| `Icon getFrameIcon()`<br>`void setFrameIcon(Icon anIcon)` | 获取或设置标题栏中显示的框架图标。 |
| `boolean isVisible()`<br>`void setVisible(boolean b)` | 获取或设置“可见”属性。 |
| `void show()` | 使此内部框架可见，并将其置于最前面。 |

**javax.swing.JComponent 1.2**

| API | 描述 |
|---|---|
| `void addVetoableChangeListener(VetoableChangeListener listener)` | 添加一个可否决更改监听器，当尝试更改受约束属性时会通知该监听器。 |

**java.beans.VetoableChangeListener 1.1**

| API | 描述 |
|---|---|
| `void vetoableChange(PropertyChangeEvent event)` | 当受约束属性的 set 方法通知可否决更改监听器时调用。 |

**java.beans.PropertyChangeEvent 1.1**

| API | 描述 |
|---|---|
| `String getPropertyName()` | 返回即将更改的属性的名称。 |
| `Object getNewValue()` | 返回该属性的建议新值。 |

**java.beans.PropertyVetoException 1.1**

- `PropertyVetoException(String reason, PropertyChangeEvent event)` 构造一个属性否决异常。
- *参数：*
  - `reason` — 否决原因
  - `event` — 被否决的事件

## 10.6.4 层

Java SE 1.7 引入了一项功能，允许你在另一个组件之上放置一个层。你可以在该层上绘制，并监听底层组件的事件。你可以使用层为用户界面添加视觉提示。例如，你可以装饰当前输入、无效输入或禁用组件。

JLayer 类将组件与负责绘制和事件处理的 LayerUI 对象关联起来。LayerUI 类有一个类型参数，必须与关联的组件匹配。例如，这里我们向 JPanel 添加一个层：

```java
JPanel panel = new JPanel();
LayerUI<JPanel> layerUI = new PanelLayerUI();
JLayer<JPanel> layer = new JLayer(panel, layerUI);
frame.add(layer);
```

请注意，添加到父容器中的是层，而不是面板。这里，PanelLayerUI 是一个子类：

```java
class PanelLayerUI extends LayerUI<JPanel>
{
    public void paint(Graphics g, JComponent c)
    {
        . . .
    }
    . . .
}
```

在 paint 方法中，你可以绘制任何你想要的内容。请确保调用 super.paint 来绘制组件。这里，我们在整个组件上绘制一种透明颜色：

```java
public void paint(Graphics g, JComponent c)
{
    super.paint(g, c);

    Graphics2D g2 = (Graphics2D) g.create();
    g2.setComposite(AlphaComposite.getInstance(AlphaComposite.SRC_OVER, .3f));
    g2.setPaint(Color.RED);
    g2.fillRect(0, 0, c.getWidth(), c.getHeight());
}
```

