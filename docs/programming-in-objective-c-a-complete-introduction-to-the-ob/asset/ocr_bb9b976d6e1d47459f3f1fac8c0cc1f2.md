# Chapter 3 Classes, Objects, and Methods

The two-line sequence of allocating a new instance of class and then initializing it is done so often in Objective-C that the two messages are typically combined, as follows:

```
myFraction = [[Fraction alloc] init];
```

This inner message expression is evaluated first:

```
[Fraction alloc]
```

As you know, the result of this message expression is the actual Fraction that is allocated. Instead of storing the result of the allocation in a variable, as you did before, you directly apply the init method to it. So, again, first you allocate a new Fraction and then initialize it. The result of the initialization is assigned to your myFraction variable.

As a shorthand technique, the allocation and initialization is often incorporated directly into the declaration line, as in the following:

```
Fraction *myFraction = [[Fraction alloc] init];
```

We use this style throughout the remainder of this book, so it's important that you understand it. You've seen it in program up to this point with the allocation of the autorelease pool

```
NSAutleasePool * pool = [[NSAutleasePool alloc] init];
```

Here an alloc message is sent to the NSleasePool class requesting a new instance be created. The init message is sent to the newly created object to get it initialized.

Returning to Program 3.2, you are now ready to set the value of your fraction. These program lines do just that:

```
// Set fraction to numerator: 1;
[myFraction setDenominator:3];
```

The first message statement sends the setNumerator: message to myFraction. The argument that is supplied is the value 1. Control is sent to the setNumerator: method you defined for your Fraction class. The Objective-C system knows that it is the method from this class to use because it knows that myFraction is an object from the Fraction class.

Inside the setNumerator: method, the passed value of 1 is stored inside the variable n. The single program line in that method stores value in the instance variable numerator. So you have effectively set the numerator of myFraction to 1.

The message invokes the setDenominator: method on myFraction follows next. The argument of 3 is assigned to the variable d inside the setDenominator: method. This value is stored inside the denominator instance variable, thus completing the