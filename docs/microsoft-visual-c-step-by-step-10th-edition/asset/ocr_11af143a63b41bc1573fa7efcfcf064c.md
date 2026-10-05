ensure the repeatability of the tests.) Return to Visual Studio when you've finished.

10. The logic that selects each item returned by the LINQ query is independent of the selection logic for all other items, so this query is an ideal candidate for partitioning. Modify the statement that defines the LINQ query, and specify the AsParallel extension method to the numbers array, as you have in bold:

Click here to view code image

```
var over100 = from n in numbers.AsParallel()
where TestIfTrue(n > 100)
select n;
```

> Note
If the selection logic or calculations require access to shared data, you must synchronize the tasks that run in parallel. Otherwise, the results might be unpredictable. However, synchronization can impose an overhead and might negate the benefits of parallelizing the test.

11. On the Debug menu, select Start Without Debugging. Verify that the number of items reported by Test1 is the same as before but that the time taken to perform the test has decreased significantly. Run the several times and take an average of the duration required for the test.

If you're running on a dual-core processor or a twin-processor computer, you should see the time reduced by 40 to 45 percent. If you have more processor cores, the decrease should be even more dramatic. On my quad-core machine, the processing time dropped from 9.5 seconds to 3.3 seconds.

12. Close the application and return to Visual Studio.

The preceding exercise shows the performance improvement you can attain by making a small change to a LINQ query. However, keep in mind that you