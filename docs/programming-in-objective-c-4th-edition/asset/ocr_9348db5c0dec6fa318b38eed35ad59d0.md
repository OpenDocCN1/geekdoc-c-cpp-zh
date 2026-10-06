This line says that myFraction is an object of type Fraction; that is, myFraction is used to store values from your new Fraction class. The asterisk that precedes the variable name is described in more detail below.

Now that you have an object to store a Fraction, you need to create one, just as you ask the factory to build you a new car. This is done with the following line:

```
myFraction = [Fraction alloc];
```

alloc is short for allocate. You want to allocate memory storage space for a new fraction. This expression sends a message to your newly created Fraction class:

```
[Fraction alloc]
```

You are asking the Fraction class to apply the alloc method, but you never defined an alloc method, so where did it come from? The method was inherited from a parent class. Chapter 8, Inheritance deals with this topic in detail.

When you send the alloc message to a class, you get back an instance of that class. In Program 3.2, the returned value is stored inside your variable myFraction. The alloc method is guaranteed to zero out all of an object's instance variables. However, that doesn't mean the object has been properly initialized for use. You need to initialize the object after you allocate it.

This is done with the next statement in Program 3.2, which reads as follows:

```
myFraction = [myFraction init];
```

Again, you are using a method that you didn't write yourself. The init method initializes the instance of a class. Note that you are sending the init message to myFraction. That is, you want to