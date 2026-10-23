

![](img/157fcf510c119278e4b1267c62717fa8_288_0.png)

## FIGURE 11.2: This shows a possible layout for the GUI that we want to build for editing recipes.

图 11.2：这展示了我们想要为编辑食谱而构建的 GUI 的一种可能布局。

The GUI should give the user the ability to add and remove recipes. They should be able to select recipes and edit the various information that we have on them.

GUI 应该使用户能够添加和删除食谱。他们应该能够选择食谱并编辑我们所拥有的各种信息。

At this point in the analysis you would probably want to sketch out a little picture of what you want the GUI to look like. That is done for this GUI in figure 11.2. The left side is taken up by a ListView that shows all the recipes. When the user clicks on a recipe, the information for it should be shown on the right. That includes a list of all the ingredients and the directions. The ingredients can also be edited and there need to be some buttons to help with this. The options for adding and removing recipes will be in the menus, which will be discussed in the next section.

在分析的这个阶段，你可能想要草拟一张小图，说明你希望 GUI 看起来是什么样子的。这在图 11.2 中已为此 GUI 完成。左侧由一个 ListView 占据，显示所有食谱。当用户点击一个食谱时，其信息应显示在右侧。这包括所有配料的列表和做法。配料也可以被编辑，并且需要一些按钮来帮助完成此操作。添加和删除食谱的选项将在菜单中，这些将在下一节讨论。

The question is how we should lay this out. Any GUI can be built in multiple different ways using the different panel and pane options that were listed above. For example, the separation between the recipe list and the information about the selected recipe could be created by a BorderPanel, a BoxPanel with a horizontal orientation, or a SplitPane. Which of these you pick will normally be determined by the way in which the panels would size things or whether you want to give the user the control of a SplitPane. We will use a BorderPanel for the top-level split. We will then use a SplitPane to separate the directions from the ingredient information. We will use two BorderPanels for the ingredient information and the Buttons will be built using a GridPanel. The settings area will also need to be refined a bit more. It probably just needs the name of the ingredient along with the amount needed. That can be laid out using a combination of BorderPanel and GridPanel.

问题是如何布局。任何 GUI 都可以使用上面列出的不同面板和窗格选项以多种不同的方式构建。例如，食谱列表与所选食谱信息之间的分隔可以通过 BorderPanel、具有水平方向的 BoxPanel 或 SplitPane 来创建。你选择哪一个通常取决于面板如何调整大小，或者你是否希望用户控制 SplitPane。我们将使用 BorderPanel 进行顶层分割。然后我们将使用 SplitPane 将做法与配料信息分开。我们将为配料信息使用两个 BorderPanel，并且按钮将使用 GridPanel 构建。设置区域也需要进一步细化。它可能只需要配料名称以及所需用量。这可以使用 BorderPanel 和 GridPanel 的组合来布局。

The code to do this is shown below. It is the full script and it is fairly long.

```
import scala.swing._
```

```
val recipeList=new ListView(List("Pop Tarts"))
val ingredientList=new ListView(List("Pop Tarts"))
val directionsArea=new TextArea("Toast the poptarts ...\nor don’t.")
val ingredientNameField=new TextField("Pop Tart")
val amountField=new TextField("1 packet")

val frame=new MainFrame {
  title="Recipe Book"
  contents=new BorderPanel {
    layout += (new ScrollPane(recipeList)
      -> BorderPanel.Position.West)
    layout += (new SplitPane(Orientation.Horizontal,
      new BorderPanel {
        layout += (new BorderPanel {
          layout += (new GridPanel(1,2) {
            contents+=Button("Add") (println("Add ingredient"))
            contents+=Button("Remove") (println("Remove ingredient"))
          } -> BorderPanel.Position.North)
          layout += (new ScrollPane(ingredientList)
            -> BorderPanel.Position.Center)
        } -> BorderPanel.Position.West)
        layout += (new BorderPanel {
          layout += (new GridPanel(2,1) {
            contents += new Label("Name")
            contents += new Label("Amount")
          } -> BorderPanel.Position.West)
          layout += (new GridPanel(2,1) {
            contents += ingredientNameField
            contents += amountField
          } -> BorderPanel.Position.Center)
        } -> BorderPanel.Position.Center)
      }, new ScrollPane(directionsArea)
    ) -> BorderPanel.Position.Center)
  }
  size=new Dimension(800,600)
}

frame.visible=true
```

The interactive elements were stored as values with names at the beginning. The purpose of that will become clear in section 11.3. Indentation has been used to indicate the nesting of panels and panes. Alternately, each different part could have been given a name as a value and then the parts could have been put together. The choice between these options is an issue of style. This example is just big enough, and the panels nested just deep enough that it could be worth considering breaking it up some with named constructs for some of the more deeply nested sections. Here is a different version that uses that approach.

交互元素在开头以带名称的值形式存储。其目的将在第 11.3 节中变得清晰。缩进已用于指示面板和窗格的嵌套。或者，每个不同的部分都可以作为值命名，然后将各部分组合起来。这两种选项之间的选择是风格问题。此示例足够大，并且面板嵌套足够深，以至于考虑使用命名结构拆分一些更深层的嵌套部分是值得的。下面是一个使用该方法的不同版本。

```
import scala.swing._

val recipeList=new ListView(List("Pop Tarts"))
val ingredientList=new ListView(List("Pop Tarts"))
val directionsArea=new TextArea("Toast the poptarts ...\nor don’t.")
val ingredientNameField=new TextField("Pop Tart")
val amountField=new TextField("1 packet")
```

```
val ingredientListPanel = new BorderPanel {
  layout += (new GridPanel(1,2) {
    contents+=Button("Add")(println("Add ingredient"))
    contents+=Button("Remove")(println("Remove ingredient"))
  } -> BorderPanel.Position.North)
  layout += (new ScrollPane(ingredientList)
    -> BorderPanel.Position.Center)
}

val ingredientDataPanel = new BorderPanel {
  layout += (new GridPanel(2,1) {
    contents += new Label("Name")
    contents += new Label("Amount")
  } -> BorderPanel.Position.West)
  layout += (new GridPanel(2,1) {
    contents += ingredientNameField
    contents += amountField
  }-> BorderPanel.Position.Center)
}

val frame=new MainFrame {
  title="Recipe Book"
  contents=new BorderPanel {
    layout += (new ScrollPane(recipeList)
      -> BorderPanel.Position.West)
    layout += (new SplitPane(Orientation.Horizontal,
      new BorderPanel {
        layout += (ingredientListPanel
          -> BorderPanel.Position.West)
        layout += (ingredientDataPanel
          -> BorderPanel.Position.Center)
      },
      new ScrollPane(directionsArea))
      -> BorderPanel.Position.Center)
  }
  size=new Dimension(800,600)
}

frame.visible=true
```

This second version would likely be preferred because the deepest nesting has been cut down two levels and the named values can help readers figure out what different parts of the code are doing. This can be taken further if you desire.

这个第二个版本可能更受欢迎，因为最深的嵌套减少了两层，并且命名值可以帮助读者弄清楚代码的不同部分在做什么。如果需要，可以进一步扩展。

When you run either of these scripts you get a window like what is shown in figure 11.3. In the code you might notice that each of the ListViews and the large TextArea are put inside of ScrollPanes. This is to make it so that if the lists get large or the directions get long, scroll bars will be added to allow the user to scroll around and see everything they need to.

运行这两个脚本中的任何一个，你都会得到一个像图 11.3 所示的窗口。在代码中，你可能会注意到每个 ListView 和大的 TextArea 都放在 ScrollPane 内。这样做是为了如果列表变大或做法变长，就会添加滚动条，让用户可以滚动查看所需的一切。

## 11.2.4 Menus

## 11.2.4 菜单

All we lack in the appearance of the GUI now is the menus. The MainFrame has a field called menuBar that we can set to be an object of type MenuBar. The MenuBar type has

现在 GUI 外观所缺少的只是菜单。MainFrame 有一个名为 menuBar 的字段，我们可以将其设置为类型为 MenuBar 的对象。MenuBar 类型具有

contents, like the panels and panes, but you should only add objects of the **Menu** type to a **MenuBar**.

contents，就像面板和窗格一样，但你只能向 **MenuBar** 添加 **Menu** 类型的对象。

The **Menu** objects are created with `new` and should be passed a `String` that you want as the title of the **Menu**. The `contents` of a **Menu** can be of one of five types.

**Menu** 对象使用 `new` 创建，并且应传递一个 `String` 作为 **Menu** 的标题。**Menu** 的 `contents` 可以是以下五种类型之一。

- * **MenuItem** - This is the most common thing you will put in a **Menu**. You create them with `new` and the easiest approach is to give them an `Action` object. The `Action` object can be made like a **Button** with a `String` and an action that is passed by-name. For example `new MenuItem(Action("Exit")(exit(0)))`.
- * **Menu** - You can add a **Menu** to a **Menu**. This will appear as a submenu when you run the program.
- * **CheckMenuItem** - Menus can also have options on them that are selected. To do this use the type **CheckMenuItem**. You make these with `new` and pass in a `String` for the text to display.
- * **RadioMenuItem** - If you have multiple values and you only want to allow one to be selected use a **RadioMenuItem**. These are made like **CheckMenuItems**. All the **RadioMenuItems** and you want to have grouped together should be added to a single object of the **ButtonGroup** type.
- * **Separator** - This is a simple component used to space items out to improve appearance and usability.

- * **MenuItem** - 这是你将放入 **Menu** 中最常见的内容。你使用 `new` 创建它们，最简单的方法是为它们提供一个 `Action` 对象。`Action` 对象可以像 **Button** 一样创建，具有一个 `String` 和一个按名称传递的操作。例如 `new MenuItem(Action("Exit")(exit(0)))`。
- * **Menu** - 你可以将一个 **Menu** 添加到另一个 **Menu**。运行时这将显示为子菜单。
- * **CheckMenuItem** - 菜单上也可以有被选中的选项。要做到这一点，请使用类型 **CheckMenuItem**。你使用 `new` 创建它们，并传入一个 `String` 作为要显示的文本。
- * **RadioMenuItem** - 如果你有多个值并且只想允许其中一个被选中，请使用 **RadioMenuItem**。它们像 **CheckMenuItems** 一样创建。你希望分组在一起的所有 **RadioMenuItems** 应该添加到一个类型为 **ButtonGroup** 的对象中。
- * **Separator** - 这是一个简单的组件，用于分隔项目以改善外观和可用性。

We can set up a simple menu system for our recipe script by adding the following code inside the `MainFrame` right before we set the `size`.

我们可以通过在设置 `size` 之前将以下代码添加到 `MainFrame` 内部，为我们的食谱脚本设置一个简单的菜单系统。

```
menuBar = new MenuBar {
    contents += new Menu("File") {
        contents += new MenuItem(Action("Open")(openFile))
        contents += new MenuItem(Action("Save")(saveFile))
        contents += new Separator
        contents += new MenuItem(Action("Exit")(exit(0)))
    }
    contents += new Menu("Recipe") {
        contents += new MenuItem(Action("Add")(addRecipe))
        contents += new MenuItem(Action("Remove")(removeRecipe))
    }
}
```

In order to get this to run, we have to put declarations of the four functions that are called in the script before we make `frame`. For now these can be left completely empty.

为了让它运行，我们必须在创建 `frame` 之前在脚本中放置四个被调用函数的声明。现在这些可以完全为空。

```
def openFile {
}

def saveFile {
}

def addRecipe {
}

def removeRecipe {
}
```

