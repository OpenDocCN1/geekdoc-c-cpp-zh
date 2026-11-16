![](bbox=[0.09, 0.05, 0.21, 0.21])

# PUT ON YOUR THINKING HAT

As you can see, registering a dependency property can get pretty complex. The trick, of course, whenever you’re working with a complex programming topic, is to break it down and only worry about one (relatively simple) part at a time. Let’s walk through building a complex registration using that technique. Hint: Check MSDN for the overloads of the PropertyMetadata constructor to decide which one to use.)

+   1. Write a simple call to Register() that creates the dependency property to wrap an integer named Amount in the RecipeItem class. (Don’t worry about writing the code for the CLR property, but remember the modifiers.)

+   2. Add a validation callback called validateAmount.

+   3. Add a property changed callback called OnAmountChanged.

+   4. Add a coerce value callback called CoerceAmount.