

这可以添加到上面创建的简单 GUI 中，以添加一个可以通过 Alt-F 拉下的“文件”菜单，以及一个在菜单展开时按“X”即可执行的“退出”项。

## 11.4 FileChooser

GUI 库中至少还有一个值得指出的选项，因为它被使用得非常频繁，那就是文件选择对话框。许多程序在菜单中都有“打开”和“保存”选项。当选择这些选项时，程序通常会弹出一个对话框，允许用户浏览目录结构并选择文件。你可以自己编写对话框来实现此功能，但这需要大量的工作，而且这是一个如此常见的任务，以至于它已被添加到库中。

FileChooser 类型用于显示文件选择对话框。你可以带或不带一个用于起始目录的单个参数来创建一个新的 FileChooser。如果省略起始目录，它将使用默认目录开始。有三种以“show”开头的方法在 FileChooser 中，都可用于弹出对话框：showDialog、showOpenDialog、showSaveDialog。全部三个都接受第一个参数，即你希望对话框在其上方弹出的 Component。如果为该参数传递 null，对话框将出现在屏幕中央。showDialog 方法还接受第二个参数，即一个 String，将显示在确认按钮上。这些方法将返回以下其中之一：FileChooser.Result.Approve、FileChooser.Result.Cancel 或 FileChooser.Result.Error。如果返回 Approve，则 FileChooser 将在 selectedFile 和 selectedFiles 成员中具有有效值。

为了帮助理解这一点，请考虑以下在上一节中创建的菜单中添加的“打开”选项的示例。此选项可以通过在菜单栏的块中添加以下代码添加到菜单中。

```
contents += new MenuItem(Action("Open")(openFile)) {
    mnemonic = Key.O
}
```

要使此功能正常工作，我们需要一个 openFile 函数。它可以按以下方式定义，并放置在 list 和 field 的声明之后以及 frame 之前。

```
def openFile {
    val chooser = new FileChooser
    if(chooser.showOpenDialog(list)==FileChooser.Result.Approve) {
        list.listData = Source.fromFile(chooser.selectedFile).getLines.toList
    }
}
```

此代码创建一个 FileChooser 并显示一个打开对话框。如果用户选择了一个文件，则该文件用于打开一个 Source，并且从该 Source 中获取的行被转换为一个 List，该 List 被设置为 ListView 的数据。

## 11.5 Tables

Swing 中更复杂的 GUI 元素之一是 Table。名称很好地描述了此元素的功能。它呈现用户可以交互的二维数据单元格网格。虽然 scala.swing.Table 类型可以轻松提供基本功能，但 javax.swing.Table 类型可以做更多的事情，这需要你进入原始的 Java 库。因此，本节专门讨论此组件。

当你创建一个 scala.swing.Table 时，有三种传递给它的参数选项。你可以告诉它在表中放置多少行和列作为两个 Int 参数。这将创建一个指定大小的简单表格，所有元素都是空白的。你可以通过在 REPL 中输入以下代码来尝试此操作。

```
val frame = new Frame {
  title = "Table Test"
  contents = new Table(3,4)
}
frame.visible = true
```

此代码将弹出一个窗口，其中包含一个具有 3 行 4 列且所有单元格为空的 Table。此示例使用 Frame 而不是 MainFrame，因为它 intended 在 REPL 中完成。如果使用 MainFrame，关闭窗口时整个 REPL 将被终止。

你也可以传入参数 rowData: Array[Array[Any]]、columnNames: Seq[_]。这将创建一个具有 rowData 大小的表格并以这些值开始。记住从图 7.1 中 Any 是 Scala 中可以表示任何其他类型的类型。你的 Table 不必包含 String 数据。它们可以更复杂，但我们在这里不会涉及所有这些细节。第二个参数是一个序列，其中包含你希望出现在列顶部作为标签的值。这些标签只有在表格嵌套在 ScrollPane 中时才会出现。

要测试其工作原理，请尝试在 REPL 中输入以下内容。

```
val data = Array(Array(1,2,"hi"),Array(3,4,"bye"))
val colHeads = Seq("Num","Num","Word")
val frame = new Frame {
  title = "Table Test"
  contents = new Table(data,colHeads)
}
frame.visible = true
```

这将弹出一个小窗口，其中包含一个具有两行三列的 Table。请注意，列标题在此版本中未出现。要获取列标题，请将设置 Frame 内容的代码行更改为以下内容。

```
contents = new ScrollPane(new Table(data,colHeads))
```

现在当你使 Frame 可见时，你会得到一个更大的窗口，其中包含相同的表格，只是现在列标题可见。

构建 Table 的第三种方式根本不传递任何参数。如果你选择此选项，你将需要做更多的工作来设置，因此现在我们将重点关注其他选项。

如果你在 REPL 中使用上述示例创建的 Table 进行操作，你可能会发现你可以选择单元格、使用箭头键移动，甚至

编辑单元格中的值。要在代码中处理 Table，我们需要有一个名称来引用 Table。我们可以通过稍微修改代码来实现这一点，以便我们有一个名为 `table` 的变量。

```
val table = new Table(data,colHeads)
...
  contents = new ScrollPane(table)
...
```

要从表中获取值，只需用行和列对其进行索引。因此，如果你在 REPL 中执行以下行，你将看到左上角单元格的值。

```
println(table(0,0))
```

如果你在创建表后立即执行此操作，你将获得值 1。但是，如果你手动编辑该单元格中的 Table 然后打印它，你将看到修改后的值。你可以用相同的方式修改 Table 中的值。只需按行和列索引对 Table 进行赋值。尝试在 REPL 中执行以下操作。

```
table(1,1) = "New text"
```

你会看到 Table 中单元格 (1,1) 的值在图形上更新以反映更改。此方法只能用于修改 Table 正常范围内的单元格。如果你超出首次创建 Table 时设置的大小，你将收到错误。如果你在 REPL 中尝试输入 `table(0,0)`，你将获得类型为 Any 的结果。这可能有点问题，因为你可以用 Any 类型做的事情并不多。例如，你可能会尝试执行以下操作。

```
table(0,0)+table(1,0)
```

对于任何数值类型或 String 类型，这种加法都完全可以正常工作，因为所有这些类型都为其定义了 `+` 方法。但是，如果你尝试这样做，你将收到以下错误消息。

```
<console>:12: error: type mismatch;
 found   : Any
 required: String
        table(0,0)+table(0,0)
                    ^
```

这是因为 Any 类型没有 + 方法。这是有道理的，因为有一些符合 Any 的类型你不应该能够使用 +。要对从表中获取的值做任何事情，我们必须调用存在于 Any 上的方法。挑战在于这些方法并不多。你可以检查相等或不相等，进行将在第 21 章讨论的多线程相关操作，检查对象的实际类型，或将对象转换为 String。后两种方法可以提供我们想要的功能。我们将重点关注最后一种方法，因为它只使用我们之前见过的方法。

要将任何对象转换为 String，调用 `toString` 方法。你可以尝试以下操作来了解其工作原理。

```
table(0,0).toString
```

一旦你这样做了，你就可以使用 + 来进行 String 拼接。如果你想做

