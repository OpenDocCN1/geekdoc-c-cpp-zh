

对 Table 中的值进行数值运算时，可以对 String 使用 toInt 或 toDouble。因此，如果你想乘以两个表值，可以这样做。

```
table(0,0).toString.toDouble * table(1,0).toString.toDouble
```

这有点冗长，但这是我们为能够在 Table 中放置各种不同类型事物所付出的代价。

如果你足够多地尝试这个，你很可能会遇到这种方法的首要缺陷，如果单元格的内容不是数字，这将失败。为了避免这种情况，你需要使用 try/catch 构造。我们将在第 22.3 节详细讨论 try-catch。现在我们将给出一个简要介绍。你可能已经看到，当语句出错时，你得到的错误消息通常以提供一个包含单词“Exception”的类型名称开头。EXCEPTION 是一个表示问题的对象，当出现问题时代码会 THROW 一个异常。如果你知道这种情况可能会发生并且你想处理它，你就告诉 Scala 你想 TRY 一些代码，然后如果发生异常就 CATCH 它。可以捕获的异常用 cases 指定，就像 match 表达式一样。

Scala 中的 try-catch 可以用作表达式。如果没有异常，你会得到你尝试执行的代码的值。如果有异常并且有一个匹配的 case，值将是该 case 中发生的情况。为了帮助你理解这一点，请考虑以下函数。

```
def asDouble(a:Any):Double = {
  try {
    if(a==null) 0.0 else a.toString.toDouble
  } catch {
    case e:NumberFormatException => 0.0
  }
}
```

此函数接受一个 Any 对象并为其返回一个数字。如果值为 null，则返回零。否则，它使用上面所示的 .toString.toDouble 方法调用。在此函数中，该代码放在 try 中，它会捕获 NumberFormatException。正如名称所示，这是当你尝试将某些格式不正确的内容制作成数字时发生的异常。如果发生这种情况，case 会返回值为 0.0。上面的和现在可以用这种方式表示。

```
asDouble(table(0,0))+asDouble(table(1,0))
```

如果 Table 单元格包含非数字内容，此代码更健壮，因为它不会因异常而停止，而是为该单元格使用 0.0。

### 11.5.1 Table Actions

你现在知道如何设置 Tables 以及如何读取和更改其中的值。对于许多应用程序来说，这已经足够了。GUI 中的操作通常可以通过让用户点击按钮或选择菜单项来启动，并由该操作启动的代码利用表中的值。然而，有些应用程序需要实际响应 Table 本身发生的事件。在这种情况下，你需要监听 Table 或可能 Table 中的 selection 对象。

Tables 可以发生的事件有一个相当长的列表。你可以在 API 中查找完整信息，但这里列出了主要的一些。

- `TableChanged` – 表示 Table 的结构保持不变，但其他任何内容都可能已更改。
- `TableColumnsSelected` – 表示当前选中的列发生变化。
- `TableRowsAdded` – 当向 Table 添加额外行时发生此事件。
- `TableRowsRemoved` – 当从 Table 中删除行时发生此事件。
- `TableRowsSelected` – 表示当前选中的行发生变化。
- `TableStructureChanged` – 此事件表示最一般类型的更改。Table 中的任何内容都可能已更改，包括行数和列数。
- `TableUpdated` – 表示 Table 指定部分中的值已更改。

要获取指示选择更改的事件，请监听 `table.selection`。要获取其他事件，只需监听 `table`。

如果你只关心单元格值何时被更改，可以使用如下代码。

```
import scala.swing._
import scala.swing.event._

val sumLabel = new Label("0.0")
val table = new Table(8,5)

def asDouble(a:Any):Double = {
  try {
    if (a==null) 0.0 else a.toString.toDouble
  } catch {
    case e:NumberFormatException => 0.0
  }
}

val frame = new MainFrame {
  contents = new BorderPanel {
    layout += sumLabel -> BorderPanel.Position.North
    layout += table -> BorderPanel.Position.Center
  }
  size = new Dimension(500,400)
  listenTo(table)
  reactions += {
    case e:TableUpdated =>
      val sum = (for(i <- 0 until table.rowCount;
        j <- 0 until table.model.getColumnCount) yield {
          asDouble(table(i,j))
      }).sum
      sumLabel.text = sum.toString
  }
}

frame.visible = true
```

此代码以一个空 Table 和一个显示 0.0 的 Label 开始。每当用户编辑一个单元格时，代码会遍历所有单元格并将每个单元格中的值相加，如果没有有效数字则使用零。它更改 Label 以反映此总和。将此代码输入到文件中并作为脚本运行。进行更改以查看还能做什么。

```
case Some(name) =>
    data = data.map(_ :+ "")
    headers :+= header.get
    table.model = new DefaultTableModel(data,headers)
case None =>
}
}
```

```
val frame = new MainFrame {
    title = "Resizable Table"
    contents = new ScrollPane(table)
    menuBar = new MenuBar {
        contents += new Menu("File") {
            contents += new MenuItem(Action("Add Column")(addColumn))
            contents += new Separator
            contents += new MenuItem(Action("Exit")(sys.exit(0)))
        }
    }
    size = new Dimension(500,500)
}

frame.visible = true
```

Table 的信息存储在 data 和 headers 中。为了与构建 DefaultTableModel 所需的类型相匹配，它们分别是 Array[Array[AnyRef]] 和 Array[AnyRef]。不幸的是，这些类型不能使用正常的 Scala 创建方法，因此而不是传递 data，table 的声明中包含一行设置模型的代码。

table 监听自身并对 TableUpdated 事件做出反应。更新的数据始终存储回 data 数组。请注意，这需要做一些额外的工作，因为从 table 中提取的数据类型为 Any。使用了 match 来确保我们拥有 AnyRef。还有一个检查以查看正在更改的行是否是最后一行。在这种情况下，会将新行附加到 data 并更新模型。

addColumn 方法由菜单选项调用。它使用 Dialog.showInput 提示用户输入名称，然后在每一行的末尾附加一个空白并将其用作更新后的 data。它还将新的 header 名称附加到 headers 的末尾。它最后要做的是更新 table 模型。showInput 的完整签名如下。

```
def showInput [A] (parent: Component, message: Any, title: String, messageType: Value, icon: Icon, entries: Seq[A], initial: A): Option[A]
```

在我们的使用中，我们让对话框框在 table 上方弹出。我们告诉它我们是在提问，没有图标，没有条目，初始值为一个空 String。这让用户可以输入他们选择的 String。如果 entries 不为空，用户将获得下拉框而不是文本字段。

请注意 showInput 返回一个 Option 类型。这是因为用户可能会点击“取消”或关闭对话框。这是使用 match 的原因。如果用户没有提供适当的响应，Option 为 None 且不会执行任何操作。

此代码未演示删除行或列，但任一操作都可以用 patch 以与此处所示非常相似的方式完成。

## 11.6 Putting it Together

我们现在可以将 GUI 的各个方面组合到食谱书脚本中。之前我们构建了一个 GUI 并向其添加了菜单。然而，GUI 并不是交互式的。点击各个元素不会对 GUI 的其他元素做任何事情。现在我们知道如何使 GUI 交互式，我们可以向此脚本添加适当的 functionality。为了能够做到这一点，我们首先需要做一些基础工作。特别是，我们需要一种很好的方式来存储与食谱相关联的信息。这需要一些 case classes。

我们 definitely 想要一个 case class 来表示食谱。由于食谱可以包含多个配料，因此拥有一个配料的 case class 也是有利的。这导致了如下内容。

```
case class Ingredient(name:String,amount:String)
case class Recipe(name:String,ingredients:List[Ingredient],directions:String)
```

你可以将它放在脚本顶部，因为脚本的其他许多部分都会参考它。

我们还需要一种方法来存储多个食谱。我们将使用一个 Recipes 数组的变量声明。也可以选择使用 var List，但其中一些交互需要交换值，而其他交互可能需要直接访问。两者都将更容易且更高效地使用 Array。添加新食谱的操作对于 List 来说会更容易，但该操作可能发生的频率较低，并且几乎可以像使用 Array 一样轻松完成。

```
var recipes = Array(Recipe("Pop Tarts",List(Ingredient("Pop Tart","1 packet")),"Toast the poptarts ...\nor don't."))
```

```
val recipeList = new ListView(recipes.map(_.name))
val ingredientList = new ListView(recipes(0).ingredients.map(_.name))
val directionsArea = new TextArea(recipes(0).directions)
val ingredientNameField = new TextField(recipes(0).ingredients(0).name)
val amountField = new TextField(recipes(0).ingredients(0).amount)
```

此代码包括数组的声明以及使用数组中一个 Recipe 的活动组件声明的修订。

现在我们已经设置好了，我们可以从完成由菜单调用的函数开始。我们将从 saveFile 函数开始，因为它定义了我们将在文件中使用的格式，而且它有点更容易。

```
def saveFile {
  val chooser = new FileChooser
  if(chooser.showSaveDialog(recipeList)==FileChooser.Result.Approve) {
    val pw = new PrintWriter(chooser.selectedFile)
    pw.println(recipes.length)
    for(r <- recipes) {
      pw.println(r.name)
      pw.println(r.ingredients.length)
      for(ing <- r.ingredients) {
        pw.println(ing.name)
        pw.println(ing.amount)
      }
    }
  }
}
```

