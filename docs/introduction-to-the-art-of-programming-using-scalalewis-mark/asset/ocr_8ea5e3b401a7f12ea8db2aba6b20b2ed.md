# 11.6 Putting it Together

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
```