
These C# features are necessary for writing object-oriented programs:

- **Controlled access:** C# controls the way in which class members can be accessed. C# keywords enable you to declare some members wide open to the `public` whereas `internal` members are `protected` from view and some secrets are kept `private`. Notice the little hints. Access control secrets are revealed in Chapter 5 of this minibook.
- **Specialization:** C# supports specialization through a mechanism known as `class inheritance`. One class inherits the members of another class. For example, you can create a `Car` class as a particular type of `Vehicle`. Chapter 6 in this minibook specializes in specialization.
- **Polymorphism:** This feature enables an object to perform an operation the way it wants to. The `Rocket` type of `Vehicle` may implement the `Start` operation much differently from the way the `Car` type of `Vehicle` does. At least, I hope it does every time I turn the key in my car. (With my car, you never know.) But all `Vehicles` have a Start operation, and you can rely on that. Chapter 7 in this minibook finds its own way of describing polymorphism.
- **Indirection:** Objects frequently use the services of other objects — by calling their public methods. But classes can “know too much” about the classes they use. The two classes are then said to be “too tightly coupled,” which makes the using class too dependent on the used class. The design is too brittle — liable to break if you make changes. But change is inevitable in software, so you should find more `indirect` ways to connect the two classes. That’s where the C# `interface` construct comes in. (You can get the scoop on interfaces in Chapter 8 of this minibook.)

## Chapter 2: Showing Some Class

### In This Chapter

- Introducing the C# class
- Storing data in an object
- Assigning and using object references
- Examining classes that contain classes
- Identifying static and instance class members
- Using constants in C#

You can freely declare and use all the intrinsic data types — such as `int`, `double`, and `bool` — to store the information necessary to make your program the best it can be. For some programs, these simple variables are enough. However, most programs need a way to bundle related data into a neat package.

As shown in Book I, C# provides arrays and other collections for gathering into one structure groups of like-typed variables, such as `strings` or `ints`. A hypothetical college, for example, might track its students by using an array. But a student is much more than just a name — how should this type of program represent a student?

Some programs need to bundle pieces of data that logically belong together but aren’t of the same type. A college enrollment application handles students, each with her own name, rank (grade-point average), and serial number. Logically, the student’s name may be a `string`; the grade-point average, a `double`; and the serial number, a `long`. That type of program needs a way to bundle these three different types of variables into a single structure named `Student`. Fortunately, C# provides a structure known as the `class` for accommodating groupings of unlike-typed variables.

## Defining a Class and an Object

A class is a bundling of unlike data and functions that logically belong together into one tidy package. C# gives you the freedom to foul up your classes any way you want, but good classes are designed to represent concepts.

Computer science models the world via structures that represent concepts or things in the world, such as bank accounts, tic-tac-toe games, customers, game boards, documents, and products. Analysts say that "a class maps concepts from the problem into the program." For example, your problem might be to build a traffic simulator that models traffic patterns for the purpose of building streets, intersections, and highways. (I really want you to build traffic simulators that can fix the intersections in front of my house.)

Any description of a problem concerning traffic would include the term vehicle in its solution. Vehicles have a top speed that must be figured into the equation. They also have a weight, and some of them are clunkers. In addition, vehicles stop and vehicles go. Thus, as a concept, vehicle is part of the problem domain.

A good C# traffic-simulator program would necessarily include the class Vehicle, which describes the relevant properties of a vehicle. The C# Vehicle class would have properties such as topSpeed, weight, and isClunker.

Because the class is central to C# programming, the rest of Book II spelunks the ins and outs of classes in much more detail. This chapter gets you started.

### Defining a class

An example of the class Vehicle may appear this way:

```
public class Vehicle
{
    public string model;    // Name of the model
    public string manufacturer; // Ditto
    public int numOfDoors;  // The number of doors on the vehicle
    public int numOfWheels; // You get the idea.
}
```

A class definition begins with the words public class, followed by the name of the class — in this case, Vehicle.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_241_0.png)

Like all names in C#, the name of the class is case sensitive. C# doesn't enforce any rules concerning class names, but an unofficial rule holds that the name of a class starts with a capital letter.

The class name is followed by a pair of open and closed braces. Within the braces, you have zero or more members. The members of a class are variables that make up the parts of the class. In this example, class Vehicle starts with the member string model, which contains the name of the model of the vehicle. If the vehicle were a car, its model name could be Trooper II. (Have you ever seen or heard of a Trooper I?) The second member of this Vehicle class example is string manufacturer. The other two properties are the number of doors and the number of wheels on the vehicle.

As with any variable, make the names of the members as descriptive as possible. Although I added comments to the data members, it isn't necessary. A good variable name says it all.

The public modifier in front of the class name makes the class universally accessible throughout the program. Similarly, the public modifier in front of the member names makes them accessible to everything else in the program. Other modifiers are possible. (Chapter 10 in this minibook covers the topic of accessibility in more detail and shows how you can hide some members.)

The class definition should describe the properties of the object that are salient to the problem at hand. That's a little hard to do right now because you don't know what the problem is, but you can see where I'm headed.

### What's the object?

Defining a Vehicle design isn't the same task as building a car. Someone has to cut some sheet metal and turn some bolts before anyone can drive an actual vehicle. A class object is declared in a similar (but not identical) fashion to declaring an intrinsic object such as an int.

The term object is used universally to mean a "thing." Okay, that isn't helpful. An int variable is an int object. A vehicle is a Vehicle object. You are a reader object. I am an author object — okay, forget that one.

The following code segment creates a car of class Vehicle:

```
Vehicle myCar;
myCar = new Vehicle();
```

The first line declares a variable myCar of type Vehicle, just like you can declare a somethingOrOther of class int. (Yes, a class is a type, and all C# objects are defined as classes.) The new Vehicle() command creates a specific object of type Vehicle and stores the location into the variable myCar. The new has nothing to do with the age of myCar. (My car could qualify for an antique license plate if it weren't so ugly.) The new operator creates a new block of memory in which your program can store the properties of myCar.

In C# terms, you say that myCar is an object of class Vehicle. You also say that myCar is an instance of Vehicle. In this context, instance means "an example of" or "one of." You can also use the word instance as a verb, as in instantiating Vehicle. That's what new does.
