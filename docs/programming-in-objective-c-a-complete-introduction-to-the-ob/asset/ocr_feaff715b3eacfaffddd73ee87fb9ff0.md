# Chapter 15 Numbers, Strings, and Collections

The print method uses the fast enumeration technique previously described to retrieve each element from the set. You also defined a macro called INTBOJ to create an object from an integer value. This enables you to make your program more concise and saves some unnecessary typing. Of course, your print method is not general because it works only with sets that have members in them. But it's a good reminder of how to add methods to a class through a category: (Note that the C library's printf routine is used in the print method to display elements of set on a single line.) setWithObjects: creates a new set from a nil-terminated list of objects. After creating three sets, the program displays the first two using your print method. isEqualSet: method tests whether set is equal to set2—it's.

The containsObject: method tests whether the integer 10 is in set and whether it is in set2. The Boolean value the method returns verify that it is in the first set, not in the second.

The program next the addObject: and removeObject: methods to add and remove 4 and 10 from set, respectively. Displaying the contents of the set that the operations were successful.

You can use the intersect: and union: methods to calculate the intersection and union of two sets. In both cases, the result of the operation replaces the receiver of the message.

The framework also provides a class called NSCountSet. These sets represent more than one occurrence of the same object; however, instead of adding multiple times in the set, a count of times is maintained. The first time an object is added to the set, its count is 1. Subsequently adding the object to the set increments the count, while removing the object decrements the count. If it reaches zero, the actual object is removed from the set. countFor: retrieves the count for a specified object in a set.

One application for a counted set could be a word counter application. Each time a word is found in some text, it can be added to the counted set. When the text is complete, each word is retrieved from the set along with its count, which indicates the number of times the word appeared in the text.

We have just shown some basic operations with sets. Tables 15.9 and 15.10 summarize commonly used methods for working with immutable and mutable sets,.. NSMutableSet is a subclass of NSSet, it inherits its methods.

In Tables 15.9 and 15.10, obj, obj, obj2 are any objects; nset is an NSSet or NSMutableSet object; and size is an NSInteger integer.

> A more general method could invoke each object's description method for displaying each member of the set. That would allow sets containing any types of objects to be displayed in a readable format. Also note that you can display the contents of any collection with a single call to NSLog, using the the "print object" format characters "%@".