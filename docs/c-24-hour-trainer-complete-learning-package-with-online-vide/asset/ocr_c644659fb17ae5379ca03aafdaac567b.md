For example, you could use a Dictionary to make an employee phone book. It could store phone numbers using names as the keys. Then given someone's name, you could use the dictionary to very quickly look up that person's phone number.

# Generic Classes

The following sections describe some particular kinds of classes that come pre-built by the .NET Framework. These are generic classes, so before you learn about them you should know a little about what a generic class is.

A generic class is one that is not tied to a particular data type. For example, suppose you build a StringList class that can store a list of strings. Now suppose you decide you wanted an IntegerList class to store lists of integers. The two classes would be practically identical; they would just work with different data types.

I've mentioned several times that duplicated code is a bad thing. Having two nearly identical classes means debugging and maintaining two different sets of code that are practically the same.

One solution to this situation is to make a more general AnythingList class that uses the general object data type to store items. An object can hold any kind of data, so this class could hold lists of integers, strings, or Customer objects. Unfortunately that has two big problems.

First, you would need to do a lot of work converting the items with the general object data type stored in the list into the int, string, or Customer type of the items that you put in there. This is annoying because it gives you more work to do and makes your code more complicated and harder to read.

A bigger problem is that a list that can hold anything can hold anything. If you make a list to hold customer data, it could still hold ints, strings, and PurchaseOrder objects. Your code would need to do a lot of work to prevent you from accidentally adding the wrong kind of item to the list.

A much better approach is to use generic classes. These classes take data type parameters in their declarations so they know what kind of data they will manipulate. That lets them automatically store and retrieve items using the correct data type. It also lets them perform type checking so you can't accidentally add a Bicycle object to a list of Employees.

Using this kind of class, you can build a list of integers, strings, or what have you.

List is one of the generic collection classes defined by the .NET Framework. The following code declares and initializes a List:

```
List<string> names = new List<string>();
```

The <string> part of the declaration indicates that the class will work with strings. You can put strings into the list and take strings out of it. You cannot add an integer to the list, just as you can't set a string variable equal to an integer. Visual Studio knows that the list works with strings and won't let you use anything else.

Note that IntelliSense knows about generic classes and provides help. If you begin a declaration with List, IntelliSense displays List<> to let you know that it is a generic class.