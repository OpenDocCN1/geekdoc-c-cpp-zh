
System.Collections.Concurrent namespace that are designed specifically for use with tasks. The following list briefly summarizes the key types in this namespace:

- **ConcurrentBag<T>** This is a general-purpose class for holding an unordered collection of items. It includes methods to insert (*Add*), remove (*TryTake*), and examine (*TryPeek*) items in the collection. These methods are thread safe. The collection is also enumerable, so you can iterate over its contents by using a *foreach* statement.
- **ConcurrentDictionary<TKey, TValue>** This class implements a thread-safe version of the generic *Dictionary<TKey, TValue>* collection class described in Chapter 18, “Using collections.” It provides the methods *TryAdd*, *ContainsKey*, *TryGetValue*, *TryRemove*, and *TryUpdate*, which you can use to add, query, remove, and modify items in the dictionary.
- **ConcurrentQueue<T>** This class provides a thread-safe version of the generic *Queue<T>* class described in Chapter 18. It includes the methods *Enqueue*, *TryDequeue*, and *TryPeek*, which you can use to add, remove, and query items in the queue.
- **ConcurrentStack<T>** This is a thread-safe implementation of the generic *Stack<T>* class, also described in Chapter 18. It provides methods such as *Push*, *TryPop*, and *TryPeek*, which you can use to push, pop, and query items on the stack.

## Note

Adding thread safety to the methods in a collection class imposes additional run-time overhead, so these classes are not as fast as the regular collection classes. You need to keep this fact in mind when deciding whether to parallelize a set of operations that requires access to a shared collection.

## Using a concurrent collection and a lock to implement thread-safe data access

In the following set of exercises, you will implement an application that calculates pi by using a geometric approximation. Initially, you will perform the calculation in a single-threaded manner, and then you will change the code to perform the calculation by using parallel tasks. In the process, you will uncover some data synchronization issues that you need to address and that you will solve by using a concurrent collection class and a lock to ensure that the tasks coordinate their activities correctly.

The algorithm that you will implement calculates pi based on some simple

mathematics and statistical sampling. If you draw a circle of radius r and draw a square with sides that touch the circle, the sides of the square are 2 * r in length, as shown in the following image:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_688_0.png)

You can calculate the area of the square, S, like this

```
S = (2 * r) * (2 * r)
```

or

```
S = 4 * r * r
```

The area of the circle, C, is calculated as follows:

```
C = pi * r * r
```

Rearranging these formulas, you can see that

```
r * r = C / pi
```

and

```
r * r = S / 4
```

Combining these equations, you get:

```
S / 4 = C / pi
```

And therefore:

```
pi = 4 * C / S
```

The trick is to determine the value of the ratio of the area of the circle, C, with

respect to the area of the square, S. This is where the statistical sampling comes in. You can generate a set of random points that lie within the square and count how many of these points also fall within the circle. If you generate a sufficiently large and random sample, the ratio of points that lie within the circle to the points that lie within the square (and also in the circle) approximates the ratio of the areas of the two shapes, C / S. All you have to do is count them.

How do you determine whether a point lies within the circle? To help visualize the solution, draw the square on a piece of graph paper with the center of the square at the origin, point (0,0). You can then generate pairs of values, or coordinates, that lie within the range (-r, -r) to (+r, +r). You can determine whether any set of coordinates (x, y) lie within the circle by applying the Pythagorean theorem to determine the distance d of these coordinates from the origin. You can calculate d as the square root of ((x * x) + (y * y)). If d is less than or equal to r, the radius of the circle, the coordinates (x, y) specify a point within the circle, as shown in the following diagram:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_689_0.png)

You can simplify matters further by generating coordinates that lie only in the upper-right quadrant of the graph so that you only have to generate pairs of random numbers between 0 and r. This is the approach you will take in the exercises.

## Note

The exercises in this chapter are intended to be run on a computer with a multicore processor. If you have only a single-core CPU, you will not observe the same effects. Also, you should not start any additional programs or services between exercises, because these might affect the results you see.

## Calculate pi by using a single thread

- 1. Start Visual Studio 2015 if it is not already running.
- 2. Open the CalculatePI solution, which is located in the \Microsoft Press\VCSBS\Chapter 24\CalculatePI folder in your Documents folder.
- 3. In Solution Explorer, in the CalculatePI project, double-click Program.cs to display the file in the Code and Text Editor window.
- This is a console application. The skeleton structure of the application has already been created for you.
- 4. Scroll to the bottom of the file and examine the Main method. It looks like this:

Click here to view code image

```
static void Main(string[] args)
{
    double pi = SerialPI();
    Console.WriteLine($"Geometric approximation of PI calculated serially: {pi}");

    Console.WriteLine();
    // pi = ParallelPI();
    // Console.WriteLine($"Geometric approximation of PI calculated in parallel: {pi}");
}
```

This code calls the SerialPI method, which calculates pi by using the geometric algorithm described before this exercise. The value is returned as a double and displayed. The code that is currently commented out calls the ParallelPI method, which performs the same calculation but by using concurrent tasks. The result displayed should be the same as that returned by the SerialPI method.

- 5. Examine the SerialPI method.

Click here to view code image

```
static double SerialPI()
{
    List<double> pointsList = new List<double>();
```

```
Random random = new Random(SEED);
int numPointsInCircle = 0;
Stopwatch timer = new Stopwatch();
timer.Start();

try
{
    // TO DO: Implement the geometric approximation of PI
    return 0;
}
finally
{
    long milliseconds = timer.ElapsedMilliseconds;
    Console.WriteLine($"SerialPI complete: Duration: {milliseconds} ms");
    Console.WriteLine(
        $"Points in pointsList: {pointsList.Count}. Points within circle: {numPointsInCircle}");
}
```

This method generates a large set of coordinates and calculates the distances of each set of coordinates from the origin. The size of the set is specified by the constant NUMPOINTS at the top of the Program class. The bigger this value is, the greater the set of coordinates and the more accurate the value of pi calculated by this method. If your computer has sufficient memory, you can increase the value of NUMPOINTS. Similarly, if you find that the application throws OutOfMemoryException exceptions when you run it, you can reduce this value.

You store the distance of each point from the origin in the pointsList List<double> collection. The data for the coordinates is generated by using the random variable. This is a Random object, seeded with a constant to generate the same set of random numbers each time you run the program. (This helps you determine that it is running correctly.) You can change the SEED constant at the top of the Program class if you want to seed the random number generator with a different value.

You use the numPointsInCircle variable to count the number of points in the pointsList collection that lie within the bounds of the circle. The radius of the circle is specified by the RADIUS constant at the top of the Program class.

To help you compare performance between this method and the ParallelPI method, the code creates a Stopwatch variable called timer and starts it running. The finally block determines how long the calculation took and displays the result. For reasons that will be described later, the finally block also displays the number of items in the pointsList collection and the number of points that it found that lie within the circle.

You will add the code that actually performs the calculation to the try block
