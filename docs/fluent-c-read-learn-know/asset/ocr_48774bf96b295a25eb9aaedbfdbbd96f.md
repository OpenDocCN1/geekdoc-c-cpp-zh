# HOW'D YOU DO?

Did you identify the relationships correctly? You really need to understand the problem you're modelling to do this, so if in doubt, ask your client. (Or in this case, ask a cook.)

![](bbox=[0.095, 0.052, 0.205, 0.212])

**StandardRecipe Class**
Properties
- Name
- Servings
Methods
- Print

**PreparationStep Class**
Properties
- Process
- StepNumber
Methods
- Print

**BakedGoodRecipe Class**
Properties
- Division
- Name
- Servings
- Yield

**FormulaItem Class**
Properties
- Name
- Percentage

**RecipeItem Class**
Properties
- Amount
- AmountType
- Count
- Name
- Preparation
- Volume
- Weight

BakedGoodRecipe ______ collection of FormulaItems.
Amount ______ one of Teaspoon, Tablespoon, Cup or Weight.
BakedGoodRecipe ______ kind of Recipe.
StandardRecipe ______ kind of Recipe.
Both StandardRecipe and PreparationStep ______ printing.
StandardRecipe ______ collection of RecipeItems.