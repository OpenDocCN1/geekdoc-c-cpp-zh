

## 清单 13.3（续）

```java
/**
@version 1.4 2017-12-23
@author Cay Horstmann
*/
public class FontTest extends Application
{
   private static final int PREFERRED_WIDTH = 400;
   private static final int PREFERRED_HEIGHT = 400;

   public void start(Stage stage)
   {
      // construct message at (0, 0)
      Text message = new Text("Bonjour le monde!");
      Font f = Font.font("Lucida Bright", FontWeight.BOLD, 36);
      message.setFont(f);

      // get message dimensions
      Bounds messageBounds = message.getBoundsInParent();
      double ascent = -messageBounds.getMinY();
      double descent = messageBounds.getMaxY();
      double width = messageBounds.getWidth();

      // center message horizontally
      double baseY = 100;
      double topY = baseY - ascent;
      double leftX = (PREFERRED_WIDTH - width) / 2;
      message.relocate(leftX, topY);

      // construct bounding rectangle and baseline
      Rectangle rect = new Rectangle(leftX, topY, width, ascent + descent);
      rect.setFill(Color.TRANSPARENT);
      rect.setStroke(Color.GRAY);
      Line baseline = new Line(leftX, baseY, leftX + width, baseY);
      baseline.setStroke(Color.GRAY);

      // center image directly below the message
      ImageView image = new ImageView("font/world.png");
      Bounds imageBounds = image.getBoundsInParent();
      image.relocate((PREFERRED_WIDTH - imageBounds.getWidth()) / 2, baseY + descent);

      Pane root = new Pane(message, rect, baseline, image);
      root.setPrefSize(PREFERRED_WIDTH, PREFERRED_HEIGHT);
      stage.setScene(new Scene(root));
      stage.setTitle("FontTest");
      stage.show();
   }
}
```

## javafx.scene.text.Font

- `static Font.font(double size)`
- `static Font.font(String family)`
- `static Font.font(String family, double size)`
- `static Font.font(String family, FontWeight weight, double size)`
- `static Font.font(String family, FontPosture posture, double size)`
- `static Font.font(String family, FontWeight weight, FontPosture posture, double size)`

获取一个字体，使用给定的族名称（或 "System"）、字重和字形（或 FontWeight.NORMAL 和 FontPosture.REGULAR）以及磅值大小。

## javafx.scene.text.Text

- `void setFont(Font value)`
  将此文本设置为给定字体。
- `double getX()`
- `double getY()`

  获取此文本节点基线的 x 和 y 位置。

## javafx.scene.Node

- `Bounds getBoundsInParent()`
  获取应用任何描边、裁剪、效果和变换后此节点的边界。
- `void relocate(double x, double y)`
  重新定位此节点，使其左上角位于给定的 x 和 y 值处。

## javafx.geometry.Bounds

- `double getMinX()`
- `double getMinY()`
- `double getMaxX()`
- `double getMaxY()`

  获取这些边界的 x 和 y 值的最小值或最大值。
- `double getWidth()`
- `double getHeight()`

  获取这些边界的宽度和高度。

## javafx.scene.image.ImageView

| 方法 | 说明 |
|---|---|
| `ImageView(String url)` | 从给定 url 字符串构造一个图像。该字符串必须是 `java.net.URL` 类的有效构造参数，或者是资源的路径。（关于资源，请参阅第 5 章。） |

## 13.3 事件处理

图形用户界面环境监视输入设备上的事件，例如按键或鼠标点击，并将它们导向适当的程序。程序随后确定哪个用户界面控件应处理该事件，并适当地将低级事件转换为语义事件。例如，当用户点击按钮时，JavaFX 会处理一系列事件，包括在按钮控件表面上按下和释放鼠标按钮。该事件序列随后被解释为一次“点击”。

为了让程序对此类事件做出反应，程序员需要向事件来源的用户界面控件注册一个*事件处理器*。

### 13.3.1 实现事件处理器

对于按钮点击，事件处理器必须实现 `EventHandler<ActionEvent>` 接口。`EventHandler<T>` 是一个函数式接口，只有一个方法：

```java
void handle(T event)
```

你可以直接使用 lambda 表达式来指定按钮动作：

```java
Button button = new Button("Click me!");
button.setOnAction(event -> System.out.println("I was clicked"));
```

在这个例子中，lambda 表达式没有使用事件参数。ActionEvent 没有太多有趣的属性。其中最有用的大概是事件源——即动作发起的控件。在这个例子中，我们知道哪个按钮是事件源。但是，如果你在多个控件之间共享一个处理器，可以调用 event.getSource() 来找出是哪一个触发了事件。

这里还有另一个事件处理的应用，你会对事件对象感兴趣。当用户关闭窗口时，窗口会收到一个“关闭请求”事件。如果你想拒绝该请求，可以安装一个处理器，在其中 *消费* 该事件：

```java
stage.setOnCloseRequest(event ->
{
    if (not OK to close) event.consume()
});
```

> **注意：** 如果需要向节点添加多个事件，请使用 addEventHandler 方法：
>
> ```java
> button.addEventHandler(javafx.event.ActionEvent.ACTION,
>     event -> System.out.println("I was clicked"));
> ```

### 13.3.2 响应属性更改

许多 JavaFX 控件为事件处理提供了不同的机制。考虑一个滑块，如图 13.7 所示。当滑块被调整时，它的值会改变。然而，你不应该监听滑块发出的指示这些变化的低级事件。相反，滑块有一个称为 value 的 JavaFX *属性*，当它改变时会发出事件。我们将在第 82 页的 13.6 节“属性和绑定”中详细讨论属性。下面是你如何监听该属性的事件并调整消息字体大小的方法：

```java
slider.valueProperty().addListener(property ->
    message.setFont(Font.font(family, slider.getValue())));
```

这里，property 参数并不是很有用——从滑块获取更新后的值更容易。

监听属性在 JavaFX 中非常常见。例如，如果你想在用户向文本字段输入文本时更改用户界面的某一部分，只需向 text 属性添加一个监听器即可。

清单 13.4 中的程序演示了动作事件和属性更改事件的工作方式。当你点击“Random font”按钮时，一个 Text 节点会被设置为随机字体的名称，并以同一种字体显示——参见图 13.7。

当滑块移动时，字体大小会被调整。

当用户关闭窗口时，事件监听器检查滑块是否位于 100%。如果是，程序将拒绝关闭，并假设用户尚未尝试使用滑块。

按钮、滑块和文本节点垂直堆叠在一个 VBox 中。我们将在第 28 页的 13.4 节“布局”中讨论这个类。

![](img/127bccebb2cfadea3f02579edaad63c3_938_0.png)

**图 13.7** 处理动作和属性更改事件

## 清单 13.4 `event/EventTest.java`

```java
package event;

import java.util.*;

import javafx.application.*;
import javafx.scene.*;
import javafx.scene.control.*;
import javafx.scene.control.Alert.*;
import javafx.scene.layout.*;
import javafx.scene.text.*;
import javafx.stage.*;

/**
   @version 1.0 2017-12-23
   @author Cay Horstmann
*/
public class EventTest extends Application
{
   public void start(Stage stage)
   {
      Button button = new Button("Random font");
      Text message = new Text("Times New Roman");
      message.setFont(Font.font("Gloucester MT Extra Condensed", 100));
      List<String> families = Font.getFamilies();
      Random generator = new Random();
      button.setOnAction(event ->
         {
            String newFamily = families.get(
               generator.nextInt(families.size()));
            message.setText(newFamily);
            message.setFont(Font.font(
               newFamily, message.getFont().getSize()));
         });

      Slider slider = new Slider();
      slider.setValue(100);
```

