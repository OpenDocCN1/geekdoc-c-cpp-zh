

如果一个模块依赖于另一个模块，那么这种依赖应该是物理上的，而不仅仅是逻辑上的。被依赖的模块不应该对它所依赖的模块做出假设（换句话说，即逻辑依赖）。相反，它应该明确地向那个模块请求它所依赖的所有信息。

例如，假设你在编写一个函数，它以纯文本格式打印员工的工作时长报告。一个名为 `HourlyReporter` 的类将所有数据汇总成方便的形式，然后传递给 `HourlyReportFormatter` 进行打印。（参见[清单 17-1](#listing-17-1)。）

### 清单 17-1 HourlyReporter.java

```java
public class HourlyReporter {
    private HourlyReportFormatter formatter;
    private List<LineItem> page;
    private final int PAGE_SIZE = 55;

    public HourlyReporter(HourlyReportFormatter formatter) {
        this.formatter = formatter;
        page = new ArrayList<LineItem>();
    }

    public void generateReport(List<HourlyEmployee> employees) {
        for (HourlyEmployee e : employees) {
            addLineItemToPage(e);
            if (page.size() == PAGE_SIZE)
                printAndClearItemList();
        }
        if (page.size() > 0)
            printAndClearItemList();
    }

    private void printAndClearItemList() {
        formatter.format(page);
        page.clear();
    }

    private void addLineItemToPage(HourlyEmployee e) {
```

首先，大多数人使用 switch 语句是因为这是一种显而易见的暴力解决方案，而不是因为它适合当前情况的正确解决方案。因此，这个启发式规则在这里提醒我们在使用 switch 之前考虑多态。

其次，函数比类型更容易变化的情况相对较少。因此，*每一个* switch 语句都应受到质疑。

我使用以下“单一 switch”规则：*对于给定类型的选择，不能有多个 switch 语句。该 switch 语句中的 case 必须创建多态对象，以替代系统中其余地方的其他类似 switch 语句。*

## **G24：遵循标准约定**

每个团队都应该遵循基于行业通用标准的编码规范。这个编码规范应该明确规定诸如在何处声明实例变量、如何命名类、方法和变量、在何处放置花括号等内容。团队不需要用文档来描述这些约定，因为他们的代码本身就是示例。

团队中的每个人都应该遵循这些约定。这意味着每个团队成员都必须足够成熟，能够意识到只要大家一致同意花括号放在哪里，那么放在哪里并不重要。

如果你想了解我遵循什么约定，可以在第 394 页的[清单 B-7](#)到[清单 B-14](#)的重构代码中看到。

## **G25：用命名常量替换魔法数字**

这可能是软件开发中最古老的规则之一。我记得在六十年代末，我在 COBOL、FORTRAN 和 PL/1 的入门手册中读到过它。一般来说，在代码中使用原始数字是一种坏主意。你应该将它们隐藏在命名得当的常量后面。

例如，数字 86,400 应该隐藏在常量 `SECONDS_PER_DAY` 后面。如果你每页打印 55 行，那么常量 55 应该隐藏在常量 `LINES_PER_PAGE` 后面。

有些常量非常容易识别，因此只要它们与以下代码结合使用，就不总是需要命名常量来隐藏它们：

```java
public void dive(String reason) {
    Gradient gradient = saturateGradient();
    List<Spline> splines = reticulateSplines(gradient);
    diveForMoog(splines, reason);
}
...
}
```

这通过创建一条“串联传递”链暴露了时间耦合。每个函数产生的结果都是下一个函数所需要的，因此没有合理的方式可以不按顺序调用它们。

你可能会抱怨这增加了函数的复杂度，你说得没错。但额外的语法复杂度恰恰暴露了情境中真实的时间复杂度。

注意我保留了实例变量。我猜想它们会被类中的私有方法使用。即便如此，我仍希望参数就位，以使时间耦合明确。

## G32：*不要武断*

你构建代码的方式要有理由，并确保这个理由通过代码结构传达出来。如果某个结构看起来是随意的，其他人就会认为有权更改它。如果某个结构在整个系统中保持一致，其他人就会使用它并保留这个约定。例如，我最近在合并 FitNesse 的更改时，发现我们的一位提交者写了这样的代码：

```java
public class AliasLinkWidget extends ParentWidget
{
    public static class VariableExpandingWidgetRoot {
        ...
    }
    ...
}
```

也许程序员是为了方便而将 `VariableExpandingWidgetRoot` 随意放进了 `AliasLinkWidget`，或者他可能认为它确实需要被限定在 `AliasLinkWidget` 内部。无论原因是什么，结果都是随意的。公共类如果不是其他类的工具类，就不应该被限定在另一个类内部。约定是让它们在包的最顶层成为公共类。

## G33：*封装边界条件*

边界条件很难记录。将它们的处理集中在一个地方。不要让它们泄漏到整个代码中。我们不希望大量的 +1 和 -1 四处散落。考虑下面这个来自 FIT 的简单示例：

```java
if(level + 1 < tags.length)
{
    parts = new Parse(body, tags, level + 1, offset + endTag);
    body = null;
}
```

注意 `level+1` 出现了两次。这是一个边界条件，应该封装在一个名为 `nextLevel` 之类的变量中。

```java
int nextLevel = level + 1;
if(nextLevel < tags.length)
{
    parts = new Parse(body, tags, nextLevel, offset + endTag);
    body = null;
}
```

## G34：*函数应该只下降一层抽象级别*

函数内的语句应该都写在相同的抽象级别上，这个级别应该比函数名称所描述的操作低一级。这可能是这些启发式规则中最难解释和遵循的一条。虽然这个思想已经足够简单，但人类太擅长无缝地混合抽象级别了。例如，考虑下面这段来自 FitNesse 的代码：

```java
public String render() throws Exception
{
    StringBuffer html = new StringBuffer("<hr");
    if(size > 0)
        html.append(" size=\"").append(size + 1).append("\"");
    html.append(">");

    return html.toString();
}
```

稍加研究，你就能明白发生了什么。这个函数构造了在页面上绘制水平线的 HTML 标签。该线的高度由 `size` 变量指定。

现在再看一遍。这个方法混合了至少两个抽象级别。第一个是水平线有大小这一概念。第二个是 HR 标签本身的语法。这段代码来自 FitNesse 的 `HruleWidget` 模块。该模块检测一行四个或更多破折号，并将其转换为相应的 HR 标签。破折号越多，尺寸就越大。

我重构了这段代码，如下所示。注意我更改了 `size` 字段的名称，以反映其真实用途。它保存的是额外破折号的数量。

```java
public String render() throws Exception
{
    HtmlTag hr = new HtmlTag("hr");
    if (extraDashes > 0)
        hr.addAttribute("size", hrSize(extraDashes));
    return hr.html();
}
```

```java
private String hrSize(int height)
{
    int hrSize = height + 1;
    return String.format("%d", hrSize);
}
```

这一改动很好地将两个抽象级别分开了。`render` 函数只是简单地构造一个 HR 标签，而无需了解任何

