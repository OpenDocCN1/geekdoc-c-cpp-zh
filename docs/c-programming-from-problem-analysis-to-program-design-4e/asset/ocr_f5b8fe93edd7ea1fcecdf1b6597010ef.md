with the berber object as the argument automatically calls the overridden ToString( ) method of the CarpetCalculator class. The ToString( ) method returns a formatted string that can be displayed.

> In Example 4.10, you do not fully qualify pricePerSqYard using a class or object name. Also notice the property identifier was not used. The private data member, pricePerSqYard, was able to be used because it was included in a member method of the class.

# Calling Instance Methods

Instance methods are nonstatic methods. When they are defined you do not use the static keyword. When you invoke an instance method, you do not use the class name. Recall methods in the Math class were class method's. In order to invoke the Pow( ) method for example, you had to precede the methods name with the class name (Math.Pow( )). A class method, static method, belongs to the whole class. You must use the class name to call it. Instance methods belong to specific objects. You must call or invoke them with an object.

After a class template has been defined to include private member data, public methods, and public properties, many different applications can use the class. To do so, objects of the class are instantiated using the class constructor.

# Calling the Constructor

Normally, the first method called is the constructor. This is the method that actually creates an object instance of the class. The syntax for this is:

```
ClassName objectName = new ClassName(argumentList);
```

or

```
ClassName objectName;
objectName = new ClassName(argumentList);
```

It is more common to call the constructor in a single statement as shown first.

Example 4-11 creates three objects and calls the three different constructor methods defined in Example 4-4.

# EXAMPLE 4.11

```
CarpetCalculator plush = new CarpetCalculator( );
CarpetCalculator pile = new CarpetCalculator(37.90, 17.95);
CarpetCalculator berber = new CarpetCalculator(17.95);
```