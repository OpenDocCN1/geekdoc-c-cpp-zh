
来计算分页位置和页数。你可以保留布局信息，以便在打印过程中随时使用。

你必须防范用户更改页面格式的可能性。如果发生这种情况，即使你想打印的信息没有变化，也必须重新计算布局。

代码清单 11.13 展示了如何生成多页打印输出。该程序用非常大的字符在多页上打印一条消息（见图 11.35）。然后你可以裁掉页边距，并把各页粘在一起组成横幅。

![](img/7dd923a566750151a3aab0dacd0cdaa5_883_0.png)

**图 11.35** 横幅

`Banner` 类的 `layoutPages` 方法计算布局。我们首先用 72 磅字体对消息字符串进行布局。然后计算所得字符串的高度，并将其与页面的可成像高度进行比较。我们根据这两个测量值推导出缩放因子。打印字符串时，我们按该缩放因子将其放大。

> **注意：** 要精确布局信息，通常需要访问打印机的图形上下文。不幸的是，在实际开始打印之前无法获得该图形上下文。在示例程序中，我们确实只能凑合使用屏幕图形上下文，并希望屏幕和打印机的字体度量相匹配。

`Banner` 类的 `getPageCount` 方法首先调用 `layout` 方法。然后它放大字符串的宽度，并将其除以每页的可成像宽度。商向上取整到下一个整数，就是页数。

听起来打印横幅可能很困难，因为字符可能会跨多页断开。然而，得益于 Java 2D API 的强大功能，这根本不是问题。当请求某一特定页面时，我们只需使用 `Graphics2D` 类的 `translate` 方法将字符串的左上角向左移动。然后，我们设置一个等于当前页面的裁剪矩形（见图 11.36）。最后，我们使用布局方法计算出的缩放因子缩放图形上下文。

![](img/7dd923a566750151a3aab0dacd0cdaa5_884_0.png)

**图 11.36** 打印横幅的一页

这个示例展示了变换的强大功能。绘图代码保持简单，而变换完成将绘图放置到适当位置的所有工作。最后，裁剪区域切掉图像中落在页面之外的部分。在下一节中，你将看到变换的另一个引人注目的用途——显示打印预览。

## 11.12.3 打印预览

大多数专业程序都有打印预览机制，让你在屏幕上查看页面，这样就不会把纸浪费在你不喜欢的打印输出上。Java 平台的打印类不提供标准的“打印预览”对话框，但设计自己的对话框很容易（见图 11.37）。本节将展示如何实现。代码清单 11.14 中的 `PrintPreviewDialog` 类是完全通用的——你可以复用它来预览任何类型的打印输出。

要构造 `PrintPreviewDialog`，请提供 `Printable` 或 `Book`，以及一个 `PageFormat` 对象。该对话框包含一个 `PrintPreviewCanvas`（见代码清单 11.15）。当你使用 Next 和 Previous 按钮翻页时，`paintComponent` 方法会为所请求的页面调用 `Printable` 对象的 `print` 方法。

通常，`print` 方法在打印机图形上下文上绘制页面内容。但是，我们提供屏幕图形上下文，并对其进行适当缩放，使整个打印页面适合一个小屏幕矩形。

![](img/7dd923a566750151a3aab0dacd0cdaa5_885_0.png)

**图 11.37** 打印预览对话框，显示一个横幅页面

```java
float xoff = . . . ; // left of page
float yoff = . . . ; // top of page
float scale = . . . ; // to fit printed page onto screen
g2.translate(xoff, yoff);
g2.scale(scale, scale);
Printable printable = book.getPrintable(currentPage);
printable.print(g2, pageFormat, currentPage);
```

`print` 方法从不知道它实际上并没有生成打印页面。它只是绘制到图形上下文上，在屏幕上生成一个微缩的打印预览。这有力地展示了 Java 2D 成像模型的能力。

代码清单 11.12 包含横幅打印程序的代码。在文本字段中输入“Hello, World!”，查看打印预览，然后打印横幅。

### 代码清单 11.12 book/BookTestFrame.java
*（续）*
```java
package book;

import java.awt.*;
import java.awt.print.*;
import javax.print.attribute.*;
import javax.swing.*;

/**
 * This frame has a text field for the banner text and buttons for printing, page setup, and print
 * preview.
 */
public class BookTestFrame extends JFrame
{
    private JTextField text;
    private PageFormat pageFormat;
    private PrintRequestAttributeSet attributes;

    public BookTestFrame()
    {
        text = new JTextField();
        add(text, BorderLayout.NORTH);

        attributes = new HashPrintRequestAttributeSet();

        JPanel buttonPanel = new JPanel();

        JButton printButton = new JButton("Print");
        buttonPanel.add(printButton);
        printButton.addActionListener(event ->
        {
            try
            {
                PrinterJob job = PrinterJob.getPrinterJob();
                job.setPageable(makeBook());
                if (job.printDialog(attributes))
                {
                    job.print(attributes);
                }
            }
            catch (PrinterException e)
            {
                JOptionPane.showMessageDialog(BookTestFrame.this, e);
            }
        });

        JButton pageSetupButton = new JButton("Page setup");
        buttonPanel.add(pageSetupButton);
        pageSetupButton.addActionListener(event ->
        {
            PrinterJob job = PrinterJob.getPrinterJob();
            pageFormat = job.pageDialog(attributes);
        });
55 JButton printPreviewButton = new JButton("Print preview");
56 buttonPanel.add(printPreviewButton);
57 printPreviewButton.addActionListener(event ->
58 {
59     PrintPreviewDialog dialog = new PrintPreviewDialog(makeBook());
60     dialog.setVisible(true);
61 });
62
63 add(buttonPanel, BorderLayout.SOUTH);
64 pack();
65 }
66
67 /**
68  * Makes a book that contains a cover page and the pages for the banner.
69  */
70 public Book makeBook()
71 {
72     if (pageFormat == null)
73     {
74         PrinterJob job = PrinterJob.getPrinterJob();
75         pageFormat = job.defaultPage();
76     }
77     Book book = new Book();
78     String message = text.getText();
79     Banner banner = new Banner(message);
80     int pageCount = banner.getPageCount((Graphics2D) getGraphics(), pageFormat);
81     book.append(new CoverPage(message + " (" + pageCount + " pages)"), pageFormat);
82     book.append(banner, pageFormat, pageCount);
83     return book;
84 }
85 }
```

### 代码清单 11.13 book/Banner.java
*（续）*
```java
1 package book;
2
3 import java.awt.*;
4 import java.awt.font.*;
5 import java.awt.geom.*;
6 import java.awt.print.*;
7
8 /**
9  * A banner that prints a text string on multiple pages.
10  */
11 public class Banner implements Printable
12 {
13     private String message;
14     private double scale;

/**
 * Constructs a banner.
 * @param m the message string
 */
public Banner(String m)
{
    message = m;
}

/**
 * Gets the page count of this section.
 * @param g2 the graphics context
 * @param pf the page format
 * @return the number of pages needed
 */
public int getPageCount(Graphics2D g2, PageFormat pf)
{
    if (message.equals("")) return 0;
    FontRenderContext context = g2.getFontRenderContext();
    Font f = new Font("Serif", Font.PLAIN, 72);
    Rectangle2D bounds = f.getStringBounds(message, context);
    scale = pf.getImageableHeight() / bounds.getHeight();
    double width = scale * bounds.getWidth();
    int pages = (int) Math.ceil(width / pf.getImageableWidth());
    return pages;
}

public int print(Graphics g, PageFormat pf, int page) throws PrinterException
{
    Graphics2D g2 = (Graphics2D) g;
    if (page > getPageCount(g2, pf)) return Printable.NO_SUCH_PAGE;
    g2.translate(pf.getImageableX(), pf.getImageableY());

    drawPage(g2, pf, page);
    return Printable.PAGE_EXISTS;
}

public void drawPage(Graphics2D g2, PageFormat pf, int page)
{
    if (message.equals("")) return;
    page--; // account for cover page

    drawCropMarks(g2, pf);
    g2.clip(new Rectangle2D.Double(0, 0, pf.getImageableWidth(), pf.getImageableHeight()));
    g2.translate(-page * pf.getImageableWidth(), 0);
    g2.scale(scale, scale);
    FontRenderContext context = g2.getFontRenderContext();
```
