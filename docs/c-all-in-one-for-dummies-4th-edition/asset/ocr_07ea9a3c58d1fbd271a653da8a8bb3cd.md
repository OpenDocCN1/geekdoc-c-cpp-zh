# ## FRIENDS OF A SAME CLASS

An instance of a class can access the private and protected members of other instances of the same class. The compiler allows you to do it. However, you normally want objects to remain isolated from each other for all sorts of reasons, including keeping bugs at bay and reducing security risks. It helps to think of the only situation in which this kind of activity is actually useful as a host and client, when one instance acts as a host to a client instance for something like creating a container for an object of the same type. To make this sort of access happen, you provide a pointer to another instance of the same class (the client) inside the host class, perhaps passed in as a parameter. The host class is free to modify any of the passed class members.

```
```
  Protected
  Private From Peeks
  Protected
  Protected
  Private From FriendFunction
```
```

# # Using Classes and Types within Classes

Sometimes an application needs a fairly complex internal structure to get its work done. Three ways to accomplish this goal with relatively few headaches are nesting classes, embedding classes, and declaring types within classes. The following sections discuss the two most common goals: nesting classes and declaring types within classes. The “Nesting a class” section also discusses protection for embedded classes.

# ## Nesting a class

You may have times when you create a set of classes with one class acting as the primary class while all the other classes function as supporting classes. For example, you may be a member of a team of programmers, and your job is to write a set of classes that log on to a competitor’s computer at night and lower all the prices on the products. Other members of your team will use your classes in their applications. You’re just writing a set of classes; the teammates are writing the rest of the application. The following sections consider the issues involved in performing this task, as well as a potential solution in the form of nested classes.