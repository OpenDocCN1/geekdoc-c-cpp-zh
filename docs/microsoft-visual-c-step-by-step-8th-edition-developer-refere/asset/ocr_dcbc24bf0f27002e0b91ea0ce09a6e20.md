Click here to view code image

```
class Point
{
    ...
    public static int ObjectCount() => objectCount;
}
```

5. Display the Program class in the Code and Text Editor window. Add a statement to the doWork method to write the value returned from the ObjectCount method of the Point class to the screen, as shown in bold type in the following code example:

Click here to view code image

```
static void doWork()
{
    Point origin = new Point();
    Point bottomRight = new Point(1366, 768);
    double distance = origin.distanceTo(bottomRight);
    Console.WriteLine($"Distance is: {distance}");
    Console.WriteLine($"Number of Point objects: {Point.ObjectCount()}");
}
```

The ObjectCount method is called by referencing Point, the name of the class, and not the name of a Point variable (such as origin or bottomRight). Because two Point objects have been created by the time ObjectCount is called, the method should return the value 2.

6. On the Debug menu, click Start Without Debugging.

Confirm that the message “Number of Point objects: 2” is written to the console window (after the message displaying the value of the distance variable).

7. Press Enter to close the program and return to Visual Studio 2015.

# Anonymous classes

An anonymous class is a class that does not have a name. This sounds rather strange, but it is actually quite handy in some situations that you will see later in this book, especially when using query expressions. (You learn about query expressions in Chapter 20, “Decoupling application logic and handling events.”) For the time being, you’ll have to take it on faith that they are useful.

You create an anonymous class simply by using the new keyword and a pair of braces defining the fields and values that you want the class to contain, like this:

Click here to view code image

```
myAnonymousObject = new { Name = "John", Age = 47 };
```

This class contains public fields called Name (initialized to the string “John”)