
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

The GUI created by running this code can be seen in figure 11.19. This is a long program, so we will consider the pieces individually. Lines 1-12 have the imports that we need, mostly from the ScalaFX libraries, but also include java.io.PrintWriter for saving the recipes out to file. Lines 14 and 15 have the class that are used to store the recipe book.

The GUI setup in lines 21-117. There are comments about the different sections of the GUI that handle different parts of the GUI. The sections for the menus and the recipe list are fairly straightforward. Note that line 45 declares a var Array that stores the recipe in memory. This is used extensively by the other elements of the GUI.

The section of the GUI that shows the ingredient information uses a GridPane and is a bit longer. The interactions with the user include changing the TextFields when user selects a different ingredient and changing the data when they edit the fields. Note that unlike previous examples, this code reacts to changes in the actual text of the TextField and the TextArea below it. This is because the code that deals with the changes refers to the indexes selected in the ListViews. If focus is lost because the user clicks on a different option in one of the two ListViews, those indexes are updated before the change in focus is processed. As a result, all changes are listed. Listening to every change in the **text** is less efficient, but it prevents any changes from being lost.

The **onChange** code uses a function below called **alterSelectedIngredient** to prevent code duplication. This function takes a single argument which is a function of **Ingredient => Ingredient**. This function returns a modified ingredient to store back into the list. If you go to the definition of **alterSelectedIngredient** on lines 220-230, you will see that we use a method of List that we have not seen before called **updated**. The behavior of this method is to replace one element of a List at a particular index with a specified value. This is used to modify the selected recipe by replacing the old one with the one that is passed.

The GUI setup ends by making the directions **TextArea** and then placing the pieces together using a **SplitPane** and a **BorderPane**. The **BorderPane** is set as the *root* of the **Scene**, so that it will size with the window.

After the GUI setup are a number of functions that are called when things change in the GUI or for buttons and menu items. These include functions for saving and loading in text files that store the recipes, as well as functions for adding and removing recipes and ingredients.

The **addRecipe** code on lines 165-177 uses another feature that we have not seen previously. It needs to ask the user for the name of the new recipe, as we do not provide any way to edit that in the GUI. To do this, it uses a type called **InputDialog** from the control package. As name implies, this class allows us to pop up a dialog box that reads text from the user. After creating the dialog box, we set the title, headerText, and getContent. When we call the method showAndWait, which waits until the user has either "OK" or "Cancel". The result of that is an Option which will be some value or None. Since we do not want to do anything if the user selects "Cancel", a call to foreach is used to handle their input. A foreach ignores None.

There is also a ChoiceDialog that allows us to allow the user to select from a number of options. Readers can look in.

## Introduction to Programming and Problem-Solving Using Scala

## Recipes

| File | Recipe | | |
|---|---|---|---|
| Pop Tarts | Add | Remove | Name: Pop Tart |
| | Pop Tart | Amount: 1 packet | | |
| | | | |
| ... | | | |
| | Toast the poptarts ... or don't. | | |

**FIGURE 11.19:** This shows the window that is produced when you run Recipe.scala.

## GUIs
