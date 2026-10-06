You extend the GraphicObject class here by adding a new instance variable called uniqueID and by synthesizing a setter and getter method for it. You also add a method called doStuffWithUniqueID:

Unnamed categories are useful because their methods are private. So if you need to write a class that has data and methods that can only be used within the class itself, an unnamed category might fit the bill.

# Some Notes About Categories

A category can override another method in the class, but this is considered poor programming practice. For one thing, after override a method, you can no longer access the original method. Therefore, you must be careful to duplicate all the functionality of the overridden method in your replacement. If you need to override a method, subclassing might be the right choice. If you override a method in a subclass, you can still reference the parent's method by sending a message to super. You don't have to understand all the intricacies of the method you are overriding; you can simply invoke the parent's method and add your own functionality to the subclass's method.

You can have as many categories as you like, following the rules we've outlined here. If a method is defined in more than one category, the language does not specify which one will be used.

Remember that extending a class by adding new methods with a category affects not just that class, but all its subclasses as well. This can be potentially dangerous if you add new methods to the root object NSObject, for example, because everyone will inherit these new methods, whether or not that was your intention.

The new methods you add to an existing class through a category can serve your purposes just fine, but they might be inconsistent with