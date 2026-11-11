

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_796_0.png)

**图 11.60** 跨平台打印对话框

> **注意：** 在 JDK 1.4 之前，打印系统使用宿主平台的原生打印和页面设置对话框。要显示原生打印对话框，请调用不带参数的 `printDialog` 方法。（无法在属性集中收集用户设置。）

在打印过程中，`PrinterJob` 类的 `print` 方法会重复调用与该任务关联的 `Printable` 对象的 `print` 方法。

由于打印任务不知道你要打印多少页，它只会持续调用 `print` 方法。只要 `print` 方法返回 `Printable.PAGE_EXISTS` 值，打印任务就会继续生成页面。当 `print` 方法返回 `Printable.NO_SUCH_PAGE` 时，打印任务停止。

> **警告：** 打印任务传递给 `print` 方法的页码从第 0 页开始。

因此，在打印输出完成之前，打印任务无法获得准确的页数。因此，打印对话框无法显示正确的页面范围，而是显示“第 1 页到第 1 页”。在下一节中，你将看到如何通过向打印任务提供 `Book` 对象来避免这个瑕疵。

在打印过程中，打印任务会重复调用 `Printable` 对象的 `print` 方法。打印任务可能会对*同一页*进行多次调用。因此，你不应在 `print` 方法中统计页数，而应始终依赖页码参数。打印任务对同一页重复调用 `print` 方法是有充分理由的。某些打印机，尤其是针式打印机和喷墨打印机，使用 `banding`。它们一次打印一个条带，进纸，然后再打印下一个条带。即使是每次打印一整页的激光打印机，打印任务也可能使用 banding——这为打印任务提供了一种管理后台打印文件大小的方法。

如果打印任务需要 `Printable` 对象来打印一个条带，它会将 `Graphics` 上下文的裁剪区域设置为所请求的条带，然后调用 `print` 方法。其绘制操作会针对条带矩形进行裁剪，只有出现在条带中的绘制元素才会被渲染。你的 `print` 方法不必意识到这一过程，但有一个注意事项：它*不应*干扰裁剪区域。

> **警告：** 你的 `print` 方法得到的 `Graphics` 对象也会根据页面边距进行裁剪。如果你替换了裁剪区域，可能会在边距之外绘图。尤其是在打印机图形上下文中，必须遵守裁剪区域。请调用 `clip`，*而不是* `setClip`，以进一步限制裁剪区域。如果必须移除裁剪区域，请确保在 `print` 方法开头调用 `getClip` 并恢复该裁剪区域。

`print` 方法的 `PageFormat` 参数包含有关所打印页面的信息。`getWidth` 和 `getHeight` 方法返回纸张尺寸，以*点*为单位。（1 点等于 1/72 英寸；1 英寸等于 25.4 毫米。）例如，A4 纸约为 595 × 842 点，美国信纸为 612 × 792 点。

点是美国印刷行业常用的度量单位。令世界其他地方大为懊恼的是，这个打印包使用点作为单位。这有两个目的：纸张尺寸和纸张边距以*点*为单位，并且点是所有打印图形上下文的默认单位。你可以在本节末尾的示例程序中验证这一点。该程序打印两行间隔为 72 个单位的文本。运行示例程序并测量基线之间的距离；它们恰好相隔 1 英寸或 25.4 毫米。

`PageFormat` 类的 `getWidth` 和 `getHeight` 方法给出完整的纸张尺寸。并非所有纸张区域都可打印。用户通常会选择边距，即使他们不选择，打印机也需要以某种方式夹住要打印的纸张，因此边缘周围会有一小块不可打印区域。

`getImageableWidth` 和 `getImageableHeight` 方法告诉你实际可以填充的区域的尺寸。然而，边距不一定是对称的，因此你还需要知道可成像区域的左上角（见图 11.61），可以通过 `getImageableX` 和 `getImageableY` 方法获取。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_798_0.png)

**图 11.61** 页面格式度量

> **提示：** 在 `print` 方法中收到的图形上下文会被裁剪以排除边距，但坐标系的原点仍然是纸张的左上角。将坐标系平移到可成像区域的左上角是合理的。只需在 `print` 方法开头使用
>
> ```java
> g.translate(pageFormat.getImageableX(), pageFormat.getImageableY());
> ```

如果你希望用户选择页面边距设置，或者在不设置其他打印属性的情况下切换纵向和横向，请调用 `PrinterJob` 类的 `pageDialog` 方法：

```java
PageFormat format = job.pageDialog(attributes);
```

> **注意：** 打印对话框的其中一个选项卡包含页面设置对话框（见图 11.62）。你可能仍然希望让用户可以在打印前设置页面格式，尤其是当你的程序提供“所见即所得”的待打印页面显示时。`pageDialog` 方法返回用户设置的 `PageFormat` 对象视图。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_799_0.png)

**图 11.62** 跨平台页面设置对话框

清单 11.23 和 11.24 中的程序展示了如何在屏幕和打印页面上渲染同一组形状。JPanel 的一个子类实现了 Printable 接口。`paintComponent` 和 `print` 方法都调用同一个方法来执行实际的绘制。

```java
class PrintPanel extends JPanel implements Printable
{
    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        var g2 = (Graphics2D) g;
        drawPage(g2);
    }

    public int print(Graphics g, PageFormat pf, int page) throws PrinterException
    {
        if (page >= 1) return Printable.NO_SUCH_PAGE;
        var g2 = (Graphics2D) g;
        g2.translate(pf.getImageableX(), pf.getImageableY());
        drawPage(g2);
        return Printable.PAGE_EXISTS;
    }

    public void drawPage(Graphics2D g2)
    {
        // shared drawing code goes here
        . . .
    }
    . . .
}
```

此示例显示并打印图 11.50 中所示的图像——即“Hello, World”消息的轮廓，用作线条图案的裁剪区域。

单击 Print 按钮开始打印，或单击 Page setup 按钮打开页面设置对话框。清单 11.23 显示了代码。

> **注意：** 要显示原生页面设置对话框，请将默认的 PageFormat 对象传递给 pageDialog 方法。该方法会克隆该对象，根据用户在对话框中的选择对其进行修改，并返回克隆后的对象。
>
> ```java
> PageFormat defaultFormat = printJob.defaultPage();
> PageFormat selectedFormat = printJob.pageDialog(defaultFormat);
> ```

## **清单 11.23** print/PrintTestFrame.java

```java
1 package print;
2
3 import java.awt.*;
4 import java.awt.print.*;
5
6 import javax.print.attribute.*;
7 import javax.swing.*;
8
9 /**
10 * This frame shows a panel with 2D graphics and buttons to print the graphics and to set up
11 * the page format.
12 */
13 public class PrintTestFrame extends JFrame
14 {
15     private PrintComponent canvas;
16     private PrintRequestAttributeSet attributes;
17
18     public PrintTestFrame()
19     {
        canvas = new PrintComponent();
        add(canvas, BorderLayout.CENTER);

        attributes = new HashPrintRequestAttributeSet();

        var buttonPanel = new JPanel();
        var printButton = new JButton("Print");
        buttonPanel.add(printButton);
        printButton.addActionListener(event ->
        {
            try
            {
                PrinterJob job = PrinterJob.getPrinterJob();
                job.setPrintable(canvas);
                if (job.printDialog(attributes)) job.print(attributes);
            }
            catch (PrinterException ex)
            {
                JOptionPane.showMessageDialog(PrintTestFrame.this, ex);
            }
        });

        var pageSetupButton = new JButton("Page setup");
        buttonPanel.add(pageSetupButton);
        pageSetupButton.addActionListener(event ->
        {
            PrinterJob job = PrinterJob.getPrinterJob();
            job.pageDialog(attributes);
        });

        add(buttonPanel, BorderLayout.NORTH);
        pack();
    }
}
```

## **清单 11.24** `print/PrintComponent.java`

```java
package print;

import java.awt.*;
import java.awt.font.*;
import java.awt.geom.*;
import java.awt.print.*;
import javax.swing.*;

/**
 * This component generates a 2D graphics image for screen display and printing.
 */
```

（续）

