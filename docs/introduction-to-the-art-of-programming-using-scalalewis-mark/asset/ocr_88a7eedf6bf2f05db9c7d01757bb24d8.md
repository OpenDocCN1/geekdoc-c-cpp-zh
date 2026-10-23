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