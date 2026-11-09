

方法声明。块实现比其所在块向右缩进一级，依此类推。

程序员非常依赖这种缩进方案。他们通过视觉上对齐左侧的行来判断自己处于哪个作用域。这使他们能够快速跳过与当前情况无关的作用域，例如`if`或`while`语句的实现。他们扫视左侧以寻找新的方法声明、新变量乃至新类。没有缩进，程序对人类来说几乎无法阅读。

考虑下面两个在语法和语义上完全相同的程序：

```java
public class FitNesseServer implements SocketServer { private FitNesseContext context; public FitNesseServer(FitNesseContext context) { this.context = context; } public void serve(Socket s) { serve(s, 10000); } public void serve(Socket s, long requestTimeout) { try { FitNesseExpediter sender = new FitNesseExpediter(s, context); sender.setRequestParsingTimeLimit(requestTimeout); sender.start(); } catch(Exception e) { e.printStackTrace(); } } }
```

---

```java
public class FitNesseServer implements SocketServer {
    private FitNesseContext context;

    public FitNesseServer(FitNesseContext context) {
        this.context = context;
    }

    public void serve(Socket s) {
        serve(s, 10000);
    }

    public void serve(Socket s, long requestTimeout) {
        try {
            FitNesseExpediter sender = new FitNesseExpediter(s, context);
            sender.setRequestParsingTimeLimit(requestTimeout);
            sender.start();
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

你的眼睛可以迅速辨别出缩进文件的结构。你几乎能立刻发现变量、构造函数、访问器和方法。只需几秒钟就能看出这是某种简单的 socket 前端，带有超时机制。而未缩进的版本，如果不仔细研究，几乎无法看透。

**打破缩进。** 有时，面对简短的`if`语句、简短的`while`循环或简短函数，我们会忍不住打破缩进规则。每当我屈服于这种诱惑时，几乎总是会回头把缩进加回去。因此，我避免把作用域压缩成一行，像这样：

```java
public class CommentWidget extends TextWidget
{
    public static final String REGEXP = "^#[^\r\n]*(?:(?:\r\n)|\n|\r)?";

    public CommentWidget(ParentWidget parent, String text){ super(parent, text);}
    public String render() throws Exception {return ""; }
}
```

我更喜欢展开并缩进作用域，像这样：

```java
public class CommentWidget extends TextWidget {
    public static final String REGEXP = "^#[^\r\n]*(?:(?:\r\n)|\n|\r)?";

    public CommentWidget(ParentWidget parent, String text) {
        super(parent, text);
    }
```

自那以后。这些并非我偏爱的规则，而是团队决定的规则。作为团队的一员，我在 FitNesse 项目中编写代码时遵循了这些规则。

记住，一个优秀的软件系统由一组读起来赏心悦目的文档组成。它们需要有一致而流畅的风格。读者需要能够相信，在一个源文件中看到的格式表达方式，在其他文件中含义相同。我们最不想做的事情，就是用一堆杂乱无章的个人风格给源代码增添更多复杂性。

## 鲍勃大叔的格式规则

我个人使用的规则非常简单，[清单 5-6](#)中的代码对此进行了说明。把这看作一个例子，说明代码如何成为最好的编码标准文档。

```java
// Listing 5-6: CodeAnalyzer.java
public int getWidestLineNumber() {
    return widestLineNumber;
}

public LineWidthHistogram getLineWidthHistogram() {
    return lineWidthHistogram;
}

public double getMeanLineWidth() {
    return (double)totalChars/lineCount;
}

public int getMedianLineWidth() {
    Integer[] sortedWidths = getSortedWidths();
    int cumulativeLineCount = 0;
    for (int width : sortedWidths) {
        cumulativeLineCount += lineCountForWidth(width);
        if (cumulativeLineCount > lineCount/2)
            return width;
    }
    throw new Error("Cannot get here");
}

private int lineCountForWidth(int width) {
    return lineWidthHistogram.getLinesForWidth(width).size();
}

private Integer[] getSortedWidths() {
    Set<Integer> widths = lineWidthHistogram.getWidths();
    Integer[] sortedWidths = (widths.toArray(new Integer[0]));
    Arrays.sort(sortedWidths);
    return sortedWidths;
}
}
```

## 6 对象和数据结构

![](img/d3848357ae109884a140c7b3662e0e30_158_0.png)

我们将变量设为私有是有原因的。我们不希望其他人依赖它们。我们希望保留随心所欲更改其类型或实现的自由。那么，为什么这么多程序员会不假思索地给对象添加 getter 和 setter，把私有变量暴露得像公开变量一样呢？

### 数据抽象

思考一下[清单 6-1](#listing-6-1)和[清单 6-2](#listing-6-2)之间的区别。两者都表示了笛卡尔平面上一个点的数据。然而，一个暴露了其实现，另一个则完全隐藏了实现。

**清单 6-1** *具体点*

```java
public class Point {
    public double x;
    public double y;
}
```

**清单 6-2** *抽象点*

```java
double getGallonsOfGasoline();
}
```

**清单 6-4** `Abstract Vehicle`

```java
public interface Vehicle {
    double getPercentFuelRemaining();
}
```

在上述两种情况下，第二种选择都更可取。我们不想暴露数据的细节，而是希望以抽象的方式表达数据。这不仅仅是通过使用接口和/或 getter 与 setter 就能实现的。需要认真思考如何以最佳方式表示对象所包含的数据。最糟糕的选择是轻率地添加 getter 和 setter。

### 数据/对象反对称性

这两个例子展示了对象与数据结构之间的区别。对象将数据隐藏在抽象之后，并暴露操作这些数据的函数。数据结构则暴露其数据，并且没有有意义的函数。回过头去再读一遍。注意这两个定义的互补性质。它们几乎是完全对立的。这种差异看似微不足道，却有着深远的影响。

例如，考虑[清单 6-5](#listing-6-5)中的过程式形状示例。`Geometry`类对三个形状类进行操作。这些形状类是简单的数据结构，没有任何行为。所有行为都在`Geometry`类中。

**清单 6-5** `Procedural Shape`

```java
public class Square {
    public Point topLeft;
    public double side;
}

public class Rectangle {
    public Point topLeft;
    public double height;
    public double width;
}

public class Circle {
    public Point center;
    public double radius;
}

public class Geometry {
    public final double PI = 3.141592653589793;

    public double area(Object shape) throws NoSuchShapeException
    {
        if (shape instanceof Square) {
            Square s = (Square)shape;
            return s.side * s.side;
        }

        else if (shape instanceof Rectangle) {
            Rectangle r = (Rectangle)shape;
            return r.height * r.width;
        }
        else if (shape instanceof Circle) {
            Circle c = (Circle)shape;
            return PI * c.radius * c.radius;
        }
        throw new NoSuchShapeException();
    }
}
```

面向对象的程序员可能会对此嗤之以鼻，抱怨这是过程式的——他们说得没错。但这种嘲笑可能并不合理。想想如果给`Geometry`添加一个`perimeter()`函数会发生什么。形状类完全不受影响！其他依赖这些形状的类也完全不受影响！另一方面，如果我添加一个新形状，就必须修改`Geometry`中的所有函数来处理它。再读一遍。注意，这两种情况是截然相反的。

