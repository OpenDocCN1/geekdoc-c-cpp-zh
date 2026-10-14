12. In the Program.cs file, edit the body of the doWork method. Declare a variable called bottomRight of type Point, and initialize it to a new Point object by using the constructor with two arguments, as shown in bold type in the code that follows. Supply the values 1366 and 768, representing the coordinates at the lower-right corner of the screen based on the resolution 1366 × 768 (a common resolution for many tablet devices). The doWork method should now look like this:

Click here to view code image

```
static void doWork()
{
    Point origin = new Point();
    Point bottomRight = new Point(1366, 768);
}
```

13. On the Debug menu, click Start Without Debugging.

The program builds and runs, displaying the following messages to the console:

![](bbox=[0.2, 0.41, 0.8, 0.62])

14. Press the Enter key to end the program and return to Visual Studio 2015.
You will now add two int fields to the Point class to represent the x- and y-coordinates of a point, and you will modify the constructors to initialize these fields.

15. Edit the Point class in the Point.cs file by adding two private fields, called x and y, of type int, as shown in bold type in the code that follows. The Point class should now look like this:

Click here to view code image

```
class Point
{
    private int x, y;

    public Point()
    {
        Console.WriteLine("default constructor called");
    }
}
```