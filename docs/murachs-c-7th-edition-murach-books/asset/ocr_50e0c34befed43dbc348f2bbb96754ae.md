# More skills for creating a class

In addition to the skills you’ve already learned in this chapter for creating classes, the topics that follow present some additional skills that you should know about.

# How to code auto-implemented properties

If you look back at the Code property in figure 12-7, you’ll see that the get and set accessors simply return the value of an instance variable and assign the value parameter to the instance variable. When that’s the case, you can code the property as an auto-implemented property as shown in figure 12-16. Auto-implemented properties provide a shorthand for coding simple properties. The auto-implemented property in the first example in this figure, for example, is equivalent to the Code property shown in figure 12-7.

When you use an auto-implemented property, you should know that the compiler creates a private instance variable for you. Because of that, this property is only accessible through the get and set accessors. You should also know that you can create a read-only auto-implemented property by omitting the set keyword as shown in the second example in this figure. However, you can’t create write-only auto-implemented properties.

The second example also shows that you can assign an initial value to an auto-implemented property. That’s particularly useful for a read-only property, since its value can’t be set in any other way.

The third and fourth examples in this figure show statements that set and get the value of the auto-implemented property in the first example. If you compare these statements with the statements in figure 12-7 that set and get the value of a property, you’ll see that they’re identical.

Note that if you want to convert a property that doesn’t use auto-implemented properties to one that does, you can use refactoring to do that. Just place the cursor anywhere in the property, press Ctrl + period (.), and select Use Auto Property from the Quick Actions menu that appears. Note that this deletes the private instance variable that’s associated with the property. In addition, if a value is assigned to the instance variable, that value is assigned to the property.

With C# 9.0 and later, you can use the init keyword instead of the set keyword to create an init-only setter. In this figure, the fifth example shows how to create an init-only setter for the Code property. When you use this type of setter, you can only assign a value to the property when the object is being initialized by a constructor or an object initializer. In this figure, the sixth example shows how to use an object initializer to set the value of the Code property. However, you could also use a constructor like the one shown in figure 12-4.