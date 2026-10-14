Click here to view code image

```
static double ParallelPI()
{
    ...
    Parallel.For(0, NUMPOINTS, (x) =>
    {
        int xCoord;
        int yCoord;

        lock(pointsList)
        {
            xCoord = random.Next(RADIUS);
            yCoord = random.Next(RADIUS);
        }

        double distanceFromOrigin = Math.Sqrt(xCoord * xCoord + yCoord * yCoord);
        pointsList.Add(distanceFromOrigin);
        doAdditionalProcessing();
    });
    ...
}
```

Notice that the xCoord and yCoord variables are declared outside the lock statement. You do this because the lock statement defines its own scope, and any variables defined within the block specifying the scope of the lock statement disappear when the construct exits.

3. On the Debug menu, click Start Without Debugging.

This time, the values of pi calculated by the SerialPI and ParallelPI methods are the same. The only difference is that the ParallelPI method runs more quickly.

![](bbox=[0.15, 0.62, 0.845, 0.755])

4. Close the console window, and return to Visual Studio.

# Summary

In this chapter, you saw how to define asynchronous methods by using the async modifier and the await operator. Asynchronous methods are based on tasks, and the await operator specifies the points at which a task can be used to perform asynchronous processing.

You also learned a little about PLINQ and how you can use the AsParallel