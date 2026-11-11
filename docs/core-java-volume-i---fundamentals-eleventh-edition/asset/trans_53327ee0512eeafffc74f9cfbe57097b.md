
将其计算为一个 lambda，并提供依赖属性列表。当其中任一属性发生变化时，就会重新计算该 lambda。例如，

```java
larger.disableProperty().bind(
    createBooleanBinding(
        () -> gauge.getWidth() >= 100, // this expression is computed. . .
        gauge.widthProperty())); // . . . when this property changes
```

> **注意：** 在 JavaFX Script 语言中，编译器会分析绑定表达式并自动推断出依赖属性。你只需声明 `larger.disable bind gauge.width >= 100`，编译器就会给 `gauge.width` 属性附加一个监听器。当然，在 Java 中，程序员需要提供这些信息。

清单 13.18 至 13.20 展示了本节三个示例的完整程序。

### 清单 13.18 `binding/BindingDemo1.java`

```java
1  package binding;
2
3  import javafx.application.*;
4  import javafx.scene.*;
5  import javafx.scene.control.*;
6  import javafx.scene.layout.*;
7  import javafx.stage.*;
8
9  /**
10   * @version 1.0 2017-12-29
11   * @author Cay Horstmann
12   */
13  public class BindingDemo1 extends Application
14  {
15      public void start(Stage stage)
16      {
17          TextArea shipping = new TextArea();
18          TextArea billing = new TextArea();
19          billing.textProperty().bindBidirectional(shipping.textProperty());
20          VBox root = new VBox(
21              new Label("Shipping"), shipping,
22              new Label("Billing"), billing);
23          Scene scene = new Scene(root);
24          stage.setScene(scene);
25          stage.show();
26      }
27  }
```

### 清单 13.19 `binding/BindingDemo2.java`

```java
package binding;

import javafx.application.*;
import javafx.beans.binding.*;
import javafx.scene.*;
import javafx.scene.layout.*;
import javafx.scene.paint.*;
import javafx.scene.shape.*;
import javafx.stage.*;

/**
   @version 1.0 2017-12-29
   @author Cay Horstmann
*/
public class BindingDemo2 extends Application
{
   public void start(Stage stage)
   {
      Circle circle = new Circle(100, 100, 100);
      circle.setFill(Color.RED);
      Pane pane = new Pane(circle);
      Scene scene = new Scene(pane);
      circle.centerXProperty().bind(
         Bindings.divide(scene.widthProperty(), 2));
      circle.centerYProperty().bind(
         Bindings.divide(scene.heightProperty(), 2));
      stage.setScene(scene);
      stage.show();
   }
}
```

### 清单 13.20 `binding/BindingDemo3.java`

```java
package binding;

import static javafx.beans.binding.Bindings.*;

import javafx.application.*;
import javafx.scene.*;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.scene.paint.*;
import javafx.scene.shape.*;
import javafx.stage.*;

/**
 * @version 1.0 2017-12-29
 * @author Cay Horstmann
 */
public class BindingDemo3 extends Application
{
   public void start(Stage stage)
   {
      Button smaller = new Button("Smaller");
      Button larger = new Button("Larger");
      Rectangle gauge = new Rectangle(0, 5, 50, 15);
      Rectangle outline = new Rectangle(0, 5, 100, 15);
      outline.setFill(null);
      outline.setStroke(Color.BLACK);
      Pane pane = new Pane(gauge, outline);

      smaller.setOnAction(
         event -> gauge.setWidth(gauge.getWidth() - 10));
      larger.setOnAction(
         event -> gauge.setWidth(gauge.getWidth() + 10));

      // using Bindings operator

      smaller.disableProperty().bind(
         lessThanOrEqual(gauge.widthProperty(), 0));

      // creating a binding from a lambda

      larger.disableProperty().bind(
         createBooleanBinding(
            () -> gauge.getWidth() >= 100, // this lambda is computed . . .
            gauge.widthProperty())); // . . . when this property changes

      Scene scene = new Scene(new HBox(10, smaller, pane, larger));
      stage.setScene(scene);
      stage.show();
   }
}
```

## 13.7 用户界面回调中的长时间运行任务

使用线程的原因之一是让程序响应更灵敏。这在具有用户界面的应用中尤为重要。当程序需要执行耗时操作时，不能在用户界面线程中完成该工作，否则用户界面会冻结。而应启动另一个工作线程。

在 JavaFX 中，使用 `Task<V>` 类来处理长时间运行的任务。方便的是，该类扩展了 `FutureTask<V>`，因此你不必再学习另一种自定义结构。

Task 类提供了在工作线程中更新某些任务属性的方法。你将这些属性绑定到用户界面元素，随后这些元素会在 UI 线程中更新。以下属性可用：

- `String message`
- `double progress`
- `double workDone`
- `double totalWork`
- `String title`
- `V value`

这里我们将 message 属性绑定到状态标签：

```java
status.textProperty().bind(task.messageProperty());
```

在工作线程中，调用 `updateMessage` 方法，而不是 `setMessage`。该方法会合并属性变更。也就是说，如果多个属性变更接连快速发生，只有最新的变更会在用户界面线程上产生相应的属性变更。

```java
task = new Task<>()
{
    public Integer call()
    {
        while (...)
        {
            ...
            lines++;
            updateMessage(lines + " lines read");
        }
    }
};
```

要取消 Task，请调用 `cancel` 方法。这会中断执行该任务的线程。在任务中，应定期调用 `isCancelled` 来检查任务是否已被取消。

```java
task = new Task<>()
{
    public Integer call()
    {
        while (!isCancelled() && !done)
        {
            ...
        }
    }
};
```

安装事件处理器，以便在任务被调度、开始运行，以及因成功、异常或取消而终止时收到通知。所有处理器都在 UI 线程上执行。

```java
task.setOnScheduled(event -> cancel.setDisable(false));
task.setOnRunning(event -> status.setText("Running"));
task.setOnSucceeded(event -> status.setText("Read " + task.getValue() + " lines"));
task.setOnFailed(event -> status.setText("Failed due to " + task.getException()));
task.setOnCancelled(event -> status.setText("Canceled"));
```

清单 13.21 中的程序提供了用于打开文本文件和取消文件加载过程的命令。你应该用一个很长的文件来尝试该程序，例如本书配套代码的 gutenberg 目录中提供的 *基督山伯爵* 全文。该文件会在单独的线程中加载。在读取文件期间，Open 按钮被禁用，Cancel 按钮被启用（见图 13.35）。每读取一行后，状态栏中的行计数器会更新。读取过程完成后，Open 按钮重新启用，Cancel 按钮被禁用，状态行文本被设置为一条“完成”消息。我们在各行之间添加了 10 毫秒延迟，以便你可以清楚地观察状态更新。在你自己的程序中不应这样做。

![](img/127bccebb2cfadea3f02579edaad63c3_1014_0.png)

**图 13.35** 在工作线程中从网页读取行

请密切关注工作线程和 UI 线程上发生的事情：

- call 方法在工作线程上执行。
- 传递给 `Platform.runLater` 的 lambda 在 UI 线程上执行。
- 用于“on scheduled”、“on running”、“on failed”、“on cancelled”和“on succeeded”事件的事件处理器在 UI 线程上执行。
- 调用 `updateMessage` 会在 UI 线程上引起属性变更，从而触发绑定属性的 setter。

### 清单 13.21 `uitask/TaskDemo.java`

```java
package uitask;

import java.io.*;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.*;

import javafx.application.*;
import javafx.concurrent.*;
import javafx.geometry.*;
import javafx.scene.*;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.stage.*;

public class TaskDemo extends Application
{
    private TextArea content = new TextArea("");
    private Label status = new Label();
    private ExecutorService executor = Executors.newCachedThreadPool();
    private Task<Integer> task;
    private Button open = new Button("Open");
    private Button cancel = new Button("Cancel");

    public void start(Stage stage)
    {
        open.setOnAction(event -> read(stage));
        cancel.setOnAction(event ->
        {
            if (task != null) task.cancel();
        });
        cancel.setDisable(true);
        stage.setOnCloseRequest(event ->
        {
            if (task != null) task.cancel();
            executor.shutdown();
            Platform.exit();
        });

        HBox box = new HBox(10, open, cancel);
        VBox pane = new VBox(10, content, box, status);
        pane.setPadding(new Insets(10));
        stage.setScene(new Scene(pane));
```
