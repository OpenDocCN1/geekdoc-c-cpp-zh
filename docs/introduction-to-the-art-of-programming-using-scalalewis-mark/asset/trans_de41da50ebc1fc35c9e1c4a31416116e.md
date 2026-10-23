

```
val rIndex = recipeList.selection.leadIndex
val iIndex = ingredientList.selection.leadIndex
changeIngredientName(rIndex,iIndex)
}
} else if(e.source==amountField) {
if(!recipeList.selection.items.isEmpty &&
!ingredientList.selection.items.isEmpty) {
val rIndex = recipeList.selection.leadIndex
val iIndex = ingredientList.selection.leadIndex
changeAmount(rIndex,iIndex)
}
}
```

这段代码适用于 `directionsArea` 和选择食材。它还为两个不同的 `TextField` 设置了相关内容，所以我们剩下的就是编写两个函数。在 `FocusLost` 的情况下，代码会检查事件的来源。事件的来源是它发出的组件。如果是 `directionsArea`，它会按此处所示的方式修改食谱。食材的修改是通过以下这些函数完成的。

```
def changeIngredientName(r:Int,i:Int) {
  val ing = recipes(r).ingredients(i)
  recipes(r) = recipes(r).copy(ingredients = {
    recipes(r).ingredients.patch(i,List(Ingredient(
      ingredientNameField.text,ing.amount)),1)
  })
  ingredientList.listData = recipes(r).ingredients.map(_.name)
  ingredientList.selectIndices(i)
}
def changeAmount(r:Int,i:Int) {
  val ing = recipes(r).ingredients(i)
  recipes(r) = recipes(r).copy(ingredients = {
    recipes(r).ingredients.patch(i,List(Ingredient(
      ing.name,amountField.text)),1)
  })
}
```

`patch` 在这里再次被使用，但这次被修补的列表包含一个修订后的食材。

所有这些不同的部分组合成一个单一的脚本。为了帮助你了解它们是如何组合在一起的，这里是完整的脚本。

```
import scala.swing._
import scala.swing.event._
import java.io.PrintWriter
import scala.io.Source

case class Ingredient(name:String,amount:String)
case class Recipe(name:String,ingredients:List[Ingredient],directions:String)

var recipes = Array(Recipe("Pop Tarts",List(Ingredient("Pop Tart","1 packet")),
"Toast the poptarts ...\nor don’t."))
val recipeList = new ListView(recipes.map(_.name))
val ingredientList = new ListView(recipes(0).ingredients.map(_.name))
val directionsArea = new TextArea(recipes(0).directions)
```

```
val ingredientNameField = new TextField(recipes(0).ingredients(0).name)
val amountField = new TextField(recipes(0).ingredients(0).amount)

def setFields(r:Recipe) {
    ingredientList.listData = r.ingredients.map(_.name)
    directionsArea.text = r.directions
    if(r.ingredients.isEmpty) {
        ingredientNameField.text = ""
        amountField.text = ""
    } else {
        ingredientNameField.text = r.ingredients.head.name
        amountField.text = r.ingredients.head.amount
    }
}

def setIngredients(ingr:Ingredient) {
    ingredientNameField.text = ingr.name
    amountField.text = ingr.amount
}

def addIngredient {
    if(!recipeList.selection.items.isEmpty) {
        val index = recipeList.selection.leadIndex
        val oldIngrs = recipes(index).ingredients
        val newIngr = Ingredient("Stuff", "Some")
        recipes(index) = recipes(index).copy(ingredients=oldIngrs:+newIngr)
        ingredientList.listData = recipes(index).ingredients.map(_.name)
        ingredientList.selectIndices(recipes(index).ingredients.length-1)
        setIngredients(recipes(index).ingredients.last)
    }
}

def removeIngredient {
    if(!recipeList.selection.items.isEmpty &&
        !ingredientList.selection.items.isEmpty) {
        val rIndex = recipeList.selection.leadIndex
        val iIndex = ingredientList.selection.leadIndex
        val shortIngr = recipes(rIndex).ingredients.patch(iIndex,List(),1)
        recipes(rIndex) = recipes(rIndex).copy(ingredients=shortIngr)
        ingredientList.listData = recipes(rIndex).ingredients.map(_.name)
        ingredientList.selectIndices(0)
        setIngredients(recipes(rIndex).ingredients.head)
    }
}

val ingredientListPanel = new BorderPanel {
    layout += (new GridPanel(1,2) {
        contents += Button("Add")(addIngredient)
        contents += Button("Remove")(removeIngredient)
    } -> BorderPanel.Position.North)
    layout += (new ScrollPane(ingredientList)
        -> BorderPanel.Position.Center)
}

val ingredientDataPanel = new BorderPanel {
```

```
layout += (new GridPanel(2,1) {
    contents += new Label("Name")
    contents += new Label("Amount")
} -> BorderPanel.Position.West)
layout += (new GridPanel(2,1) {
    contents += ingredientNameField
    contents += amountField
} -> BorderPanel.Position.Center)
}
```

```
def openFile {
    val chooser = new FileChooser
    if(chooser.showOpenDialog(recipeList)==FileChooser.Result.Approve) {
        val src = Source.fromFile(chooser.selectedFile)
        val lines = src.getLines
        recipes = Array.fill(lines.next.toInt)(Recipe(
            lines.next,
            List.fill(lines.next.toInt)(Ingredient(lines.next,lines.next)),
            {
                var dir = ""
                var line = lines.next
                while(line!=".") {
                    dir += (if(dir.isEmpty) "" else "\n")+line
                    line = lines.next
                }
                dir
            }
        ))
        src.close()
        recipeList.listData = recipes.map(_ .name)
        recipeList.selectIndices(0)
        setFields(recipes(0))
    }
}

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
            pw.println(r.directions)
            pw.println(".")
        }
        pw.close()
    }
}

def addRecipe {
```

```
```scala
val name = Dialog.showInput(recipeList, "What is the name of this recipe?",
    "Input", Dialog.Message.Question, null, Nil, "")
name match {
  case Some(n) =>
    recipes = recipes :+ Recipe(name.get,
      List(Ingredient("ingredient","amount")),"Directions")
    recipeList.listData = recipes.map(_.name)
    recipeList.selectIndices(recipes.length-1)
    setFields(recipes.last)
  case None =>
}
```
```

```
```scala
def removeRecipe {
  if(!recipeList.selection.items.isEmpty) {
    recipes = recipes.patch(recipeList.selection.leadIndex,List(),1)
    if(recipes.isEmpty) {
      recipes = Array(Recipe("New recipe",
        List(Ingredient("ingredient","amount")),"Directions"))
    }
    recipeList.listData = recipes.map(_.name)
    recipeList.selectIndices(0)
    setFields(recipes.head)
  }
}
```
```

```
```scala
def changeIngredientName(r:Int,i:Int) {
  val ing = recipes(r).ingredients(i)
  recipes(r) = recipes(r).copy(ingredients = {
    recipes(r).ingredients.patch(i,List(Ingredient(
      ingredientNameField.text,ing.amount)),1)
  })
  ingredientList.listData = recipes(r).ingredients.map(_.name)
  ingredientList.selectIndices(i)
}
```
```

```
```scala
def changeAmount(r:Int,i:Int) {
  val ing = recipes(r).ingredients(i)
  recipes(r) = recipes(r).copy(ingredients = {
    recipes(r).ingredients.patch(i,List(Ingredient(
      ing.name,amountField.text)),1)
  })
}
```
```

```
```scala
val frame=new MainFrame {
  title = "Recipe Book"
  contents = new BorderPanel {
    layout += (new ScrollPane(recipeList)
      -> BorderPanel.Position.West)
    layout += (new SplitPane(Orientation.Horizontal,
      new BorderPanel {
        layout += (ingredientListPanel
          -> BorderPanel.Position.West)
        layout += (ingredientDataPanel
          -> BorderPanel.Position.Center)
```

```
},
new ScrollPane(directionsArea)
-> BorderPanel.Position.Center)
}
listenTo(recipeList.selection,ingredientList.selection,directionsArea,
    ingredientNameField,amountField)
reactions += {
    case e:SelectionChanged =>
        if(e.source==recipeList) {
            if(!recipeList.selection.items.isEmpty) {
                setFields(recipes(recipeList.selection.leadIndex))
            }
        } else if(e.source==ingredientList) {
            if(!recipeList.selection.items.isEmpty &&
                !ingredientList.selection.items.isEmpty) {
                val rIndex = recipeList.selection.leadIndex
                val iIndex = ingredientList.selection.leadIndex
                setIngredients(recipes(rIndex).ingredients(iIndex))
            }
        }
    case e:FocusLost =>
        val rIndex = recipeList.selection.leadIndex
        if(e.source==directionsArea) {
            recipes(rIndex) = recipes(rIndex).copy(directions=directionsArea.text)
        } else if(e.source==ingredientNameField) {
            if(!recipeList.selection.items.isEmpty &&
                !ingredientList.selection.items.isEmpty) {
                val rIndex = recipeList.selection.leadIndex
                val iIndex = ingredientList.selection.leadIndex
                changeIngredientName(rIndex,iIndex)
            }
        } else if(e.source==amountField) {
            if(!recipeList.selection.items.isEmpty &&
                !ingredientList.selection.items.isEmpty) {
                val rIndex = recipeList.selection.leadIndex
                val iIndex = ingredientList.selection.leadIndex
                changeAmount(rIndex,iIndex)
            }
        }
    }
menuBar = new MenuBar {
    contents += new Menu("File") {
        contents += new MenuItem(Action("Open")(openFile))
        contents += new MenuItem(Action("Save")(saveFile))
        contents += new Separator
        contents += new MenuItem(Action("Exit")(sys.exit(0)))
    }
    contents += new Menu("Recipe") {
        contents += new MenuItem(Action("Add")(addRecipe))
        contents += new MenuItem(Action("Remove")(removeRecipe))
    }
}
size = new Dimension(800,600)
}
```

