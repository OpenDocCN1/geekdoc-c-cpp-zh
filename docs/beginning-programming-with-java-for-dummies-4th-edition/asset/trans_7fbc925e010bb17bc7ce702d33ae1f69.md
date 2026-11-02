
回到第 17 章的清单 17-3 中，我用以下行创建了 Purchase 类的一个实例

```
Purchase onePurchase = new Purchase();
```

所以在清单 20-1 中，我做了类似的事情。我用以下几行创建了 JFrame、ImageIcon 和 JLabel 类的实例：

```
JFrame frame = new JFrame();
ImageIcon icon = new ImageIcon("androidBook.jpg");
JLabel label = new JLabel(icon);
```

以下是关于这些行的一些八卦：

JFrame 就像一个窗口（只是它叫做 JFrame，而不是“窗口”）。在清单 20-1 中，该行

```
JFrame frame = new JFrame();
```

创建了一个 JFrame 对象，但这一行不会在任何地方显示该 JFrame 对象。（显示在代码后面的部分进行。）

ImageIcon 对象是一张图片。在程序项目目录的根目录下，我有一个名为 androidBook.jpg 的文件。该文件包含图 20-1 所示的图片。所以在清单 20-1 中，该行

```
ImageIcon icon = new ImageIcon("androidBook.jpg");
```

创建了一个 ImageIcon 对象——一个包含 androidBook.jpg 图片的图标。

出于我永远无法理解的原因，在运行清单 20-1 时，你可能不想使用我的 androidBook.jpg 图像文件。你可以用几乎任何 .gif、.jpg 或 .png 文件替换我的（漂亮的）Android 书籍封面图像。要这样做，请将你自己的图像文件拖到 Eclipse 的 Package Explorer 中。（将其拖到此示例项目文件夹的根目录。）然后，在 Eclipse 编辑器中，将名称 androidBook.jpg 改为你自己的图像文件的名称。就这样！

我需要一个放置图标的地方。我可以把它放在一个叫做 JLabel 的东西上。所以在清单 20-1 中，该行

```
JLabel label = new JLabel(icon);
```

创建了一个 JLabel 对象，并将 androidBook.jpg 图标放在新标签的表面上。

如果你阅读了之前的要点，你可能会产生错误的印象。措辞可能暗示每个组件（JFrame、ImageIcon、JLabel 等）的使用是你已知的知识的逻辑延伸。“把 ImageIcon 放在哪里？当然，你把它放在 JLabel 上。”当你长时间、努力地使用 Java 的 Swing 组件后，所有这些对你来说都变得自然。但在那之前，你会查阅 Java API 文档中的所有内容。

![](img/bf4858233d2b2a32ff4e3991860526b3_412_0.png)

![](img/bf4858233d2b2a32ff4e3991860526b3_413_0.png)

你永远不需要记住 Java API 类的名称或特性。相反，你要随时备好 Java API 文档。当你需要了解某个类时，就在文档中查找它。如果你经常需要某个类，你就会记住它的特性。对于不常使用的类，你始终有文档可查。

有关使用 Java API 文档的提示，请参阅我的文章“Making Sense of Java’s API Documentation”，网址为 www.dummies.com/extras/beginningprogrammingwithjava。要查找大量示例 Java 代码，请访问第 21 章中列出的一些网站。

## 又一个类

JFrame 是什么？像任何其他类一样，JFrame 有几个部分。有关其中一些部分的简化视图，请参见图 20-2。

```java
public class JFrame {
    int height;
    int width;
    public Component add() ...
    public void setDefaultCloseOperation() ...
    public void pack() ...
    public void setVisible() ...
    ...
}
```

| height | width | add | setDefaultCloseOperation | pack | setVisible |
|---:|---:|---|---|---|---|
| 485 | 375 | (method to place something on the frame) | (method to decide what happens when the user closes the frame) | (method to shrink-wrap the frame) | (method to make the frame visible or invisible) |

**图 20-2：** A simplified depiction of the `JFrame` class.

如第 18 章图 18-6 中的 `String` 一样，由 `JFrame` 类形成的每个对象都同时具有数据部分和方法部分。数据部分包括框架的高度和宽度。方法部分包括 add、setDefaultCloseOperation、pack 和 setVisible。总的来说，JFrame 类大约有 320 个方法。

出于本书负担不起的技术原因，你不能使用点来引用框架的高度或宽度。但你可以用那些臭名昭著的点来调用许多 JFrame 方法。在清单 20-1 中，我通过编写 add(label)、frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)、frame.pack() 和 frame.setVisible(true) 来调用框架的方法。

以下是清单 20-1 中 `JFrame` 方法的详细情况：

- 调用 `frame.add(label)` 将标签放到框架上。标签显示我的 `androidBook.jpg` 图片，因此此调用使图片出现在框架上。

- 对 `frame.setDefaultCloseOperation` 的调用告诉 Java 当你尝试关闭框架时该做什么。（在 Windows 中，你点击标题栏旁的上方右侧的“x”。在 Mac 上，“x”位于框架的左上角。）对于大型应用程序的一部分的框架，你可能希望在点击“x”时框架消失，但你可能不希望应用程序停止运行。

但在清单 20-1 中，框架就是整个应用程序——全部内容。所以当你点击“x”时，你希望 Java 虚拟机自行关闭。为此，你使用参数 `JFrame.EXIT_ON_CLOSE` 调用 `setDefaultCloseOperation` 方法。其他替代方案如下：

  - `JFrame.HIDE_ON_CLOSE`：框架消失，但它仍然存在于计算机的内存中。
  - `JFrame.DISPOSE_ON_CLOSE`：框架消失并且不再存在于计算机的内存中。
  - `JFrame.DO_NOTHING_ON_CLOSE`：框架仍然出现，仍然存在，并且仍然做你在点击“x”之前所做的一切。点击“x”时什么也不会发生。因此，使用此 `DO_NOTHING_ON_CLOSE` 选项，你可能会变得非常困惑。

如果你不调用 `setDefaultCloseOperation`，Java 会自动选择 `HIDE_ON_CLOSE` 选项。当你点击“x”时，框架消失，但 Java 程序继续运行。当然，没有可见的框架，清单 20-1 的运行不会做太多事情。运行的唯一明显效果是你的开发环境的表现。在 Eclipse 中，Console 视图工具栏中的小方块保持其鲜红色。当你将鼠标悬停在方块上时，你会看到 Terminate 工具提示。因此，要结束 Java 程序的运行（并将方块恢复为褪色的红灰色），只需点击这个小方块即可。

- 框架的 `pack` 方法将框架收缩包装在已添加到框架的任何内容周围。如果不调用 pack，框架可能比必要的大得多或小得多。

不幸的是，默认设置是使框架比必要的小得多。如果在清单 20-1 中，你忘记调用 `frame.pack`，你会得到图 20-3 所示的微小框架。当然，你可以通过用鼠标拖动框架的边缘来放大框架。但为什么你必须这样做呢？只需调用 `frame.pack` 即可。

![](img/bf4858233d2b2a32ff4e3991860526b3_414_0.png)

![](img/bf4858233d2b2a32ff4e3991860526b3_415_0.png)

> ✓ 调用 `setVisible(true)` 使框架出现在你的屏幕上。如果你忘记调用 `setVisible(true)`（我经常这样做），当你运行清单 20-1 中的代码时，你的屏幕上将看不到任何内容。在你弄清楚自己做错了什么之前，这总是令人不安。

## 构造函数调用

在第 17 章的清单 17-3 中，我用以下行创建了 Purchase 类的一个实例

```java
Purchase onePurchase = new Purchase();
```

清单 20-1 中的代码做了同样的事情。在清单 20-1 中，我用以下行创建了 JFrame 类的一个实例：

```java
JFrame frame = new JFrame();
```

将第 17 章的图 17-4 与本章的图 20-4 进行比较。

![](img/bf4858233d2b2a32ff4e3991860526b3_415_1.png)

在两幅图中，新的 `SomethingOrOther()` 调用都会从现有类创建一个对象。

- ✔ **在第 17 章中，我创建了我自己的 `Purchase` 类的一个实例。**

  这个对象代表一次实际购买（包括购买金额、税款等）。

- ✔ **在本章中，我创建了 `JFrame` 类的一个实例。**

  这个对象代表计算机屏幕上的一个框架（带边框、最小化按钮等的框架）。在一个更复杂的应用程序中——一个显示多个框架的应用程序——代码可能会从 `JFrame` 等类创建多个对象（参见图 20-5）。

![](img/bf4858233d2b2a32ff4e3991860526b3_416_0.png)

在清单 20-1 中，以下几行

```
JFrame frame = new JFrame();
ImageIcon icon = new ImageIcon("androidBook.jpg");
JLabel label = new JLabel(icon);
```

看起来像是包含方法调用。毕竟，方法调用由名称后跟括号组成。你可能会在打开和关闭括号之间放置一些参数。表达式 `keyboard.nextLine()` 是对名为 `nextLine` 的方法的调用。所以在清单 20-1 中，`JFrame()` 是对名为 `JFrame` 的方法的调用吗？不是。
