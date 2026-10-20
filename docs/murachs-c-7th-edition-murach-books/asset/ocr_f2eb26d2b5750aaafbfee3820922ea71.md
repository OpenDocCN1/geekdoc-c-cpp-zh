# How to convert data types

In chapter 3, you were introduced to the use of classes, which provide properties and methods for the objects that are instantiated from the classes. Now, you’ll be introduced to structures, which are similar to classes. Then, you’ll learn how to use these structures and classes to convert data from one type to another.

# The .NET structures and classes that define data types

Figure 4-12 summarizes the structures and classes that define the data types, along with the C# keywords that you can use to work with these structures and classes. To work with the Decimal structure, for example, you use the decimal keyword. To work with the Int32 structure, you use the int keyword. And to work with the String class, you use the string keyword.

When you declare a variable as one of the data types that’s supported by a structure, that variable is a value type. That means that the variable stores its own data. If, for example, you declare a variable as a decimal type, that variable stores the decimal value. In addition, if you assign that variable to another decimal variable, the new variable will store a separate copy of the value.

By contrast, when you declare a variable as one of the data types that’s supported by a class, an object is created from the class. Then, the variable stores a reference to the object, not the object itself. Because of that, object data types are called reference types.

In this figure, the two reference types defined by the .NET Framework are string and object. So when you declare a variable as a string, that variable holds a reference to a String object, which contains the data for the string. As a result, it’s possible for two or more variables to refer to the same String object.

In addition to the String class, the .NET Framework also provides a generic Object class. You can use a variable created from this class to hold a reference to any type of object. You’ll learn more about working with the Object class in chapter 14.