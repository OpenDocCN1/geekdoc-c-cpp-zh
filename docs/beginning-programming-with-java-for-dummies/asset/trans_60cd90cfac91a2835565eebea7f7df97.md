

![](img/f938eba5f15e231d828a6255e7ec5523_429_0.png)

- 窗口的左下部分包含一个*文档面板*，其中包含一个层次结构区域和一个控制器区域。层次结构区域包含一个 AnchorPane 项。

层次结构区域中有一个树，显示窗口中的哪些元素位于哪些其他元素内部。控制器区域帮助你把自己设计的窗口与应用程序的 Java 代码联系起来。

- 窗口最右侧部分包含一个*检查器面板*，其中包含属性区域、布局区域和代码区域。

在属性区域中，你可以描述窗口中元素的特征。在代码区域中，你为与窗口中元素关联的 Java 方法命名。

![](img/f938eba5f15e231d828a6255e7ec5523_429_1.png)

你的情况可能有所不同！这些说明适用于 Scene Builder 2.0 的预览版。如果你使用的 Scene Builder 版本不同，操作步骤可能会略有不同。

- 8. 在层次结构区域中选择 AnchorPane 项。

Scene Builder 的内容面板中间会出现一个标记。

- 9. 拖动内容面板中的标记来放大 AnchorPane（参见图 20-11）。

- 12. **在主菜单中，选择“文件 → 保存”。**

这样做会保存新的 FXML 文件。

- 13. **关闭 Scene Builder 应用程序。**

当你返回 Eclipse 工作台时，可以在 Root.fxml 文件中看到新代码（参见图 20-13）。

双击“包资源管理器”中的 Root.fxml 分支以查看文件的代码。如果代码中没有看到 `TextField` 和 `Button` 字样，请在编辑器窗口内单击鼠标。（单击鼠标会更新编辑器，以反映 Scene Builder 所做的更改。）如果编辑器中的代码缩进似乎不正确，请在编辑器中的空白区域单击鼠标，然后按 `Ctrl-Shift-F`。

任何时候你想格式化 Eclipse 编辑器中的代码（使代码更易读、更易理解），请按 `Ctrl-Shift-F`。

![](img/f938eba5f15e231d828a6255e7ec5523_431_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_431_1.png)

![](img/f938eba5f15e231d828a6255e7ec5523_431_2.png)

- 14. **编辑项目的 `Main.java` 文件。**

注释掉 `BorderPane` root 语句，并添加一条 `Parent` root 语句，如清单 20-3 中的粗体字所示。

清单 20-3 中的编辑将应用程序连接到新设计的 `Root.fxml` 布局。

- 15. **运行项目。**

运行时，你会看到如图 20-14 所示的窗口。

![](img/f938eba5f15e231d828a6255e7ec5523_431_3.png)

## 清单 20-3：如何编辑 Main.java 文件

```java
package application;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class Main extends Application {
    @Override
    public void start(Stage primaryStage) {
        try {
            // BorderPane root = new BorderPane();
            Parent root = FXMLLoader.load(getClass().
                    getResource("Root.fxml"));
            Scene scene = new Scene(root, 400, 400);
            scene.getStylesheets().
                    add(getClass().getResource("application.css")
                    .toExternalForm());
            primaryStage.setScene(scene);
            primaryStage.show();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

按照本节步骤操作时，Scene Builder 会修改项目的 Java 代码。完成本节步骤后，你可以像往常一样运行项目（选择“运行➪运行方式➪Java 应用程序”）。但项目运行时，应用程序不会执行任何操作。单击按钮时，什么也不会发生。在文本字段中键入时，什么也不会发生。真是白费功夫！

在下一节中，你将让按钮和文本字段执行操作。

## 采取行动

本章中创建的程序大约有 50 行代码。但到目前为止，你只输入了一行代码。在本节的说明中，你将让按钮响应鼠标单击。你只需要再多输入几行代码！

- 5. **在检查器面板中，单击代码区域。**

- 6. **在代码区域中，找到标记为 _On Action_ 的字段。在该字段中，输入 _onClick_ 然后按 Enter（参见图 20-16）。**

在输入 onClick 之前，请确保在代码区域顶部看到“Button”字样。如果你看到的是其他字样（例如 TextField 或 AnchorPane），那么你即将更改错误组件的 On Action 字段。

你的 Button 控件就到这里！现在，你开始操作 TextField 控件。

![](img/f938eba5f15e231d828a6255e7ec5523_434_0.png)

- 7. **选择你的 TextField 控件（在内容面板或文档面板的层次结构区域中）。**

- 8. **在代码区域中，找到标记为 _fx:id_ 的字段。在该字段中，输入 textField 然后按 Enter（参见图 20-17）。**

在向 Scene Builder 道别之前，你需要将 Scene Builder 的工作与 Java 代码联系起来：

![](img/f938eba5f15e231d828a6255e7ec5523_434_1.png)

- 9. **单击文档面板中的控制器区域。**

这样做会展开控制器区域，同时折叠层次结构区域。

- 10. **在控制器类字段（位于控制器区域内部）中输入 `application.Main`（两个单词之间有一个点），然后按 Enter（参见图 20-18）。**

在执行本节中的其他一些步骤时，你有一定的自由。例如，如果在第 4 步中键入 `Click` 而不是 `Capitalize`，程序仍然可以运行。但在填写本步骤的控制器类字段时，你的自由非常有限。默认情况下，e(fx)clipse 工具将你的程序命名为 `Main.java`，并将你的程序放在名为 `application` 的包中。因此，在控制器类字段中，你必须指向这个 application.Main 程序。如果你指向其他地方，则必须重命名程序或包，或两者都重命名。而且，本章到目前为止已经有 40 多个步骤，你可能不想做不必要的重命名。

终于！你与 Scene Builder 的合作即将结束！

![](img/f938eba5f15e231d828a6255e7ec5523_435_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_435_1.png)

- 11. **在 Scene Builder 的主菜单中，选择“文件 › 保存”。**

- 12. **关闭 Scene Builder 应用程序。**

呼！你回到了 Eclipse 工作台。

当你关闭 Scene Builder 时，Eclipse 可能不会自动更新 `Root.fxml` 文件的内容。如果代码中没有看到 `Capitalize` 字样，请在编辑器窗口内单击鼠标。（单击鼠标会更新编辑器，以反映 Scene Builder 所做的更改。）

- 13. **在 `Main.java` 文件中，在清单 20-4 开头附近和结尾附近添加粗体代码。**

清单 20-4 中的编辑告诉 Java 在用户单击 Button 控件时更改 TextField 控件中显示的文本。

完成这一步后，你就拥有了一个真正的 GUI 应用程序！

![](img/f938eba5f15e231d828a6255e7ec5523_435_2.png)

- 14. **运行项目。**

## 清单 20-4：如何编辑 Main.java 文件

```java
package application;

import javafx.event.ActionEvent;
import javafx.scene.control.TextField;
import javafx.application.Application;
import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class Main extends Application {
    @Override
    public void start(Stage primaryStage) {
        try {
            // BorderPane root = new BorderPane();
            Parent root = FXMLLoader.load(getClass().
                        getResource("Root.fxml"));
            Scene scene = new Scene(root, 400, 400);
            scene.getStylesheets().
                add(getClass().getResource("application.css").
                        toExternalForm());

            primaryStage.setScene(scene);
            primaryStage.show();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        launch(args);
    }

    @FXML
    private TextField textField;

    @FXML
    protected void onClick(ActionEvent event) {
        textField.setText(textField.getText().toUpperCase());
    }
}
```

当你运行本节的程序时，你会看到类似图 20-19、20-20 和 20-21 中的屏幕截图。*瞧！* 当你单击按钮时，Java 会将你的文本转换为大写！

