# # INHERITANCE

The ability for a type to inherit state and behavior from another type.

In the .NET Framework, classes can only inherit from a single base class. Some languages support MULTIPLE INHERITANCE, which allows multiple base classes, which seems like a good idea, but in practice tends to be very confusing. Interfaces provide much the same functionality in a conceptually simpler way.

![](bbox=[0.55, 0.08, 0.75, 0.38])

StandardRecipe and BakedGoodRecipe both inherit from Recipe.

# # ABSTRACTION

The simplification of an object model by including only necessary details, and working at the most appropriate level of detail.

The word "Abstraction" is used in several ways in the programming world. You can also "abstract out" the common members of classes to define a base class.

![](bbox=[0.65, 0.43, 0.85, 0.58])

The RecipeItem class doesn't include nutritional information because it isn't relevant.

```
```csharp
List<Recipe> myList = new List<Recipe>();
...
myList[3] = new BakedGoodRecipe();
MessageBox.Show(myList[3].Name);
```
```

Abstraction also lets you work with the simplest form of an object. If you don't care about the Formula property of a BakedGoodRecipe, you can just treat it as a Recipe. (This is also an example of polymorphism. Do you know why?)