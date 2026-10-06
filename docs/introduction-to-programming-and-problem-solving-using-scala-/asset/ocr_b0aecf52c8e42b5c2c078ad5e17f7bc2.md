# Introduction to Programming and Problem-Solving Using Scala

```
val pw = new PrintWriter(selected)
println(r.recipes.length)
for (r <- r.recipes) {
  pw.println(r.name)
  pw.println(r.ingredients.length)
  for (ing <- r.ingredients) {
    pw.println(ing.name)
    pw.println(ing.amount)
  }
  pw.println(r.directions)
  pw.println(".")
}
pw.close()
```

```
def addRecipe:Unit = {
val dialog = new TextInputDialog
dialog.headerText = "Recipe Name"
dialog.contentText = "What is the name of the new recipe?"
dialog.showAndWait().foreach { name ->
  recipes += StringProperty(name),
  List(StringProperty("ingredient"),
  StringProperty("amount"), StringProperty("Directions\))
recipeList.items = ObservableBuffer(recipes.map(_.name).value*)
recipeList.selectionModel.value.clearAndSelect(recipes.length-1)
}
```

```
def removeRecipe:Unit = {
  if (recipeList.selectionModel.value.selectedItems.isEmpty) {
    recipes = recipes.patch(recipeList.selectionModel.value.selectedIndex,
    value.Null,1)
    recipeList.items = ObservableBuffer(recipes.map(_.name).value*)
    recipeList.selectionModel.value.clearAndSelect()
  }
```

```
def addIngredient:Unit = {
val recipeIndex = recipeList.selectionModel.value.selectedIndex.value
if (recipeIndex>0) {
  val newIng = Ingredient(StringProperty("Stuff"), StringProperty("Some"))
  recipes(recipeIndex) = recipes(recipeIndex).copy(
  ingredients = recipes(recipeIndex).ingredients += newIng
  recipeList.items.value += newIng.name.value
  }
```

```
def removeIngredient:Unit = {
val recipeIndex = recipeList.selectionModel.value.selectedIndex.value
val ingredientIndex =
ingredientsList.selectionModel.value.selectedIndex
if (recipeIndex>0 && ingredientIndex>0) {
  recipes(recipeIndex) = recipes(recipeIndex).copy(ingredients =
```