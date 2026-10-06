# GUIs 319

```
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
        val newRecipe = recipes(recipeIndex).copy(ingredients =\            recipes(recipeIndex).ingredients.updated(ingredientIndex,
            newIngredient))
        recipes(recipeIndex) = newRecipe
    }
}
app.main(args)
```

The GUI created by running this code can be seen in figure 11.19. This is a long program, so we will consider the pieces individually. Lines 1-12 have the imports that we need, mostly from the ScalaFX libraries, but also include java.io.PrintWriter for saving the recipes out to file. Lines 14 and 15 have the class that are used to store the recipe book.

The GUI setup in lines 21-117. There are comments about the different sections of the GUI that handle different parts of the GUI. The sections for the menus and the recipe list are fairly straightforward. Note that line 45 declares a var Array that stores the recipe in memory. This is used extensively by the other elements of the GUI.

The section of the GUI that shows the ingredient information uses a GridPane and is a bit longer. The interactions with the user include changing the TextFields when user selects a different ingredient and changing the data when they edit the fields. Note that unlike previous examples, this code reacts to changes in the actual text of the TextField