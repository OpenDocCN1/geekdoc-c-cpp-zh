# # HOW'D YOU DO?

There are, of course, lots of ways to solve the problems with the Recipe hierarchy, but here's what I'd do: The problem is a semantic one, so I looked at the semantics of classes. Originally the Yield property belonged only to the BakedGoodRecipe class, the idea being that instead of a specific number of servings, these recipes yielded a certain number of items (2 loaves of bread, or 3 dozen cookies, for example.)

But, of course, any recipe yields a certain amount, and that's useful information. Take, for example, a recipe that yields 2 quarts of soup. That might serve 4 as a main course, or 6 as a first course, or 12 if you're serving it in teeny tiny cups as part of a starter. So the solution I chose is to move the Yield property up to RecipeBase, so that all Recipes can now specify both Yield and Servings.

![](bbox=[0.555, 0.225, 0.885, 0.605])

# # MY VIEW

![](bbox=[0.115, 0.705, 0.275, 0.855])

The solution probably seems obvious, doesn't it? It does to me, in retrospect. You might even feel like I set you up. But here's the reality: I'm a dedicated cook, and I have a couple decades' experience as an application designer, but it took me two days of pondering to come up with this solution. Lots of things are obvious in retrospect. Remember the paperclip?