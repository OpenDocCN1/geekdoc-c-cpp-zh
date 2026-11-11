

> **警告：** 不要将包含按钮的 HBox 在网格中居中。该 HBox 已扩展到完整的水平尺寸，居中将不会改变其位置。相反，应让 HBox 将其内容居中：
>
> `buttons.setAlignment(Pos.CENTER);`

你还需要在行和列周围设置一些间距，并在表格周围设置一些内边距：

```java
pane.setHgap(0.8 * rem);
pane.setVgap(0.8 * rem);
pane.setPadding(new Insets(0.8 * rem));
```

你在本节中看到的布局面板应该足以满足大多数应用程序的需求。表 13.2 显示了 JavaFX 附带的所有布局。清单 13.6 显示了此布局的完整程序。有关该程序使用的用户界面控件的更多信息，请参阅第 47 页的 13.5.1 节“文本输入”。

**表 13.2 JavaFX 布局**

| 面板类 | 说明 |
| --- | --- |
| HBox、VBox | 水平或垂直排列子节点。 |
| GridPane | 以表格网格形式布局子节点，类似于 Swing 的 GridBagLayout。 |
| TilePane | 以网格形式布局子节点，使它们具有相同的大小，类似于 Swing 的 GridLayout。 |
| BorderPane | 提供北、东、南、西和中心区域，类似于 Swing 的 BorderLayout。 |
| FlowPane | 按行排列子节点，空间不足时换行，类似于 Swing 的 FlowLayout。 |
| AnchorPane | 将子节点放置在绝对位置或相对于面板边界的位置。这是 Scene Builder 布局工具中的默认面板。 |
| StackPane | 将子节点堆叠在一起。可用于装饰控件，例如将按钮叠放在彩色矩形上。 |

> **提示：** Scala、Kotlin 和 Groovy 提供了 JavaFX 绑定（http://www.scalafx.org、http://tornadofx.io、http://groovyfx.org），并带有便捷的“领域特定语言”用于构建用户界面，这些语言让人联想到旧版 FX Script 构建器语法。

## 清单 13.6 `gridPane/GridPaneDemo.java`

```java
package gridPane;

import javafx.application.*;
import javafx.geometry.*;
import javafx.scene.*;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.scene.text.*;
import javafx.stage.*;

public class GridPaneDemo extends Application
{
    public void start(Stage stage)
    {
        final double rem = new Text("").getLayoutBounds().getHeight();

        GridPane pane = new GridPane();
        // uncomment for debugging
        // pane.setGridLinesVisible(true);

        pane.setHgap(0.8 * rem);
        pane.setVgap(0.8 * rem);
        pane.setPadding(new Insets(0.8 * rem));
        Label usernameLabel = new Label("User name:");
        Label passwordLabel = new Label("Password:");
        TextField username = new TextField();
        PasswordField password = new PasswordField();

        Button okButton = new Button("Ok");
        Button cancelButton = new Button("Cancel");

        HBox buttons = new HBox(0.8 * rem);
        buttons.getChildren().addAll(okButton, cancelButton);
        buttons.setAlignment(Pos.CENTER);
        // uncomment for debugging
        // buttons.setStyle("-fx-border-color: red;");

        pane.add(usernameLabel, 0, 0);
        pane.add(username, 1, 0);
        pane.add(passwordLabel, 0, 1);
        pane.add(password, 1, 1);
        pane.add(buttons, 0, 2, 2, 1);

        GridPane.setHalignment(usernameLabel, HPos.RIGHT);
        GridPane.setHalignment(passwordLabel, HPos.RIGHT);

        stage.setScene(new Scene(pane));
        stage.show();
    }
}
```

| `javafx.scene.layout.BorderPane` |
| --- |
| • `BorderPane()`<br>构造一个空的边界面板。<br><br>• `void setTop(Node value)`<br>• `void setRight(Node value)`<br>• `void setBottom(Node value)`<br>• `void setLeft(Node value)`<br>• `void setCenter(Node value)`<br>将节点放置到此边界面板的某个区域中。 |

| `javafx.scene.layout.HBox` |
| --- |
| • `HBox(double spacing, Node... children)`<br>用给定的子节点构造一个水平框，子节点之间以 spacing 参数指定的像素数分隔。<br><br>• `void setAlignment(Pos pos)`<br>设置子节点的对齐方式。Pos 枚举的值为 `TOP_LEFT`、`TOP_CENTER`、`TOP_RIGHT`、`CENTER_LEFT`、`CENTER`、`CENTER_RIGHT`、`BASELINE_LEFT`、`BASELINE_CENTER`、`BASELINE_RIGHT`、`BOTTOM_LEFT`、`BOTTOM_CENTER`、`BOTTOM_RIGHT`。 |

| `javafx.scene.layout.VBox` |
| --- |
| • `VBox(double spacing, Node... children)`<br>用给定的子节点构造一个垂直框，子节点之间以 spacing 参数指定的像素数分隔。 |

| `class javafx.scene.layout.Region` |
| --- |
| • `void setPadding(Insets value)`<br>设置此区域内容周围的内边距。 |

- **javafx.geometry.Insets**
  - `public Insets(double topRightBottomLeft)`
  - `public Insets(double top, double right, double bottom, double left)` 用给定的上、右、下、左像素数构造内边距。

- **javafx.scene.layout.GridPane**
  - `GridPane()` 构造一个空的网格面板。
  - `void add(Node child, int columnIndex, int rowIndex)`
  - `void add(Node child, int columnIndex, int rowIndex, int colSpan, int rowSpan)` 在指定位置添加节点。第二个方法使控件占据多个网格单元。若要占据所有剩余的行或列，可传入 `GridPane.REMAINING`。
  - `static void setHalignment(Node child, HPos value)` 设置给定节点在其网格单元内的水平对齐方式。`HPos` 枚举的值为 `LEFT`、`RIGHT` 和 `CENTER`。
  - `static void setValignment(Node child, VPos value)` 设置给定节点在其网格单元内的垂直对齐方式。`VPos` 枚举的值为 `TOP`、`CENTER`、`BASELINE` 和 `BOTTOM`。
  - `void setHgap(double value)`
  - `void setVgap(double value)` 将行或列之间的水平或垂直间距设置为给定的像素数。

### 13.4.2 FXML

JavaFX 用于描述布局的标记语言称为 FXML。我们将对其作较为详细的讨论，因为这些概念不仅对 JavaFX 有意义，而且其实现也相当通用。

下面是上一节中登录对话框的 FXML 标记：

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import java.lang.*?>
<?import java.util.*?>
<?import javafx.geometry.*?>
<?import javafx.scene.control.*?>
<?import javafx.scene.text.*?>
<?import javafx.scene.layout.*?>

<GridPane hgap="10" vgap="10">
    <padding>
        <Insets top="10" right="10" bottom="10" left="10"/>
    </padding>
    <children>
        <Label text="User name:" GridPane.columnIndex="0" GridPane.rowIndex="0"
            GridPane.halignment="RIGHT"/>
        <Label text="Password:" GridPane.columnIndex="0" GridPane.rowIndex="1"
            GridPane.halignment="RIGHT"/>
        <TextField GridPane.columnIndex="1" GridPane.rowIndex="0"/>
        <PasswordField GridPane.columnIndex="1" GridPane.rowIndex="1"/>
        <HBox GridPane.columnIndex="0" GridPane.rowIndex="2"
            GridPane.columnSpan="2" alignment="CENTER" spacing="10">
            <children>
                <Button text="OK"/>
                <Button text="Cancel"/>
            </children>
        </HBox>
    </children>
</GridPane>
```

仔细看一下 FXML 文件。注意用于导入 Java 包的“处理指令”`<?import . . . ?>`。（一般来说，XML 处理指令是应用程序特定处理 XML 文档的“逃生舱口”。）

现在来看文档的结构。首先，GridPane、标签和文本字段、HBox 及其按钮子节点的嵌套关系，反映了我们在上一节中使用 Java 代码构建的嵌套结构。

大多数属性对应于属性的 setter 方法。例如，

```xml
<GridPane hgap="10" vgap="10">
```

意思是“构造一个 GridPane，然后设置 hgap 和 vgap 属性。”

当属性以类名和静态方法开头时，将调用该方法。例如，

```xml
<TextField GridPane.columnIndex="1" GridPane.rowIndex="0"/>
```

意味着将调用静态方法 GridPane.setColumnIndex(thisTextField, 1) 和 GridPane.setRowIndex(thisTextField, 0)。

当属性值过于复杂而无法用字符串表示时，可以使用嵌套元素来代替属性。例如，

