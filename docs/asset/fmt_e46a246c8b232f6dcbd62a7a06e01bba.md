
GUI 设置通过将方向设置为 `TextArea` 并结束，然后使用 `SplitPane` 和 `BorderPane` 将部分组合在一起。`BorderPane` 被设置为 `Scene` 的 `root`（根节点），这样它就会随窗口调整大小。

GUI 设置之后是若干函数，它们在 GUI 发生变化或点击按钮和菜单项时被调用。这些包括在文本文件中保存和加载存储食谱的函数，以及添加和删除食谱及配料的函数。

第 165-177 行的 `addRecipe` 代码使用了我们之前没过的另一个特性。它需要询问用户新食谱的名称，因为我们没有在 GUI 中提供编辑的方法。为了实现这一点，它使用了来自控制包的类型 `InputDialog`。如名所示，该类允许我们弹出一个对话框从用户处读取文本。创建对话框后，我们设置了标题、头部文本和内容。当我们调用 `showAndWait` 方法时，它会等待用户点击“确定”或“取消”。结果是一个 `Option`，可能是某个值或 `None`。由于我们不想在用户选择“取消”时执行任何操作，因此使用 `foreach` 调用来处理他们的输入。`foreach` 会忽略 `None`。

还有一个 `ChoiceDialog` 允许用户从多个选项中选择。读者可以。

## 使用 Scala 进行编程和解决问题的简介

## 食谱

| 文件 | 食谱 | | | |

|---|---|---|---|---|

| Pop Tarts | 添加 | 删除 | 名称: Pop Tart | |

| | Pop Tart | 数量: 1 包 | | |

| | | | | |

| ... | | | | |

| | 烤 poptarts ... 或者不烤。 | | | |

**图 11.19:** 这显示了运行 `Recipe.scala` 时产生的窗口。

## GUIs

# GUI 323

```scala
ingredientNameField.text.onChange {
  val newName = ingredientNameField.text.value
  val ingredientIndex =
    ingredientsList.selectionModel.value.selectedIndex
  if (ingredientIndex>=0) ingredientsList.items.value(ingredientIndex) = newName
}

// 方向说明
val directionsA = new TextArea

val splitPane = new SplitPane
splitPane.orientation = scalafx.geometry.Orientation.Vertical
splitPane.items += ingredientsGrid
splitPane.items += directionsA

// 顶层布局
val topBorderPane = new BorderPane
topBorderPane.top = menuBar
topBorderPane.left = recipeList
topBorderPane.center = splitPane

root = topBorderPane
```

```scala
def createFile:Unit = {
  val chooser = new FileChooser
  val selected = chooser.showDialog(stage)
  if (selected!=null) {
    val src = io.SourceFrom(selected)
    val lines = src.getlines
    recipes = Array.fill(lines.next.toInt)(Recipe(
      StringProperty(lines.next),
      List.fill(lines.next.toInt)(Ingredient(StringProperty(lines.next)),
      StringProperty(lines.next))),
      {
        var dir = ""
        var line = lines.next
        while (line!=".") {
          dir += (if (dir.isEmpty) "" else "\n")+line
          dir = lines.next
        }
        StringProperty(dir)
      })
    src.close()
    recipeList.items = ObservableBuffer(recipes.map(_.name.value):*)
    recipeList.selectionModel.value.selectFirst
    bindRecipeFields(recipes.head)
  }
}
```

```scala
def createFile:Unit = {
  val chooser = new FileChooser
  val selected = chooser.showDialog(stage)
  if (selected!=null) {
```

# 使用 Scala 进行编程与问题解决

```scala
val pw = new PrintWriter(selected)
println(r.recipes.length)
for (r <- r.recipes) {
  pw.println(r.name)
  pw.println(r.ingredients.length)
  for (ing <- r.ingredients) {
    pw.println(ing.name)
    pw.println(ing.amount)
  }
  pw.println(r.directions)
  pw.println(".")
}
pw.close()
```

```scala
def addRecipe:Unit = {
  val dialog = new TextInputDialog
  dialog.headerText = "Recipe Name"
  dialog.contentText = "新食谱的名字是什么？"
  dialog.showAndWait().foreach { name ->
    recipes += StringProperty(name),
    List(StringProperty("ingredient"),
    StringProperty("amount"), StringProperty("Directions"))
    recipeList.items = ObservableBuffer(recipes.map(_.name).value*)
    recipeList.selectionModel.value.clearAndSelect(recipes.length-1)
  }
}
```

```scala
def removeRecipe:Unit = {
  if (recipeList.selectionModel.value.selectedItems.isEmpty) {
    recipes = recipes.patch(recipeList.selectionModel.value.selectedIndex,
    null,1)
    recipeList.items = ObservableBuffer(recipes.map(_.name).value*)
    recipeList.selectionModel.value.clearAndSelect()
  }
}
```

```scala
def addIngredient:Unit = {
  val recipeIndex = recipeList.selectionModel.value.selectedIndex.value
  if (recipeIndex>0) {
    val newIng = Ingredient(StringProperty("Stuff"), StringProperty("Some"))
    recipes(recipeIndex) = recipes(recipeIndex).copy(
    ingredients = recipes(recipeIndex).ingredients += newIng
    recipeList.items.value += newIng.name.value
  }
}
```

```scala
def removeIngredient:Unit = {
  val recipeIndex = recipeList.selectionModel.value.selectedIndex.value
  val ingredientIndex =
    ingredientsList.selectionModel.value.selectedIndex
  if (recipeIndex>0 && ingredientIndex>0) {
    recipes(recipeIndex) = recipes(recipeIndex).copy(ingredients =
```

## GUI

```scala
recipes(recipeIndex).patch(ingredientIndex,Nil,1))
bindRecipeFields(recipeIndex)
```

```scala
def bindRecipeFields(r:Recipe):Unit = {
  ingredientsList.items = ObservableBuffer(r.ingredients.map(_.name.value):*)
  selectedRecipe.foreach(_.directions.unbind)
  directionsArea.text = r.directions.value
  r.directions <= directionsArea.text
  selectedRecipe = Some(r)
}
```

```scala
def bindIngredientFields(ingr:Ingredient):Unit = {
  selectedIng.foreach { si =>
    s.name.unbind
    ingredientField.text = ingr.name.value
    ingr.name <= ingredientField.text
    amountField.text = ingr.amount.value
    ingr.amount <= amountField.text
    recipes.foreach(println)
    selectedIng = Some(si)
  }
}
```

```scala
app.main(args)
```

你可以看到我们在上面的代码中消除了 `AlterSelectedIngredient` 函数，但除了用于食谱的函数外，我们在绑定原料时又做了另一个函数。绑定在某些方面简化了代码，但它们引入了一个显著的复杂性。当我们从一个食谱切换到另一个食谱时，必须解绑不再被选中的值。这需要两个变量来存储我们绑定的内容。由于程序启动时尚未绑定任何内容，因此这些地方使用了 `Option` 类型。

使用绑定的方法在绑定内容变化极少时通常效果最好，因此这并不是它们的理想应用场景。在编写自己的 GUI 时，鼓励你使用任何最符合逻辑的方法。

## 章节结束

### 概念总结

- 如今大多数与之交互的程序都具有图形用户界面（GUI）。

- 我们可以使用 JavaFX 库在 Scala 中编写 GUI，尽管这一事实在我们的代码中通常并不明显。

# 使用 Scala 进行编程与问题解决

GUI 的元素被称为“节点”（`Nodes`）。ScalaFX 库中有许多不同的活动和被动活动节点。你应该查阅 API 以查看所有可用内容。

- 为了表示窗口，你可以使用 `Stage` 或 `Dialog` 类型。

- 有许多从简单的 `Button` 到复杂的 `TableView` 的不同节点。

- 复杂的 GUI 是使用 `Panes` 构建的。这些窗格可以包含其他节点，包括其他 `Panes`。

- 不同的 `Pane` 对其内容的放置和尺寸调整有不同的规则。`MenuBar` 包含多种类型，包括 `MenuItem`。

- 不同的窗格对于其内容的放置和尺寸调整有不同的规则。`MenuBar` 包含多种类型，包括 `MenuItem`。

- 不同的窗格对于其内容的放置和尺寸调整有不同的规则。`MenuBar` 包含多种类型，包括 `MenuItem`。

- 不同的窗格对于其内容的放置和尺寸调整有不同的规则。`MenuBar` 包含多种类型，包括 `MenuItem`。

## 自学练习

GUI 无法通过 REPL 完成。

- 1. 使用 `ComboBox` 和 `TextField` 编写一个评分器。

- 2. 使用 `TextArea` 编写一个可以打开和保存文件的编辑器。

- 3. 使用 `TableView` 编写一个可以显示 CSV 文件的 GUI，将其导出到 CSV 格式。

- 4. 使用 `Grid` 编写一个三字棋游戏。

- 5. 使用 `Pane` 编写一个可以设置选项的 GUI。

- 6. 使用 `Slider` 和 `TextField` 编写一个可以执行操作的 GUI。

- 7. 使用 `Slider` 和 `TextField` 编写一个可以显示结果的 GUI。

- 8. 使用 `ListView` 和 `Button` 编写一个可以进行加减操作的 GUI。

- 9. 使用 `ListView` 和 `Checkbox` 编写一个可以显示大写、小写和数字的 GUI。

- 10. 使用 `RadioButton` 和 `ToggleGroup` 编写一个只能选择一个选项的 GUI。

## 项目

- 1. 编写一个 GUI 计算器。你可以通过 http://www.online-calculator/ 了解它是如何工作的。

- 2. 如果你做过 8.5 解析化学方程式，你也可以考虑这个问题。不需要化学解析器，所以你可以从这里开始。事实上，线性方程将构建一个 GUI 来表示矩阵，然后对其进行基础的加法运算。保持简单，矩阵将是正方形。你应该有一个菜单选项让用户设置矩阵的大小。它们至少应该是 2x2。GUI 将显示名为 A、B、C 的三个矩阵。用户输入 A 和 B 的值。当用户选择加法选项时，设置 C 的值。

- 3. 编写一个玩扫雷游戏的 GUI。你可以使用 `GridPane` 或 `TilePane` 用于显示和用户交互。这个项目的挑战在于如何显示雷并与 `Button` 关联。学生应该考虑不同的方法，而不是直接冲进去。

- 4. 这个项目延续了光线追踪选项。你应该构建一个允许你编辑场景的 GUI。你应该有一个球体、行星和光源的 `ListView`。每个都具有几何设置以及颜色信息。你需要菜单选项来保存文件或加载文件。

- 5. 在 10.3 中使用基础文本编辑器编辑地图遍历房间是具有挑战性的且容易出错的。有一个允许你编辑房间的 GUI 将非常有帮助。它可以显示一个房间的 `ListView`，你可以选择它，然后有设置房间值的其他选项。你需要加载文件、保存文件和添加房间的菜单选项。为了增加额外挑战，考虑放入删除房间的选项。注意，当你这样做时，所有房间的索引将保持不变。

- 6 你可以扩展 10.8。在这个项目中，你将编写一个允许用户对喜欢的歌曲进行排序的 GUI。你应该有一个允许用户对每首歌进行五星级评分的元素。你还应该有 元素让用户选择最喜欢的歌曲并放入前十 `ListView` 中。

# 使用 Scala 进行编程和问题解决介绍

同时也能够从前 10 的 `ListView` 中移除歌曲。为用户提供保存和加载新排名文件的菜单选项。

- 7. 编写一个显示音乐数据库的程序。你希望为不同的歌曲存储重要信息，包括歌曲名称、艺术家、专辑、发行年份以及你认为认为的任何其他内容。该程序应该能够显示所有歌曲的信息，并允许用户缩小范围到特定的艺术家、专辑、年份等。

- 8. 对于此项目，我们想要将项目 10.4 中基于菜单驱动的脚本转换为 GUI 程序。你可以使用 `ListView` 或 `Table` 来显示与食品储物和食谱项目相关的信息。你需要设置用于保存和加载的菜单选项。与基于菜单的版本一样，用户应该能够向食品储物中添加项目、检查是否可以制作某道菜谱，并告诉程序他们已经制作了该菜谱，且从他们的食品储物中删除了相应的数量。具体实现细节以及大部分功能是使用 `Buttons` 还是 `MenuItems` 来实现，由你决定。

- 9. 本章没有使用在该项目构思中出现的主题公园示例。你应该使用 GUI 实现主题公园功能，并在 `TabPane` 中使用不同的标签页来代表公园的不同区域。GUI 应该至少包含以下标签页：“票务 (Ticket Sales)”、“食品销售 (Food Sales)”和“游乐操作 (Ride Operation)”。

对于前两个，你有用户可以点击的按钮将项目添加到购买列表中。在票务标签页上，这些包括不同年龄的人、是否要去公园以及各种冷藏箱。对于食品购买，有不同类型的食物及其尺寸。你可以在第 66 页找到价格。所有购买项目都应添加到 `ListView` 中。还应该有一个 `Button` 来移除选中的项目。

在游乐操作标签页上，你需要一个 `ComboBox` 来选择游乐项目，一个 `TextField` 来输入一段时间内游玩的人数，以及一个用于提交数据的 `Button`。

- 10. 对于此项目，你将把项目 10.5 中基于文本菜单程序的功能转换为 GUI。你可以决定 GUI 的具体格式，但你应该有一个显示感兴趣课程的 `ListView`，并具备添加和删除条目的能力以及编辑条目值的能力。课程应该至少与课程编号、名称、级别和时间段相关联。
