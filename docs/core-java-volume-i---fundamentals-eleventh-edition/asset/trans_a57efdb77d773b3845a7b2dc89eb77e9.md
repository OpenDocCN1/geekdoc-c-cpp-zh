
以下是显示网页的代码：

```java
String location = "http://horstmann.com";
WebView browser = new WebView();
WebEngine engine = browser.getEngine();
engine.load(location);
```

这个浏览器是可交互的——你可以像平常一样点击链接。JavaScript 也能正常工作。不过，如果你要显示来自 JavaScript 的状态栏或弹出消息，就需要安装通知处理器，并实现自己的状态栏和弹出窗口。

> **注意：** WebView 不支持任何插件，因此不能用它显示 Flash 动画或 PDF 文档。它也不显示 applet。

在 JavaFX 之前，Java 中的媒体播放能力非常糟糕。Java Media Framework 曾作为可选下载项提供，但并没有得到开发者的太多青睐。当然，实现音频和视频播放甚至比编写浏览器更难。因此，JavaFX 利用了一个现有工具包：开源的 GStreamer 框架。

要播放视频，请根据 URL 字符串构造一个 `Media` 对象，构造一个 `MediaPlayer` 来播放它，并使用 `MediaView` 显示播放器：

```java
Path path = Paths.get("moonlanding.mp4");
Media media = new Media(path.toUri().toString());
MediaPlayer player = new MediaPlayer(media);
player.setAutoPlay(true);
MediaView video = new MediaView(player);
video.setOnError(System.out::println);
```

如图 13.31 所示，视频可以播放——但遗憾的是，没有视频控件。你可以添加自己的控件（参见 https://docs.oracle.com/javase/8/javafx/media-tutorial/playercontrol.htm），但如果能提供一组默认控件就更好了。

> **注意：** GStreamer 有时无法处理某个特定的视频文件。代码示例中的错误处理器会显示 GStreamer 消息，以便你诊断播放问题。

程序清单 13.17 展示了本节所有示例的完整代码。

![](img/127bccebb2cfadea3f02579edaad63c3_1000_0.png)

*图 13.31  播放视频（图片来源：NASA）*

**程序清单 13.17  `fancy/FancyControls.java`**

```java
package fancy;

import java.nio.file.*;
import javafx.application.*;
import javafx.geometry.*;
import javafx.scene.*;
import javafx.scene.chart.*;
import javafx.scene.layout.*;
import javafx.scene.media.*;
import javafx.scene.web.*;
import javafx.stage.*;

/**
   @version 1.0 2017-12-29
   @author Cay Horstmann
*/
public class FancyControls extends Application
{
    public void start(Stage stage)
    {
        PieChart chart = new PieChart();
        chart.getData().addAll(
            new PieChart.Data("Asia", 4298732300.0),
            new PieChart.Data("North America", 353561000.0),
            new PieChart.Data("South America", 616644000.0),
            new PieChart.Data("Europe", 742452000.0),
            new PieChart.Data("Africa", 1116305000.0),
            new PieChart.Data("Oceania", 38304000.0));
        chart.setTitle("Population of the Continents");

        String location = "http://horstmann.com";
        WebView browser = new WebView();
        WebEngine engine = browser.getEngine();
        engine.load(location);

        Path path = Paths.get("fancy/moonlanding.mp4");
        Media media = new Media(path.toUri().toString());
        MediaPlayer player = new MediaPlayer(media);
        player.setAutoPlay(true);
        MediaView video = new MediaView(player);
        video.setOnError(ex -> System.out.println(ex));

        stage.setWidth(500);
        stage.setHeight(500);
        stage.setScene(new Scene(browser));
        stage.show();

        Stage stage2 = new Stage();
        stage2.setWidth(500);
        stage2.setHeight(500);
        stage2.setX(stage.getX() + stage.getWidth());
        stage2.setY(stage.getY());
        stage2.setScene(new Scene(chart));
        stage2.show();

        HBox box = new HBox(video);
        box.setAlignment(Pos.CENTER);
        Stage stage3 = new Stage();
        stage3.setWidth(500);
        stage3.setHeight(500);
        stage3.setX(stage.getX());
        stage3.setY(stage.getY() + stage.getHeight());
        stage3.setScene(new Scene(box));
        stage3.show();
    }
}
```

## 13.6 属性与绑定

*属性*是类的一个特性，你可以读取或写入它。通常，属性由一个字段支持，属性的 getter 和 setter 只是读写该字段。但 getter 和 setter 也可以执行其他操作，例如从数据库读取值或发出变更通知。

在 JavaFX 中，属性尤其重要，因为很容易将它们“绑定”，使一个属性在另一个属性变化时更新。在以下小节中，我们将详细讨论属性和绑定。

### 13.6.1 JavaFX 属性

在许多编程语言中，有方便的语法来调用属性 getter 和 setter。在赋值语句右侧使用属性会调用 getter，在左侧使用则调用 setter。

```text
value = obj.property; // in many languages (but not Java), this calls the property getter
obj.property = value; // and this calls the property setter
```

遗憾的是，Java 没有这种语法。但自 Java 1.1 起，它就按约定支持属性。JavaBeans 规范规定，属性应从 getter/setter 对推断出来。例如，一个具有方法 `String getText()` 和 `void setText(String newValue)` 的类被视为具有 text 属性。`java.beans` 包中的 `Introspector` 和 `BeanInfo` 类可以让你枚举一个类的所有属性。

JavaBeans 规范还定义了*绑定属性*，当调用 setter 时对象会发出属性变更事件。JavaFX 并未使用规范的这一部分。相反，JavaFX 属性除了 getter 和 setter 之外还有第三个方法，返回一个实现 `Property` 接口的对象。例如，JavaFX 的 text 属性有三个方法

```java
String getText()
void setText(String value)
Property<String> textProperty()
```

> **注意：** `Node` 类有 80 多个 JavaFX 属性，而 `Rectangle` 或 `Button` 等子类有一百多个。Java API 文档会在构造器和方法之前单独列出它们。

你可以将监听器附加到属性对象上。这与老式 JavaBeans 不同。在 JavaFX 中，发出通知的是属性对象，而不是 bean。这一变化有充分的理由。实现绑定的 JavaBeans 属性需要样板代码来添加、移除和触发监听器；在 JavaFX 中则简单得多，因为有许多库类完成了大部分工作。

看看如何在 `Greeting` 类中实现属性 `text`。下面是最简单的方法：

```java
public class Greeting
{
    private StringProperty text = new SimpleStringProperty("");

    public final StringProperty textProperty() { return text; }
    public final void setText(String newValue) { text.set(newValue); }
    public final String getText() { return text.get(); }
}
```

`StringProperty` 类包装了一个字符串。它具有获取和设置所包装值以及管理监听器的方法。

如你所见，实现 JavaFX 属性需要一些样板代码，遗憾的是 Java 无法自动生成这些代码。但至少不必编写管理监听器的代码。

并不要求将属性 getter 和 setter 声明为 `final`，但 JavaFX 设计者建议这样做。

> **注意：** 使用这种模式时，每个属性都需要一个属性对象，无论是否有人监听它。如果你实现一个具有许多属性的类，并预期会构造该类的许多实例，就应该按需实例化属性对象。使用普通字段保存属性值，仅在有人调用 `xxxProperty()` 方法时才切换到属性对象。

在前面的示例中，我们定义了一个 `StringProperty`。对于基本类型属性，请使用 `IntegerProperty`、`LongProperty`、`DoubleProperty`、`FloatProperty` 或 `BooleanProperty` 之一。还有 `ListProperty`、`MapProperty` 和 `SetProperty` 类。对于其他所有情况，请使用 `ObjectProperty<T>`。这些都是抽象类，具体子类包括 `SimpleIntegerProperty`、`SimpleObjectProperty<T>` 等。

> **注意：** 如果你只关心管理监听器，属性方法可以返回 `ObjectProperty<T>` 类型的对象，甚至 `Property<T>` 接口。更专门的类有助于利用属性进行计算，下一节将对此进行说明。
