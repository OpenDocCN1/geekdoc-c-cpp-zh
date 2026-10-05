
![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_940_0.png)

Apart from the timing, your result should be the same as that shown, 3.1414888, unless you've changed the NUMPOINTS, RADIUS, or SEED constants.

10. Close the console window and return to Visual Studio.

In the SerialPI method, the code in the for loop that generates the points and calculates their distance from the origin is an obvious area that can be parallelized. This is what you'll do in the next exercise.

### To calculate pi by using parallel tasks

- 1. In Solution Explorer, double-click Program.cs to display the file in the Code and Text Editor if it is not already open.

- 2. Locate the ParallelPI method. It contains the same code as the initial version of the SerialPI method before you added the code to the try block to calculate pi.

- 3. In the try block, delete the comment and remove the return statement.
Then add the Parallel.For statement shown here in bold to the try block:

Click here to view code image

```
try {
  Parallel.For (0, NUMPOINTS, (x) => {
    int xCoord = random.Next(RADIUS);
    int yCoord = random.Next(RADIUS);
    double distanceFromOrigin = Math.Sqrt(xCoord * xCoord + yCoord * yCoord);
    pointsList.Add(distanceFromOrigin);
    doAdditionalProcessing();
  });
}
```

This construct is the parallel analog of the code in the for loop in the SerialPI method. The body of the original for loop is wrapped in a lambda expression. Remember that each iteration of the for loop is performed by a task, and tasks can run in parallel. The degree of parallelism depends on the number of processor cores and other resources available on your computer.

- 4. Add the following code shown in bold to the try block, after the Parallel.For statement. This code is the same as the corresponding statements in the SerialPI method.

Click here to view code image

```
try {
  Parallel.For (...\  {
    ...
  });

  foreach (double datum in pointsList) {
    if (datum <= RADIUS) {
      numPointsInCircle++;
    }
  }
```

```
}

double pi = 4.0 * numPointsInCircle / NUMPOINTS;
return pi;
}
```

- 5. In the Main method near the end of the Program.cs file, uncomment the code that calls the ParallelPI method and the Console.WriteLine statement that displays the results.

- 6. On the Debug menu, select Start Without Debugging.

The program runs. The following image shows the typical output. (Your timings might be different; I was using a quad-core processor.)

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_942_0.png)

The ParallelPI method runs a lot more quickly than the SerialPI method. However, although the value calculated by the SerialPI method should be exactly as before, the result of the ParallelPI method, 3.8035444, looks a little suspect. The random number generator is seeded with the same value as used by the SerialPI method, so it should produce the same sequence of random numbers with the same result and the same number of points within the circle. Moreover, if you run the application again, you should get the same value of pi for the SerialPI method but calculated by the ParallelPI method is likely to be different (and still inaccurate). Another curious point is that the pointsList collection in the ParallelPI method seems to contain fewer points than the same collection in the SerialPI method.

> Note: If the pointsList collection actually contains the expected number of items, run the application again. You should find that it contains fewer items than expected in most (but not necessarily all) runs.

- 7. Close the console window and return to Visual Studio.

What went wrong with the parallel calculation? A good place to start is the number of items in the pointsList collection. This collection is a generic List<double> object. However, this type is not thread-safe. The code in the Parallel.For statement calls the Add method to append a value to the collection, but remember that this code is being executed by tasks running as concurrent threads. Consequently, it is highly probable that some of the calls being added to the collection, will interfere with one another and cause some corruption. A solution is to use a collection from the System.Collections.Concurrent namespace because these collections are thread-safe. The generic ConcurrentBag<T> class in this namespace is probably the most suitable collection to use for this example.

## To use a thread-safe collection

- 1. In Solution Explorer, double-click Program.cs to display the file in the Code and Text window if it is not already open.
- 2. Add the following using directive to the list at the top of the file:

Click here to view code image
`using System.Collections.Concurrent;`
- 3. Locate the ParallelPI method. At the start of this method, replace the statement that instantiates the List<double> collection with code that creates a ConcurrentBag<double> collection instead, as shown in bold in the following code example:

Click here to view code image

```
static double ParallelPI()
{
    ConcurrentBag<double> pointsList = new ConcurrentBag<double>();
    Random random = ...;
}
```

Notice that you cannot specify a default capacity for this class, so the constructor does not take a parameter.

You don't need to change any other code in this method; you add an item to a ConcurrentBag<T> collection using the Add method, which is the same mechanism that you use to add an item to a List<T> collection.

- 4. On the Debug menu, select Start Without Debugging.

The program runs and displays its approximation of pi by using the SerialPI and ParallelPI methods. The following image shows the typical output:

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_944_0.png)

This time, the pointsList collection in the ParallelPI method contains the correct number of points, but the value should be the same as that reported by the SerialPI method.

Also note that the time taken by the ParallelPI method has increased compared with the previous exercise. This is because the ConcurrentBag<T> class have to lock and unlock data to guarantee thread safety, and this process adds to calling these methods. Keep this in mind when you're considering whether it's appropriate to parallelize an operation.

- 5. Close the console window, and return to Visual Studio.

You currently have the correct number of points in the pointsList collection, but the value recorded for each of these points is questionable. The code in the Parallel.For construct calls the Next method of a Random object, but like the methods in the generic List<T> class, this method is not thread-safe. Sadly, there is no concurrent version of the Random class, so you must resort to using an alternative technique to serialize calls. Because each invocation is relatively brief, it makes sense to use a simple lock to guard this.

## To use a lock to serialize method calls

- 1. In Solution Explorer, double-click Program.cs to display the file in the Code and Text Editor if it is not already open.
- 2. Locate the ParallelPI method. Modify the code in the lambda expression in the Parallel.For statement to protect the calls to random.Next by using a lock statement. Specify the pointsList collection as the subject of the lock, as shown here in:

Click here to view code image

```
static double ParallelPI()
{
    Parallel.For(0
```

```
{
  xCoord = random.Next(RADIUS);
  yCoord = random.Next(RADIUS);
}

double distanceFromOrigin = Math.Sqrt(xCoord * xCoord + yCoord * yCoord);
pointsList.Add(distanceFromOrigin);
doAdditionalProcessing();
});
```

Notice that the xCoord and yCoord variables are declared outside the lock statement. You do do this because the lock statement defines its own scope, and any variables defined within the block specifying the scope of the lock statement disappear when the construct exits.

- On the Debug menu, select Start Without Debugging.

This time, values of pi calculated by the SerialPI and ParallelPI methods are the same. The only difference is that the ParallelPI method runs much more quickly.

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_946_0.png)

- Close the console window, and return to Visual Studio.
