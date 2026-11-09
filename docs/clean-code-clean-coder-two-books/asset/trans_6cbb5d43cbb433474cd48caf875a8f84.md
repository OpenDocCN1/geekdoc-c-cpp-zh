
```java
private String getPageNameOrDefault(Request request, String
defaultPageName)
{
    String pageName = request.getResource();
    if (StringUtil.isBlank(pageName))
        pageName = defaultPageName;

    return pageName;
}

protected void loadPage(String resource, FitNesseContext context)
    throws Exception {
    WikiPagePath path = PathParser.parse(resource);
    crawler = context.root.getPageCrawler();
    crawler.setDeadEndStrategy(new VirtualEnabledPageCrawler());
    page = crawler.getPage(context.root, path);
    if (page != null)
        pageData = page.getData();
}

private Response notFoundResponse(FitNesseContext context, Request
request)
    throws Exception {
    return new NotFoundResponder().makeResponse(context, request);
}

private SimpleResponse makePageResponse(FitNesseContext context)
    throws Exception {
    pageTitle = PathParser.render(crawler.getFullPath(page));
    String html = makeHtml(context);

    SimpleResponse response = new SimpleResponse();
    response.setMaxAge(0);
    response.setContent(html);
    return response;
}
}
...
```

顺便说一句，这段代码为如何在适当的层次上保留常量提供了一个很好的例子[G35]。“FrontPage”常量本可以埋藏在`getPageNameOrDefault`函数内部，但那会把这个众所周知且理应出现的常量隐藏在一个不适当的低层函数中。更好的做法是，把这个常量从知道它有意义的地方向下传递到真正使用它的地方。

**概念亲和性。**某些代码片段*希望*彼此靠近。它们具有某种概念上的亲和性。这种亲和性越强，它们之间的垂直距离就应该越小。

正如我们所见，这种亲和性可能基于直接的依赖关系，例如一个函数调用另一个函数，或者一个函数使用某个变量。但亲和性还有其他可能的原因。一组函数执行类似的操作也可能导致亲和性。请看JUnit 4.3.1中的这段代码：

![](img/d3848357ae109884a140c7b3662e0e30_147_0.png)

```java
public class Assert {
    static public void assertTrue(String message, boolean condition) {
        if (!condition)
            fail(message);
    }

    static public void assertTrue(boolean condition) {
        assertTrue(null, condition);
    }

    static public void assertFalse(String message, boolean condition) {
        assertTrue(message, !condition);
    }
}
```

![](img/d3848357ae109884a140c7b3662e0e30_149_0.png)

这表明我们应该努力让代码行保持简短。旧的Hollerith 80列限制有点武断，我并不反对代码行延伸到100甚至120个字符。但再长的话，可能就只是粗心大意了。

我曾遵循一条规则：永远不需要向右滚动。但如今显示器已经太宽了，年轻程序员可以把字体缩得很小，以至于一屏能放下200个字符。不要这样做。我个人把限制设为120。

## 水平开放性与密度

我们使用水平空白来关联关系紧密的事物，并分离关系较弱的事物。考虑以下函数：

```java
private void measureLine(String line) {
    lineCount++;
    int lineSize = line.length();
    totalChars += lineSize;
    lineWidthHistogram.addLine(lineSize, lineCount);
    recordWidestLine(lineSize);
}
```

另一方面，我没有在函数名和左括号之间加空格。这是因为函数与其参数紧密相关。将它们分开会让它们看起来是分离的，而不是结合在一起的。我会在函数调用的括号内分隔参数，以突出逗号，并表明各个参数是相互独立的。

空白的另一个用途是突出运算符的优先级。

```java
public class Quadratic {
    public static double root1(double a, double b, double c) {
        double determinant = determinant(a, b, c);
        return (-b + Math.sqrt(determinant)) / (2*a);
    }

    public static double root2(double a, double b, double c) {
        double determinant = determinant(a, b, c);
        return (-b - Math.sqrt(determinant)) / (2*a);
    }

    private static double determinant(double a, double b, double c) {
        return b*b - 4*a*c;
    }
}
```

注意这些方程读起来多么优美。因子之间没有空格，因为它们是高优先级的。各项之间用空格分隔，因为加法和减法的优先级较低。

不幸的是，大多数代码重新格式化工具对运算符的优先级视而不见，会在整个代码中强加相同的间距。因此，像上面展示的那种微妙间距，在重新格式化代码之后往往会丢失。

## 水平对齐

当我还是汇编语言程序员时^3，我使用水平对齐来突出某些结构。当我开始用C、C++，并最终用Java编码时，我仍然试图将一组声明中的所有变量名对齐，或将一组赋值语句中的所有值对齐。我的代码可能看起来像这样：

```java
public class FitNesseExpediter implements ResponseSender
{
    private Socket socket;
    private InputStream input;
    private OutputStream output;
    private Request request;
    private Response response;
    private FitNesseContext context;
    protected long requestParsingTimeLimit;
    private long requestProgress;
    private long requestParsingDeadline;
    private boolean hasError;

    public FitNesseExpediter(Socket s,
                             FitNesseContext context) throws Exception
    {
        this.context = context;
        socket = s;
        input = s.getInputStream();
        output = s.getOutputStream();
        requestParsingTimeLimit = 1000;
    }
}
```

然而，我发现这种对齐并没有用处。对齐似乎强调了错误的东西，会把我的视线从真正的意图上引开。例如，在上面的声明列表中，你会忍不住顺着变量名往下读，而不去看它们的类型。同样，在赋值语句列表中，你会忍不住只看右值列表，而从不看赋值运算符。更糟的是，自动格式化工具通常会消除这种对齐。

所以，归根结底，我不再这样做了。如今我更喜欢不对齐的声明和赋值，如下所示，因为它们能暴露出一个重要缺陷。如果我需要对齐很长的列表，问题在于列表的长度，而不是缺少对齐。下面`FitNesseExpediter`中声明列表的长度表明，这个类应该被拆分。

```java
public class FitNesseExpediter implements ResponseSender
{
    private Socket socket;
    private InputStream input;
    private OutputStream output;
    private Request request;

    private Response response;
    private FitNesseContext context;
    protected long requestParsingTimeLimit;
    private long requestProgress;
    private long requestParsingDeadline;
    private boolean hasError;

    public FitNesseExpediter(Socket s, FitNesseContext context) throws Exception
    {
        this.context = context;
        socket = s;
        input = s.getInputStream();
        output = s.getOutputStream();
        requestParsingTimeLimit = 10000;
    }
}
```

## 缩进

源文件是一个类似大纲的层次结构。有些信息属于整个文件，有些属于文件中的各个类，有些属于类中的方法，有些属于方法中的代码块，并递归地属于代码块中的代码块。这个层次结构的每一层都是一个作用域，可以在其中声明名称，也可以在其中解释声明和可执行语句。

为了使这个作用域层次结构可见，我们根据源代码行在层次结构中的位置按比例缩进它们。文件级别的语句（如大多数类声明）完全不缩进。类中的方法在类的基础上向右缩进一级。这些方法的实现则实现在……的右侧一级处
