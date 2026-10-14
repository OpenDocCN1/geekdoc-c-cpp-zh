
in the next few steps.

6. In the try block, delete the comment and remove the return statement. (This statement was provided only to ensure that the code compiles.) Add to the try block the for block and statements shown in bold in the following code:

Click here to view code image

```
try
{
    for (int points = 0; points < NUMPOINTS; points++)
    {
        int xCoord = random.Next(RADIUS);
        int yCoord = random.Next(RADIUS);
        double distanceFromOrigin = Math.Sqrt(xCoord * xCoord +
 yCoord * yCoord);
        pointsList.Add(distanceFromOrigin);
        doAdditionalProcessing();
    }
}
```

This block of code generates a pair of coordinate values that lie in the range 0 to RADIUS, and it stores them in the xCoord and yCoord variables. The code then employs Pythagoras’s theorem to calculate the distance of these coordinates from the origin and adds the result to the pointsList collection.

## Note

Although there is a little bit of computational work performed by this block of code, in a real-world scientific application you are likely to include far more complex calculations that will keep the processor occupied for longer. To simulate this situation, this block of code calls another method, doAdditionalProcessing. All this method does is occupy a number of CPU cycles as shown in the following code sample. I opted to follow this approach to better demonstrate the data synchronization requirements of multiple tasks rather than have you write an application that performs a highly complex calculation such as a fast Fourier transform (FFT) to keep the CPU busy:

Click here to view code image

```
private static void doAdditionalProcessing()
{
    Thread.SpinWait(SPINWAITS);
}
```

SPINWAITS is another constant defined at the top of the Program class.

7. In the SerialPI method, in the try block, after the for block, add the foreach statement shown in bold in the following example.

Click here to view code image

```
try
{
    for (int points = 0; points < NUMPOINTS; points++)
    {
        ...
    }
    
    foreach (double datum in pointsList)
    {
        if (datum <= RADIUS)
        {
            numPointsInCircle++;
        }
    }
}
```

This code iterates through the pointsList collection and examines each value in turn. If the value is less than or equal to the radius of the circle, it increments the numPointsInCircle variable. At the end of this loop, numPointsInCircle should contain the total number of coordinates that were found to lie within the bounds of the circle.

8. After the foreach statement, add to the try block the following statements shown in bold:

Click here to view code image

```
try
{
    for (int points = 0; points < NUMPOINTS; points++)
    {
        ...
    }
    
    foreach (double datum in pointsList)
    {
        ...
    }
    
    double pi = 4.0 * numPointsInCircle / NUMPOINTS;
    return pi;
}
```

The first statement calculates pi based on the ratio of the number of points that lie within the circle to the total number of points, using the formula described earlier. The value is returned as the result of the method.

9. On the Debug menu, click Start Without Debugging.

The program runs and displays its approximation of pi, as shown in the following image. (It took just over 46 seconds on my computer, so be prepared to wait for a little while.) The time taken to calculate the result also appears.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_694_0.png)

## Note

Apart from the timing, your results should be the same unless you have changed the NUMPOINTS, RADIUS, or SEED constants.

10. Close the console window, and return to Visual Studio.

In the SerialPI method, the code in the for loop that generates the points and calculates their distance from the origin is an obvious area that can be parallelized. This is what you will do in the next exercise.

## Calculate pi by using parallel tasks

- 1. In Solution Explorer, double-click Program.cs to display the file in the Code and Text Editor window if it is not already open.
- 2. Locate the ParallelPI method. It contains the same code as the initial version of the SerialPI method before you added the code to the try block to calculate pi.
- 3. In the try block, delete the comment and remove the return statement. Add the Parallel.For statement shown here in bold to the try block:

Click here to view code image

```
try
{
    Parallel.For (0, NUMPOINTS, (x) =>
    {
        int xCoord = random.Next(RADIUS);
        int yCoord = random.Next(RADIUS);
        double distanceFromOrigin = Math.Sqrt(xCoord * xCoord + yCoord * yCoord);
        pointsList.Add(distanceFromOrigin);
        doAdditionalProcessing();
    });
}
```

This construct is the parallel analog of the code in the for loop in the SerialPI method. The body of the original for loop is wrapped in a lambda expression. Remember that each iteration of the loop is performed by using a task, and tasks can run in parallel. The degree of parallelism depends on the number of processor cores and other resources available on your computer.

4. Add the following code shown in bold to the try block, after the Parallel.For statement. This code is the same as the corresponding statements in the SerialPI method.

Click here to view code image

```
try
{
  Parallel.For (...)
  {
    ...
  });

  foreach (double datum in pointsList)
  {
    if (datum <= RADIUS)
    {
      numPointsInCircle++;
    }
  }

  double pi = 4.0 * numPointsInCircle / NUMPOINTS;
  return pi;
}
```

5. In the Main method near the end of the Program.cs file, uncomment the code that calls the ParallelPI method and the Console.WriteLine statement that displays the results.

6. On the Debug menu, click Start Without Debugging.

The program runs. The following image shows the typical output (your timings might be different; I was using a quad-core processor):

![](img/16f6e3fe08f01ddadb2741a92c392b0e_695_0.png)

The value calculated by the SerialPI method should be exactly as before, but the result of the ParallelPI method actually looks a little suspect. The random number generator is seeded with the same value as that used by the SerialPI method, so it should produce the same sequence of random numbers with the same result and the same number of points within the circle. Another curious point is that the pointsList collection in the ParallelPI method seems to contain fewer points than the same collection in the SerialPI method.

## Note

If the pointsList collection actually contains the expected number of items, run the application again. You should find that it contains fewer items than expected in most (but not necessarily all) runs.

7. Close the console window, and return to Visual Studio.

What went wrong with the parallel calculation? A good place to start is the number of items in the pointsList collection. This collection is a generic List<double> object. However, this type is not thread safe. The code in the Parallel.For statement calls the Add method to append a value to the collection, but remember that this code is being executed by tasks running as concurrent threads. Consequently, given the number of items being added to the collection, it is highly probable that some of the calls to Add will interfere with one another and cause some corruption. A solution is to use one of the collections from the System.Collections.Concurrent namespace because these collections are thread safe. The generic ConcurrentBag<T> class in this namespace is probably the most suitable collection to use for this example.

## Use a thread-safe collection

- 1. In Solution Explorer, double-click Program.cs to display the file in the Code and Text Editor window if it is not already open.
- 2. Add the following using directive to the list at the top of the file:
- 3. Locate the ParallelPI method. At the start of this method, replace the statement that instantiates the List<double> collection with code that creates a ConcurrentBag<double> collection, as shown in bold in the following code example:

Click here to view code image

```
using System.Collections.Concurrent;
```

Click here to view code image

```
static double ParallelPI()
{
    ConcurrentBag<double> pointsList = new ConcurrentBag<double>();
    Random random = ...;
    ...
}
```

Notice that you cannot specify a default capacity for this class, so the
