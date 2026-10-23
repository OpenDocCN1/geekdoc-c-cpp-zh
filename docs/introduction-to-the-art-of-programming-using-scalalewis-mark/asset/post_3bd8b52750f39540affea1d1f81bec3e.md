
numeric operations on the values in a Table you can use toInt or toDouble on the String. So if you want to multiply two table values you could do this.

```
table(0,0).toString.toDouble * table(1,0).toString.toDouble
```

This is a bit verbose, but it is the price we pay for being able to put all types of different things in a Table.

If you play around with this enough you will probably stumble across the primary downfall of this approach, if the contents of the cell are not a number this will fail. To get around this, you would need to use the try/catch construct. We will discuss try-catch in detail in section 22.3. For now we will give a brief introduction. You might have seen that when something goes wrong with a statement the error message you get typically starts by giving you a type name that includes the word “Exception”. An EXCEPTION is an object that indicates a problem and when something goes wrong the code will THROW an exception. If you know this might happen and you want to deal with it, you tell Scala you want to TRY some code and then CATCH the exception if one occurs. The exceptions you can catch are specified with cases, just like a match expression.

The try-catch in Scala can be used as an expression. If there is no exception you get the value of the code you tried to do. If there is an exception that has a matching case, the value will be what happens in that case. To help you understand this, consider the following function.

```
def asDouble(a:Any):Double = {
  try {
    if(a==null) 0.0 else a.toString.toDouble
  } catch {
    case e:NumberFormatException => 0.0
  }
}
```

This function takes an Any object and returns a number for it. If the value is null it returns zero. Otherwise, it uses the .toString.toDouble method calls shown above. In this function that code is put inside of a try that will catch a NumberFormatException. As the name implies, this is an exception that occurs when you try to make a number of something that does not have the right format. If that happens, the case gives back the value 0.0. The sum above could now be expressed in this way.

```
asDouble(table(0,0))+asDouble(table(1,0))
```

This code is more robust in that if a Table cell contains something that is not a number, instead of stopping with an exception, the code uses 0.0 for that cell.

### 11.5.1 Table Actions

You now know how to set up Tables as well as how to read and alter the values in them. For many applications this will be sufficient. The actions in a GUI can very often be initiated by having the user click a button or select a menu item and have the code initiated by that action utilize the values in the table. There are some applications, however, when you need to actually respond to events that occur with the Table itself. In this situation you need to listen to the Table or possibly the selection object in the Table.

There is a significant list of events that can happen with Tables. You can look in the API for complete information, but here is a list of the main ones.

- `TableChanged` – Indicates that the structure of the Table stayed the same, but anything else could have changed.
- `TableColumnsSelected` – Indicates a change in the column(s) currently selected.
- `TableRowsAdded` – This event occurs when additional rows are added to the Table.
- `TableRowsRemoved` – This event occurs when rows are removed from the Table.
- `TableRowsSelected` – Indicates a change in the row(s) currently selected.
- `TableStructureChanged` – This event indicates the most general type of change. Anything in the Table could have changed including row and column counts.
- `TableUpdated` – Indicates that values in a specified part of the Table have changed.

To get the events that indicate changes in the selection you listen to `table.selection`. To get the others simply listen to the `table`.

If all that you are interested in is knowing when the value in a cell has been changed, you can use code like the following.

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

This code starts with an empty Table and a Label that shows 0.0. Every time that the user edits a cell, the code runs through all the cells and adds up the values in each, using zero if there is not a valid number. It changes the Label to reflect this sum. Enter this code into a file and run it as a script. Make changes to see what else you can do.

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

The information for the Table is stored in data and headers. To match with the types needed for building a DefaultTableModel, they are an Array[Array[AnyRef]] and an Array[AnyRef] respectively. Unfortunately, these types can not be used with the normal Scala creation approach so instead of passing in the data, the declaration of table includes a line that sets the model.

The table listens to itself and reacts to TableUpdated events. The updated data is always stored back into the data array. Note that this requires a bit of extra work because data pulled from the table is of the Any type. A match is used to make certain we have an AnyRef. There is also a check to see if the row being changed is the last one. In that situation, a new row is appended to data and the model is updated.

The addColumn method is called from a menu option. It asks the user for a name using Dialog.showInput, then appends a blank to the end of every row and uses the result as the updated data. It also appends the new header name to the end of headers. The last thing it does is to update the table model. The full signature of showInput is as follows.

```
def showInput [A] (parent: Component, message: Any, title: String, messageType: Value, icon: Icon, entries: Seq[A], initial: A): Option[A]
```

In our usage, we have the dialog box pop up over the table. We tell it that we are asking a question, with no icon, no entries, and an empty String for the initial value. This lets the user type in a String of their choosing. If entries were not empty, the user would get a drop-down box instead of a text field.

Note that showInput returns an Option type. That is because the user could hit “Cancel” or close the dialog box. This is the reason for the use of match. If the user does not provide a proper response, the Option is None and nothing is done.

This code does not demonstrate removing rows or columns, but either operation could be done with patch in a manner very similar to what is shown here.

## 11.6 Putting it Together

We can now put together all of the various aspects of GUIs into the recipe book script. Earlier we had built a GUI and added menus to it. However, the GUI was not interactive. Clicking on various elements did not do anything to other elements of the GUI. Now that we know how to make GUIs interactive we can add the proper functionality to this script. In order to be able to do this, we need to add some groundwork first. In particular, we need a good way to store the information associated with a recipe. This calls for some case classes.

We definitely want a case class to represent a recipe. The fact that a recipe can contain multiple ingredients makes it advantageous to have a case class for that as well. This leads to something like the following.

```
case class Ingredient(name:String,amount:String)
case class Recipe(name:String,ingredients:List[Ingredient],directions:String)
```

You can put this near the top of the script as many other parts of the script will be referring back to it.

We also need to have a way to store multiple recipes. We will do this with a variable declaration of an Array of Recipes. One could also choose to use a var List, but some of the interactions will require swapping out values and others might require doing direct access. Both of those will be easier and more efficient with an Array. The adding of new recipes would be easier with a List, but that operation will probably occur less frequently and can be done almost as easily with an Array.

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

This code includes a declaration of the Array as well as revisions of the active component declarations that use the one Recipe in the Array.

Now that we have this set up, we can start with the easy part of completing the functions that are called from the menus. We will start with the saveFile function as that defines the format that we will use in the file and it is a bit easier.

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
