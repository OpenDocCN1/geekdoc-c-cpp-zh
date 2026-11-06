The first step in `main()` is to create a Door instance. The code doesn’t use a pointer to show that you can mix pointers with stack variables in an application. After creating the Door instance, the code calls `Start()`. Next, the code creates three creature instances: Cat, Dog, and Human, and sets the name property for each.

The calls to the entrance.`GoThrough()` method passes a Cat, a Dog, and a Human (all in order). Because you can see the Door class, you know the code calls three different methods that are all named the same. But when using the class, you consider them one method that accepts a Cat, a Dog, or a Human. That’s the goal of overloading: to create what feels like versions of the one function. Here’s what you see when you run this application:

```
Welcome, Sneeky Girl
A cat just entered!
Welcome, Little George
A dog just entered!
Welcome, John
A human just entered!
```

# # Starting and Ending with Constructors and Destructors

You can add two special methods to your class that let you provide special startup and shutdown functionality: a *constructor* and a *destructor*. The following sections provide details about these methods.

# ## Starting with constructors

When you create a new instance of a class, you may want to do some basic object setup. Suppose you have a class called Apartment, with a private property called `NumberOfOccupants` and a method called `ComeOnIn()`. The code for `ComeOnIn()` adds 1 to `NumberOfOccupants`.

When you create a new instance of Apartment, you probably want to start `NumberOfOccupants` at 0. The best way to do this is by adding a special method, a *constructor*, to your class. This method has a line of code such as

```
NumberOfOccupants = 0;
```