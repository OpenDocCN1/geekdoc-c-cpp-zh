# **PUT ON YOUR THINKING HAT**

No, that wasn't an editing mistake. The descriptions of the functions are in order of cohesion. Did you have the courage of your convictions, or did you think you'd gotten it wrong when you started drawing all those straight arrows?

![](bbox=[0.1, 0.05, 0.2, 0.2])

# **FUNCTIONAL**

The GetIngredientNutrition() method calculates the USDA nutritional values for a specific Ingredient.

This method does only one thing. It's functionally cohesive, and demonstrates the SRP.

# **SEQUENTIAL**

The RecalculateRecipe() method accepts a number of servings, and updates the Amount of each Ingredient in a Recipe with the new amounts required, and the NutritionalData structure of the recipe with the new values.

Because the ingredient amounts and nutritional data must be synchronized, this is a valid sequential operation.

# **TEMPORAL**

The Recipe() constructor performs all the operations needed to initialize a new instance of the Recipe class.

Constructors are the classic example of method that display temporal cohesion.

# **COMMUNICATIONAL**

The ConvertAndCalculate() method converts all ingredients to metric measurements and re-calculates the nutritional data.

This method used the same data, the Items collection of the Recipe, but the two operations aren't otherwise related. It should be re-designed.

# **CHAOTIC**

The GetPrintableVersion() method accepts the number of servings as an argument, and then calculates the ingredient amounts and nutritional data and returns a formatted FixedDocument object.

Calculating amounts and formatting the recipe for printing are completely unrelated activities. This is a bad method!

![](bbox=[0.78, 0.75, 0.9, 0.85])