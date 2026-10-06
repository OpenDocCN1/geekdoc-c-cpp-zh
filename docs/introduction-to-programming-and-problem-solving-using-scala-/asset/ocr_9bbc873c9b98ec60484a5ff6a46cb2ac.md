# GUIs

MenuBar, the recipe list, ingredient information and tools, and the recipe directions.
BorderPane allow us to resize the elements if the user resizes the window, and it will
ge us a top, left, and center that can be used to further optimize the content. We can
place the MenuBar in the center, the recipe list in the left, and else in the center.
We will break up the center and use a SplitPane to separate the recipe directions from
t ingredient information. We will use a GridPanel for the buttons, ingredient list, and
ingredient settings. The following code shows how we could solve this adding "traditional"
handlers to the code instead of bindings.

Listing 11.20: Recipe.scala

```
import scalafx.Imports..
import scalafx.scene.Scene
import scalafx.application.JFXApp
import scalafx.scene.control..
import scalafx.scene.layout..
import scalafx.event.ActionEvent
import scalafx.scene.input.KeyCode
import scalafx.scene.input.KeyCombination
import scalafx.scene.input.KeyCodeCombination
import scalafx.stage.FileChooser
import scalafx.collections.ObservableBuffer
import java.io.PrintWriter
```

```
case class Ingredient(name:String, amount:String)
case class Recipe(name:String, ingredients:List[Ingredient]), directions:String)
val app = new JFXApp {
stage = new JFXApp.PrimaryStage {
  title = "Recipes"
  scene = new Scene(600,400) {}
  MenuBar
    val menuBar = new MenuBar
    val fileMenu = new Menu("File")
    val openItem = new MenuItem("Open"
    openItem.accelerator = new KeyCodeCombination(KeyCode.O,ControlDown)
    openItem.setOnAction = (e:ActionEvent) => { openFile }
    val saveItem = new MenuItem("Save")
    saveItem.accelerator = new KeyCodeCombination(KeyCode.S,ControlDown)
    saveItem.setOnAction = (e:ActionEvent) => { saveFile }
    val exitItem = new MenuItem("Exit")
    exitItem.accelerator = new KeyCodeCombination(KeyCode.X,ControlDown)
    exitItem.setOnAction = (e:ActionEvent) => { System.exit(0) }
  fileMenu.items = List(openItem,saveItem,exitItem)
val recipeMenu = new Menu("Recipe"
  val addItem = new MenuItem("Add")
  addItem.setOnAction = (e:ActionEvent) => { addRecipe }
  val removeItem = new MenuItem("Remove")
  removeItem.setOnAction = (e:ActionEvent) => { removeRecipe }
  recipeMenu.items = List(addItem,removeItem)
}
```