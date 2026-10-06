

## GUIs 319

```scala
}
def removeIngredient: Unit = {
    val recipeIndex = recipeList.selectionModel.value.selectedIndex
    val ingredientIndex = =
        ingredientsList.selectionModel.value.selectedIndex
    if(recipeIndex>0 && ingredientIndex>0) {
        recipes(recipeIndex).copy(ingredients =
            recipes(recipeIndex).patch(ingredientIndex,Nil,1))
        setFields(recipes(recipeIndex))
    }
}
def setFields(r:Recipe):Unit = {
    ingredientsList.items.value.clear
    ingredientsList.items.value += r.ingredients.map(_)
    directionsArea.text = r.directions
    ingredientName.text = ""
}
def alterSelectedIngredient(diff: Ingredient => Ingredient):Unit = {
    val recipeIndex = recipeList.selectionModel.value.selectedIndex
    val ingredientIndex = =
        ingredientsList.selectionModel.value.selectedIndex
    if(recipeIndex>0 && ingredientIndex>0) {
        val newIngredient =
            diff(recipes(recipeIndex).ingredients(ingredientIndex))
        val newRecipe = recipes(recipeIndex).copy(ingredients =\
            recipes(recipeIndex).ingredients.updated(ingredientIndex,
            newIngredient))
        recipes(recipeIndex) = newRecipe
    }
}
app.main(args)
```

运行此代码创建的 GUI 可以在图 11.19 中看到。这是一个长程序，我们将逐部分考虑。第 1-12 行包含了我们需要导入，大部分来自 ScalaFX 库，但也包含了用于将食谱保存文件的 `java.io.PrintWriter`。第 14 和 15 行包含了用于存储食谱书的类。

第 21-117 行是 GUI 设置。其中包含了关于处理 GUI 不同部分的注释。菜单部分和食谱列表部分非常直观。注意第 45 行声明了一个存储在内存中食谱的 `var Array`。它被 GUI 的其他元素广泛使用。

显示配料信息的 GUI 部分使用了 `GridPane`，并且稍微长一些。与用户的交互包括在用户选择不同配料时更改 `TextField`，以及在他们编辑字段时更改数据。注意，与之前的示例不同，这段代码会响应 `TextField` 及其下方 `TextArea` 实际文本的变化。这是因为处理更改的代码引用了 `ListView` 中选中的索引。如果用户点击两个 `ListView` 之一的另一个选项导致失去焦点，这些索引会在处理焦点更改之前更新。结果是，所有的更改都会被记录下来。监听**文本**的每处变化效率较低，但它能防止任何更改丢失。

**onChange** 代码使用了下方一个名为 **alterSelectedIngredient** 的函数来防止代码重复。该函数接受单个参数，其类型为函数 **Ingredient => Ingredient**。该函数返回一个修改后的配料，以存回列表。如果你查看第 220-230 行 **alterSelectedIngredient** 的定义，你会发现我们使用了一个之前没过的 List 方法 **updated**。该方法的行为是在特定索引处用指定的值替换 List 中的一个元素。这被用于通过用传入的替换掉旧的来修改选中的食谱。

GUI 设置通过将方向设置为 **TextArea** 并结束，然后使用 **SplitPane** 和 **BorderPane** 将部分组合在一起。**BorderPane** 被设置为 **Scene** 的 *root*（根节点），这样它就会随窗口调整大小。

GUI 设置之后是若干函数，它们在 GUI 发生变化或点击按钮和菜单项时被调用。这些包括在文本文件中保存和加载存储食谱的函数，以及添加和删除食谱及配料的函数。

第 165-177 行的 **addRecipe** 代码使用了我们之前没过的另一个特性。它需要询问用户新食谱的名称，因为我们没有在 GUI 中提供编辑的方法。为了实现这一点，它使用了来自控制包的类型 **InputDialog**。如名所示，该类允许我们弹出一个对话框从用户处读取文本。创建对话框后，我们设置了标题、头部文本和内容。当我们调用 `showAndWait` 方法时，它会等待用户点击“确定”或“取消”。结果是一个 `Option`，可能是某个值或 `None`。由于我们不想在用户选择“取消”时执行任何操作，因此使用 `foreach` 调用来处理他们的输入。`foreach` 会忽略 `None`。

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

**图 11.19:** 这显示了运行 Recipe.scala 时产生的窗口。

## GUIs

