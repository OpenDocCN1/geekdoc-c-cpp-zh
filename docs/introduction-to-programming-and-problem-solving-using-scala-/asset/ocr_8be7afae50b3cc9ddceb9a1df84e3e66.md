# GUIs

```
recipes(recipeIndex).patch(ingredientIndex,Nil,1))
bindRecipeFields(recipeIndex)
```

```
def bindRecipeFields(r:Recipe):Unit = {
ingredientsList.items = ObservableBuffer(r.ingredients.map(_.name.value):*)
selectedRecipe.foreach(_.directions.unbind
directionsArea.text = r.directions.value
r.directions <= directionsArea.text
selectedRecipe = Some(r)
}
```

```
def bindIngredientFields(ingr:Ingredient):Unit = {
selectedIng.foreach { si =>
s.name.unbind
ingredientField.text = ingr.name.value
ingr.name <= ingredientField.text
amountField.text = ingr.amount.value
ingr.amount <= amountField.text
recipes.foreach(println)
selectedIng = Some(si)
}
```

```
app.main(args)
```

You can see that we were able to eliminate the AlterSelectedIngredient function in the above code, but we did another function to call when binding ingredients in addition to the one for recipes. The bindings simplify the code in some ways, but they introduce one notable complexity. When we switch from one recipe to another we have to unbind the values that are no longer selected. This requires two vars to store what we have bound to. The Option type is used for these as nothing has been bound when the program is started.

The approach of using bindings typically works best if there is minimal changing of what values are being bound, hence, this is not the ideal application for them. In your own GUIs, you are encouraged to use whichever approach makes the most sense to you.

# ## 11.9 End of Chapter Material

# ### 11.9.1 Summary of Concepts

+   - Most of the programs that people interact with these days have Graphical User Interfaces, GUIs.

+   - We can write GUIs in Scala using types from the ScalaFX. This library wraps around the JavaFX library, though this fact is generally not obvious in our code.