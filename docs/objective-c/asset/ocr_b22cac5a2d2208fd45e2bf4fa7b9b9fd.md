be incremented or decremented. The Objective-C language runtime knows that when the retain count reaches zero, the object in question can be deallocated. When the object is deallocated, all of its memory resources are given back to the system to be reused.

The retain count can be incremented by using several standardized means. First and foremost, any time you create a new object using a method whose name contains the words alloc, or create, the object returned will have a retain count of one. Additionally, any time you acquire an object by using a method with a method name containing the word copy, that object will also have a retain count of one. You can manually increment the retain count by calling the method retain. Finally, you can decrement the retain count by calling the method release. Again, when the retain count reaches zero, the object, and its memory, are deallocated.

In the following listings, I go over a few scenarios to show how this works in practice. First, in Listing 4.1 I allocate an object using a standard alloc, and init.

# Listing 4.1

# A standard allocation of an object

```
Bar *foo = [[Bar alloc] init];
```

In this case, at the end of this method, the object foo has a retain count of one.

Now take a look at Listing 4.2

# Listing 4.2

# Retaining an object

```
Bar *foo = [[Bar alloc] init];
[foo retain];
```

In this case, in addition to allocating the object using an alloc call, I’m also incrementing the retain count by using the retain method. At the end of this code, the object has a retain count of two.