
# 附录 F Java 编码规范

## A. 标识符命名

- 1. 为标识符赋予语义含义。例如，除非单个字母具有语义含义，否则不要使用单个字母名称，如 a 或 i。

- 2. 使标识符易于阅读。例如，使用 currentValue 而不是 curval。

- 3. 保持标识符长度在合理范围内。

- 4. 使用下划线字符分隔常量的单词。

### B. 标识符大小写

- 1. 常量使用 UPPERCASE。

- 2. 类、包和接口名称使用 Title Case。

- 3. 变量和方法名称使用 lowercase，除第一个单词外的每个单词的首字母大写。例如，minTaxRate。请注意，所有保留字必须为小写。

### C. 缩进

- 1. 将任何块中的代码缩进三个或四个空格（保持一致）。

- 2. 如果循环、if 语句或 else 子句的主体是一个单一语句（不是块），则将该语句单独缩进三空格到其行上。

- 3. 将开始每个新块的左大括号（{）放在新行上。使结束的右大括号（}）与开始的左大括号对齐。例如：

```java
while (value < 25)
{
    value += 5;
    System.out.println("The value is " + value);
}
```

- 4. 在 switch 语句中，将每个 case 标签缩进三空格。将与某个 case 关联的所有代码再缩进三个空格。

### D. 间距

- 1. 仔细使用空白来突出程序的适当特征。

- 2. 在参数列表中的每个逗号后加一个空格。

- 3. 在二元运算符的两侧各加一个空格。

- 4. 不要在左括号后或右括号前加空格。

- 5. 不要在分号前加空格。

- 6. 在左括号前加一个空格，除空参数列表外。

```
//***********************************
//
//          header block
//***********************************
```

### D. 行内注释

- 1. 适当使用行内文档来清晰描述有趣的处理过程。
- 2. 仅当注释适用于一行代码并且可以方便地放在该行上时，才将注释与代码放在同一行。否则，将注释放在单独的行上，位于其适用的代码行或代码段上方。

### E. 杂项

- 1. 避免使用 /* */ 风格的注释，除非符合 javadoc (/ ** */) 注释约定。
- 2. 不要等到程序完成后再插入文档。随着系统各部分的完成，适当对其进行注释。

# Java Applet

在第 2 章中我们介绍了 applet 的基本概念，包括 applet 与应用程序的区别以及如何在 HTML 页面中引用 applet 以便在浏览器中执行。第 2 章中的 applet 示例展示了简单的绘图。我们在第 9 章重新探讨了 applet 的概念，探索了 applet 如何成为继承的一个良好示例。本附录补充了有关 Java applet 的其他细节。

第 2 章中的示例 applet 重写了 JApplet 类的 paint 方法。Applet 有多个执行特定任务的其他方法。因为 applet 设计为与网页配合工作，所以一些 applet 方法就是专门为此概念设计的。图 G.1 列出了几个 applet 方法。

```
public void init ()
Initializes the applet. Called just after the applet is loaded.

public void start ()
Starts the applet. Called just after the applet is made active.

public void stop ()
Stops the applet. Called just after the applet is made inactive.

public void destroy ()
Destroys the applet. Called when the browser is exited.

public URL getCodeBase ()
Returns the URL at which this applet's bytecode is located.

public URL getDocumentBase ()
Returns the URL at which the HTML document containing this applet is located.

public AudioClip getAudioClip (URL url, String name)
Retrieves an audio clip from the specified URL.

public Image getImage (URL url, String name)
Retrieves an image from the specified URL.
```

图 G.1 Applet 类的一些方法

init 方法在 applet 第一次加载时执行一次，例如当浏览器或 appletviewer 最初查看 applet 时。因此 init 方法是初始化 applet 环境和永久数据的合适位置。

applet 的 start 和 stop 方法分别在 applet 变得活动或非活动时被调用。例如，在我们使用浏览器首次加载 applet 后，applet 的 start 方法会被调用。然后我们可能会离开该页面访问另一个页面，此时 applet 变得非活动，stop 方法会被调用。如果我们返回到 applet 的页面，applet 再次变得活动，start 方法会再次被调用。

请注意，init 方法在 applet 加载时只调用一次，但 start 可能在页面被多次访问时被调用多次。如果 applet 积极使用 CPU 时间，例如显示动画时，实现 start 和 stop 对于 applet 是良好的实践，这样不会浪费 CPU 时间在不可见的 applet 上。

另请注意，在浏览器中重新加载网页不一定会重新加载 applet。为了强制 applet 重新加载，大多数浏览器都提供了相应的键组合。例如，在 Netscape Navigator 中，按住 Shift 键同时用鼠标点击 Reload 按钮，不仅会重新加载网页，还会重新加载（并重新初始化）与该页面链接的所有 applet。

getCodeBase 和 getDocumentBase 方法对于确定 applet 的字节码或 HTML 文档所在位置很有用。Applet 可以使用适当的 URL 来检索额外的资源，例如通过 applet 方法 getImage 或 getAudioClip 分别检索图像或音频剪辑。

安全性是 applet 的一个问题。当你浏览网页时，你可能会打开包含 applet 的页面，突然一个未知程序在你的机器上执行。由于该过程固有的危险，applet 在其可以执行的操作方面受到限制。例如，applet 不能向本地驱动器写入数据。

在本书的 Graphics Track 各节中，我们探讨了与开发使用图形用户界面（GUI）的程序相关的问题。那些节中的示例以 Java 应用程序形式呈现，使用 JFrame 组件作为主要重量级容器。Applet 也可以用于呈现基于 GUI 的程序。像 JFrame 一样，JApplet 也是一个重量级容器。

Applet 对于小型、独立的程序很有用，例如游戏或计算器。由于其安全限制和处理开销，它们不常用于大型系统。通常，其他技术用于支持完全集成、动态的网站。

# 正则表达式

在整本书中我们使用 Scanner 类从用户读取交互式输入并将字符串解析为单个标记，如单词。在第 5 章中我们也用它从数据文件读取输入。通常我们使用扫描器输入的默认空白分隔符作为标记的分隔符。

Scanner 类也可以根据正则表达式解析其输入，正则表达式是一个表示模式的字符字符串。正则表达式可用于设置提取标记时使用的分隔符，或可在 findInLine 等方法中用于匹配特定字符串。

构造正则表达式的一些通用规则包括：

- 点号 (.) 字符匹配任何单个字符。
- * 字符，称为 Kleene 星号，匹配零个或多个字符。
- 方括号 ([ ]) 中的字符串匹配该字符串中的任何单个字符。
- \ 字符后跟一个特殊字符（如本列表中的字符）匹配该字符本身。
- \ 字符后跟一个字符匹配该字符指定的模式（见下表）。

例如，正则表达式 B.b* 匹配 Bob、Bubba 和 Baby。正则表达式 T[aei]*ing 匹配 Taking、Tickling 和 Telling。

这些示例只是众多示例中的几个。图 H.1 指定了可在 Java 正则表达式中匹配的一些模式，此列表并不完整。请参阅 Pattern 类的在线文档以获取完整列表。
