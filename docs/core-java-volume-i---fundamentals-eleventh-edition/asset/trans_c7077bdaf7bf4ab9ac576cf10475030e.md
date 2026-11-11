
该处理器扩展了 `StreamHandler` 类，并安装一个流，其写入方法将流输出显示在文本区域中。

```java
class WindowHandler extends StreamHandler
{
    public WindowHandler()
    {
        . . .
        var output = new JTextArea();

        setOutputStream(new
            OutputStream()
            {
                public void write(int b) { } // not called
                public void write(byte[] b, int off, int len)
                {
                    output.append(new String(b, off, len));
                }
            });
    }
    . . .
}
```

这种方法只有一个问题——处理器会缓冲记录，并且仅在缓冲区满时才将它们写入流。因此，我们重写 publish 方法，以便在每条记录之后刷新缓冲区：

```java
class WindowHandler extends StreamHandler
{
    . . .

    public void publish(LogRecord record)
    {
        super.publish(record);
        flush();
    }
}
```

如果要编写更奇特的流处理器，请扩展 Handler 类并定义 publish、flush 和 close 方法。

## 7.5.6 过滤器

默认情况下，记录会根据其日志级别进行过滤。每个日志记录器和处理器都可以有一个可选过滤器来执行额外过滤。要定义过滤器，请实现 Filter 接口并定义以下方法

```java
boolean isLoggable(LogRecord record)
```

使用你希望的任何标准分析日志记录，并对应该包含在日志中的记录返回 true。例如，某个特定过滤器可能只关心 entering 和 exiting 方法生成的消息。然后，该过滤器应调用 `record.getMessage()` 并检查它是否以 `ENTRY` 或 `RETURN` 开头。

要将过滤器安装到日志记录器或处理器中，只需调用 `setFilter` 方法。请注意，一次最多只能有一个过滤器。

## 7.5.7 格式化器

ConsoleHandler 和 FileHandler 类以文本和 XML 格式发出日志记录。不过，你也可以定义自己的格式。你需要扩展 Formatter 类并重写以下方法

```java
String format(LogRecord record)
```

以你喜欢的任何方式格式化记录中的信息，并返回结果字符串。在你的 format 方法中，你可能想调用以下方法

```java
String formatMessage(LogRecord record)
```

该方法格式化记录的消息部分，替换参数并应用本地化。

许多文件格式（例如 XML）需要包围格式化记录的头部分和尾部分。为此，请重写以下方法

```java
String getHead(Handler h)
String getTail(Handler h)
```

最后，调用 `setFormatter` 方法将格式化器安装到处理器中。

## 7.5.8 日志记录配方

日志记录有如此多的选项，很容易忽略基础知识。以下配方总结了最常见的操作。

- 1. 对于简单的应用程序，选择一个日志记录器。最好给该日志记录器取与主应用程序包相同的名称，例如 `com.mycompany.myprog`。你始终可以通过调用 `Logger logger = Logger.getLogger("com.mycompany.myprog");` 来获取该日志记录器。

   为方便起见，对于日志活动较多的类，你可能想添加静态字段 `private static final Logger logger = Logger.getLogger("com.mycompany.myprog");`。

```java
Logger logger = Logger.getLogger("com.mycompany.myprog");
```

```java
private static final Logger logger = Logger.getLogger("com.mycompany.myprog");
```

## 清单 7.2 `logging/LoggingImageViewer.java`

```java
package logging;

import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.util.logging.*;
import javax.swing.*;

/**
 * A modification of the image viewer program that logs various events.
 * @version 1.03 2015-08-20
 * @author Cay Horstmann
 */
public class LoggingImageViewer
{
   public static void main(String[] args)
   {
      if (System.getProperty("java.util.logging.config.class") == null
            && System.getProperty("java.util.logging.config.file") == null)
      {
         try
         {
            Logger.getLogger("com.horstmann.corejava").setLevel(Level.ALL);
            final int LOG_ROTATION_COUNT = 10;
            var handler = new FileHandler("%h/logging/ImageViewer.log", 0, LOG_ROTATION_COUNT);
            Logger.getLogger("com.horstmann.corejava").addHandler(handler);
         }
         catch (IOException e)
         {
            Logger.getLogger("com.horstmann.corejava").log(Level.SEVERE,
               "Can't create log file handler", e);
         }
      }

      EventQueue.invokeLater(() ->
      {
         var windowHandler = new WindowHandler();
         windowHandler.setLevel(Level.ALL);
         Logger.getLogger("com.horstmann.corejava").addHandler(windowHandler);

         var frame = new ImageViewerFrame();
         frame.setTitle("LoggingImageViewer");
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         Logger.getLogger("com.horstmann.corejava").fine("Showing frame");
         frame.setVisible(true);
      });
   }
}

/**
 * The frame that shows the image.
 */
class ImageViewerFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 400;

   private JLabel label;
   private static final Logger logger = Logger.getLogger("com.horstmann.corejava");

   public ImageViewerFrame()
   {
      logger.entering("ImageViewerFrame", "<init>");
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // Set up menu bar
      var menuBar = new JMenuBar();
      setJMenuBar(menuBar);

      var menu = new JMenu("File");
      menuBar.add(menu);

      var openItem = new JMenuItem("Open");
      menu.add(openItem);
      openItem.addActionListener(new FileOpenListener());

      var exitItem = new JMenuItem("Exit");
      menu.add(exitItem);
      exitItem.addActionListener(new ActionListener()
         {
            public void actionPerformed(ActionEvent event)
            {
               logger.fine("Exiting.");
               System.exit(0);
            }
         });

      // use a label to display the images
      label = new JLabel();
      add(label);
      logger.exiting("ImageViewerFrame", "<init>");
   }

   private class FileOpenListener implements ActionListener
   {
      public void actionPerformed(ActionEvent event)
      {
         logger.entering("ImageViewerFrame.FileOpenListener", "actionPerformed", event);

         // set up file chooser
         var chooser = new JFileChooser();
         chooser.setCurrentDirectory(new File("."));

         // accept all files ending with .gif
         chooser.setFileFilter(new javax.swing.filechooser.FileFilter()
         {
            public boolean accept(File f)
            {
               return f.getName().toLowerCase().endsWith(".gif") || f.isDirectory();
            }

            public String getDescription()
            {
               return "GIF Images";
            }
         });

         // show file chooser dialog
         int r = chooser.showOpenDialog(ImageViewerFrame.this);

         // if image file accepted, set it as icon of the label
         if (r == JFileChooser.APPROVE_OPTION)
         {
            String name = chooser.getSelectedFile().getPath();
            logger.log(Level.FINE, "Reading file {0}", name);
            label.setIcon(new ImageIcon(name));
         }
         else logger.fine("File open dialog canceled.");
         logger.exiting("ImageViewerFrame.FileOpenListener", "actionPerformed");
      }
   }
}

/**
 * A handler for displaying log records in a window.
 */
class WindowHandler extends StreamHandler
{
   private JFrame frame;

   public WindowHandler()
   {
      frame = new JFrame();
      var output = new JTextArea();
      output.setEditable(false);
      frame.setSize(200, 200);
      frame.add(new JScrollPane(output));
      frame.setFocusableWindowState(false);
      frame.setVisible(true);
      setOutputStream(new OutputStream()
      {
         public void write(int b)
         {
            // not called
         }

         public void write(byte[] b, int off, int len)
         {
            output.append(new String(b, off, len));
         }
      });
   }

   public void publish(LogRecord record)
   {
      if (!frame.isVisible()) return;
      super.publish(record);
      flush();
   }
}
```

## **java.util.logging.Logger** 1.4

- `Logger getLogger(String loggerName)`
- `Logger getLogger(String loggerName, String bundleName)`

获取具有给定名称的日志记录器。如果该日志记录器不存在，则会创建它。本地化消息位于名称为 bundleName 的资源包中。

