
![](img/157fcf510c119278e4b1267c62717fa8_288_0.png)

## FIGURE 11.2: This shows a possible layout for the GUI that we want to build for editing recipes.

The GUI should give the user the ability to add and remove recipes. They should be able to select recipes and edit the various information that we have on them.

At this point in the analysis you would probably want to sketch out a little picture of what you want the GUI to look like. That is done for this GUI in figure 11.2. The left side is taken up by a ListView that shows all the recipes. When the user clicks on a recipe, the information for it should be shown on the right. That includes a list of all the ingredients and the directions. The ingredients can also be edited and there need to be some buttons to help with this. The options for adding and removing recipes will be in the menus, which will be discussed in the next section.

The question is how we should lay this out. Any GUI can be built in multiple different ways using the different panel and pane options that were listed above. For example, the separation between the recipe list and the information about the selected recipe could be created by a BorderPanel, a BoxPanel with a horizontal orientation, or a SplitPane. Which of these you pick will normally be determined by the way in which the panels would size things or whether you want to give the user the control of a SplitPane. We will use a BorderPanel for the top-level split. We will then use a SplitPane to separate the directions from the ingredient information. We will use two BorderPanels for the ingredient information and the Buttons will be built using a GridPanel. The settings area will also need to be refined a bit more. It probably just needs the name of the ingredient along with the amount needed. That can be laid out using a combination of BorderPanel and GridPanel.

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

When you run either of these scripts you get a window like what is shown in figure 11.3. In the code you might notice that each of the ListViews and the large TextArea are put inside of ScrollPanes. This is to make it so that if the lists get large or the directions get long, scroll bars will be added to allow the user to scroll around and see everything they need to.

## 11.2.4 Menus

All we lack in the appearance of the GUI now is the menus. The MainFrame has a field called menuBar that we can set to be an object of type MenuBar. The MenuBar type has

contents, like the panels and panes, but you should only add objects of the **Menu** type to a **MenuBar**.

The **Menu** objects are created with `new` and should be passed a `String` that you want as the title of the **Menu**. The `contents` of a **Menu** can be of one of five types.

- * **MenuItem** - This is the most common thing you will put in a **Menu**. You create them with `new` and the easiest approach is to give them an `Action` object. The `Action` object can be made like a **Button** with a `String` and an action that is passed by-name. For example `new MenuItem(Action("Exit")(exit(0)))`.
- * **Menu** - You can add a **Menu** to a **Menu**. This will appear as a submenu when you run the program.
- * **CheckMenuItem** - Menus can also have options on them that are selected. To do this use the type **CheckMenuItem**. You make these with `new` and pass in a `String` for the text to display.
- * **RadioMenuItem** - If you have multiple values and you only want to allow one to be selected use a **RadioMenuItem**. These are made like **CheckMenuItems**. All the **RadioMenuItems** and you want to have grouped together should be added to a single object of the **ButtonGroup** type.
- * **Separator** - This is a simple component used to space items out to improve appearance and usability.

We can set up a simple menu system for our recipe script by adding the following code inside the `MainFrame` right before we set the `size`.

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
