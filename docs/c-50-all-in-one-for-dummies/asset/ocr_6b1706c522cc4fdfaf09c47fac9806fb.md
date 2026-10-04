# Defining a Class and an Object 213

other two properties are the number of doors and the number of wheels on the vehicle.

As with any variable, make the names of the members as descriptive as possible. Although I added comments to the data members, it isn't necessary. A good variable name says it all.

The public modifier in front of the class name makes the class universally accessible throughout the program. Similarly, the public modifier in front of the member names makes them accessible to everything in the program. Other modifiers are possible. (Chapter 5 in this minibus covers the topic of accessibility in detail and how you can hide your members.)

The class definition should describe the properties of the object that is salient to the problem at hand. A little hard to do right now because you don't know what the problem is, but you can see where I'm headed.

# What's the object?

Defining a Vehicle design isn't the same task as building a car. Someone has to cut some metal and turn bolts before anyone can drive an actual vehicle. A class object is declared in a similar (but not identical) fashion for declaring intrinsic object as an int.

The term object is used generally to mean a "thing". Okay, that isn't helpful. An instance variable is an int object. A vehicle is a Vehicle object. You are a reader. I am an author object— okay, for that one.

The following code segment creates a car of class Vehicle:

```
Vehicle myCar;
myCar = new Vehicle();
```

The first line declares a variable myCar of type Vehicle, just like you can declare somethingOther of class int. (Yes, a class is a type, and C# objects are defined as classes). The Vehicle() command creates a specific object of type Vehicle and stores the location in the variable myCar. The new has nothing to do with the age of myCar. (My car could qualify for an antique license plate if it weren't ugly) The new operator creates a new block of memory in which you can store the properties of myCar.

In C#, you say that myCar is an object of class Vehicle. You also say that myCar is an instance of Vehicle. In this context, instance means "an example of" or "one of them". You can use the word instance as a verb, in instantiating Vehicle. That's what new does.