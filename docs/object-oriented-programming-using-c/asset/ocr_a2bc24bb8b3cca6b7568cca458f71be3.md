# Object Oriented Programming using C#

# The Unified Modelling Language (UML)

We use an association when we want to give two related classes, and their relationship, prominence on a class diagram

‘source' class points to the 'target' class.

Strictly we could use an association when a class we define a String instance variable – but we would not do this because the String class is part of the C# platform and 'taken for granted' like an attribute of a primitive type. This would generally be true of all library classes unless we are drawing the diagram specifically to explain some aspect of the library class for the benefit of someone unfamiliar with its purpose and functionality.

Additionally we can show multiplicity at both ends of an association:

![](bbox=[0.282, 0.305, 0.783, 0.368])

This implies that 'OneClass' maintains a collection of objects of type 'OtherClass'. Collections are an important part of the C# library that we will look at the use of collections in Chapter 7.

| Activity 3 |
| Draw a diagram to represent a class called 'Catalogue' and a class 'ItemForSale' as defined below - |
ItemForSale has an attribute 'name' of type String and an attribute 'price' of type int. It also has a method SetPrice() which takes an integer parameter 'newPrice'.

'Catalogue' has an attribute 'listOfItems' i.e. the items currently held in the catalogue. As zero or more items can be stored in the catalogue 'listOfItems' will need to be an array or collection. 'Catalogue' also has one method AddItem() which takes an 'item' as a parameter (of type ItemForSale) and adds this item to the 'listOfItems'.

Draw this on a class diagram showing appropriate visibility modifiers for attributes and methods. |