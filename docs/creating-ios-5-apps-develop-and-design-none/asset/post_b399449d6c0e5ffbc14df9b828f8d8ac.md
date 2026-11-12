
Finally, in C you must define the function before it is used. Most of the time we simply place a function declaration in a corresponding header file (filename ending in .h). The function declaration is just the function signature followed by a semicolon.

```c
CGFloat calculateDistance(CGPoint p1, CGPoint p2);
```

We can then import the header file before using the function anywhere else in our application.

## PASS BY VALUE

In C, all functions pass their arguments by value. This means the compiler makes local copies of the arguments. Those copies are used within the function and are removed from memory when the function returns. In general, this means you can do whatever you want to the local copy, and the original value will remain unchanged. That is a very good thing. Check out the following examples.

```c
void inner(int innerValue) {
    printf("innerValue = %d\n", innerValue);
    innerValue += 20;
    printf("innerValue = %d\n", innerValue);
}
void outer() {
    int outerValue = 10;
    printf("outerValue = %d\n", outerValue);
    inner(outerValue);
    printf("outerValue = %d\n", outerValue);
}
```

Here, printf() will replace the %d specifiers with an int value. Calling outer() prints the following series of messages to the console:

```text
outerValue = 10
innerValue = 10
innerValue = 30
outerValue = 10
```

As you can see, the value of outerValue does not change when we modify innerValue. However, this is only half of the story. Consider the following code:

```c
void inner(int* innerPointer) {
    printf("innerValue = %d\n", *innerPointer);
    *innerPointer += 20;
    printf("innerValue = %d\n", *innerPointer);
}

void outer() {
    int buffer = 10;
    int* outerPointer = &buffer;
    printf("outerValue = %d\n", *outerPointer);
    inner(outerPointer);
    printf("outerValue = %d\n", *outerPointer);
}
```

Superficially, this looks very similar to the earlier code. However, there are some important differences. First, we create a buffer variable and set its value to 10. We then create a pointer to this buffer and pass that pointer into the inner() function. Then, inner() modifies the value pointed at by its innerPointer argument. This time, we get the following output:

```text
outerValue = 10
innerValue = 10
innerValue = 30
outerValue = 30
```

Here, both the innerValue and the outerValue change. We're still passing our argument by value. However, this time the value is the address of the buffer variable. The inner() function receives a copy of this address—but the address still points to the same piece of data in memory. When we dereference the pointer (either to modify it or to print out its value), we are actually accessing the buffer's value.

## OBJECTS VS. CLASSES

When we talk about objects, we typically talk about two different aspects: the class and the object itself. The class is the technical specification. It describes the methods and instance variables that the object will have. An object, on the other hand, is an instantiation of a class in memory. You can create multiple objects from a single class—each one will have the same set of features, but the individual values will be independent from each other. Setting an instance variable or calling a method on one object does not affect any other objects of the same class.

Think of it this way: The class is the blueprint, the object is the house. You can build several different houses from the same blueprint. Each house will have a `setThermostatToTemperature:` method; however, calling `setThermostatToTemperature:` on my house will not affect the thermostat settings in yours.

### OBJECTS

All the language features we’ve discussed so far come from C. However, with the introduction of objects, we leave C behind and enter the world of Objective-C.

Superficially, an object combines the data management of structs with a set of related functions (though in this case we call them methods). Under the hood, that’s exactly how they are implemented; however, objects give us several advantages over generic C code.

### ENCAPSULATION

Encapsulation is one of the main advantages of object-oriented code. Objects should hide away much of their complexity, only exposing those functions and values that a developer needs to use them effectively.

To put it another way, objects function as black boxes. They have a public interface, which describes all the methods and values that can be accessed from the outside. The actual implementation of the object may include any number of private instance variables and methods; however, you shouldn’t need to know anything about these details in order to use the object in your code.

Since Objective-C is a highly dynamic, reflexive programming language, the public interface is more of a suggestion than a strict rule of law. You can always gain access to hidden instance variables and methods, but doing so breaks encapsulation. This is bad. Sure, it may make things easier in the short term, but you're probably setting yourself up for long-term pain.

In an ideal world, an object's interface should remain static and unchanging. You can add new methods over time, but you shouldn't remove or alter any existing methods. The interior details, however, are fair game. The object's developer may completely redesign the implementation from one build to the next, and as long as the rest of your code only interacts with the object through its interface, everything will continue to function properly.

Of course, we live in the real world, and we often need to alter an object's interface, especially during early development. This isn't a big deal if you're the only one using the object—but if other people depend on your classes, you will need some way of coordinating these changes with them.

Apple, for example, will occasionally mark methods as deprecated. These methods will continue to operate as normal; however, developers should stop using them, because they will disappear in some future release. This gives developers an opportunity to redesign their applications before these changes take effect.

### INHERITANCE

Inheritance is the second main benefit of object-oriented code. One class can inherit the instance variables and methods of another—and can then modify those methods or add new methods and instance variables to further specialize the new class. Most importantly, we can still use the subclasses wherever we could have used the superclasses.

Say, for example, we have a class called Vehicle. This contains all the common features of a vehicle: methods to allow you to set or retrieve the driver, passengers, cargo, current location, destination, and so on. You might even have some methods to query the vehicle's capabilities: canOperateOnLand, canOperateOnWater, canFly, cruiseSpeed, and so on.

We could then create subclasses that all inherit from Vehicle—Boat, Airplane, and Car. The Boat subclass would override the canOperateOnWater method to return YES. Airplane would similarly override canFly.

Finally, we might make Maserati and Yugo subclasses of Car. Maserati's cruise speed would return 150 MPH, while Yugo's would return 15 MPH (or something close to that, I'm sure).

![](img/fe9fea534a8e7868f811f7cd33da015f_77_0.png)

Then let's say we have a function that consumes vehicles: canVehicleReachLocationInTime(Vehicle* vehicle, Location* location, Time* deadline). We could pass any instance of Boat, Airplane, Car, Maserati, or Yugo to this function. Similarly, we could pass any Car, Maserati, or Yugo object to the estimatedTimeToFinishIndy500(Car* sampleCar) function.

We will frequently run into inheritance and class hierarchies when we interact with Cocoa Touch view objects (**Figure 2.1**). UIView inherits from UIResponder, which inherits from NSObject. NSObject is a root class—almost all other objects inherit from it. There are a few exceptions (e.g., NSProxy) but these are unusual corner cases.

The NSObject root class ensures that all objects have a basic set of methods (memory management, testing for equality, testing for class membership, and the like). Next, UIResponder adds an interface for objects that respond to motion and touch events, allowing them to participate in the responder chain. Finally, UIView adds support for managing and displaying rectangular regions on the screen.

Figure 2.1 also shows a few subclasses of UIView. As you can see, some screen elements (like UILabel) inherit directly from UIView. Others (UIButton and UITextField) inherit from UIControl, which adds support for registering targets for events, and for dispatching action messages when the events occur.
