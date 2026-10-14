(you will add the code to do this later in this set of exercises), run it, and display the time taken. The code for each of these methods is almost completely separate from the statements that actually create and run the queries.

# 3. Examine the Test1 method.

This method creates a large array of integers and populates it with a set of random numbers between 0 and 200. The random number generator is seeded, so you should get the same results every time you run the application.

# 4. Immediately after the first TODO comment in this method, add the LINQ query shown here in bold:

Click here to view code image

```
// TO DO: Create a LINQ query that retrieves all numbers that are greater than 100
var over100 = from n in numbers
    where TestIfTrue(n > 100)
    select n;
```

This LINQ query retrieves all the items in the numbers array that have a value greater than 100. The test n > 100 is not by itself computationally intensive enough to show the benefits of parallelizing this query, so the code calls a method named TestIfTrue, which slows it down a little by performing a SpinWait operation. The SpinWait method causes the processor to continually execute a loop of special “no operation” instructions for a short period of time, keeping the processor busy but not actually doing any work. (This is known as spinning.) The TestIfTrue method looks like this:

Click here to view code image

```
public static bool TestIfTrue(bool expr)
{
    Thread.SpinWait(1000);
    return expr;
}
```

# 5. After the second TODO comment in the Test1 method, add the following code shown in bold:

Click here to view code image

```
// TO DO: Run the LINQ query, and save the results in a List<int> object
List<int> numbersOver100 = new List<int>(over100);
```

Remember that LINQ queries use deferred execution, so they do not run until you retrieve the results from them. This statement creates a List<int> object and populates it with the results of running the over100 query.