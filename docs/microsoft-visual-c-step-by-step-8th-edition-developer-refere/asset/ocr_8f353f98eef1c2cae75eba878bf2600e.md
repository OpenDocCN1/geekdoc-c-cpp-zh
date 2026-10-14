a task, and tasks can run in parallel. The degree of parallelism depends on the number of processor cores and other resources available on your computer.

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

![](bbox=[0.15, 0.66, 0.84, 0.79])

The value calculated by the SerialPI method should be exactly as before, but the result of the ParallelPI method actually looks a little suspect. The random number generator is seeded with the same value as that used by the SerialPI method, so it should produce the same sequence of random numbers with the same result and the same number of points within the circle. Another curious point is that the pointsList collection in the