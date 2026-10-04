# Chapter 10

# Abstract Data Types in C++ (Classes)

The object named c, however, is defined with the arguments 4, 1, and 2000. These arguments are passed to the constructor function when the object is defined, resulting in the following initialization of c's data members:

```
c.month = 4
c.day = 1
c.year = 2000
```

The next statement in main(), b.setDate(12,25,2006), calls b's setDate() function, which assigns the values 12, 25, and 2006 to b's data members, in this assignment:

```
b.month = 12
b.day = 25
b.year = 2006
```

Notice the syntax for calling an object's method:

```
objectName.methodName(parameters)
```

The objectName is the name of a specific object, and methodName is the name of the function defined for the class. Because all class functions have been defined as public, a statement such as b.setDate(12,25,2006) is valid inside the main() function and a call to c's class setDate() function. This statement sets the setDate() function to operate on the b object with arguments 12, 25, and 2006. It's important to understand that because all class data members were specified as private, a statement such as b.month = 12 would be invalid inside main(). Therefore, you're forced to rely on member functions to access data value members.

The last three statements in main() call the showDate() function to operate on a, and c objects. The first call results in the display of a's data values, the second call in the display of b's data values, and the third call in the display of c's data values. Therefore, the output of Program 10.1 is the following:

```
The date is 07/04/05
The date is 12/25/06
The date is 04/01/00
```

Notice that a statement such as cout <<; is valid inside main() because cout doesn't know how to handle an object of class Date. Therefore, the Date class is supplied with a function that can be used to access and display an object's intervals.

# Terminology

As there's sometimes confusion about the classes, objects, and other object-oriented programming terminology, taking a moment to clarify and review the terminology is helpful.