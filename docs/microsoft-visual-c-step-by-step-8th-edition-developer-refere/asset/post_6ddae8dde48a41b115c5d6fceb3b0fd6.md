
10. Verify that Test2 retrieves 830 orders, and note the duration of the test. Run the application several times to obtain an average duration, and then return to Visual Studio.

11. In the Test2 method, modify the LINQ query and add the AsParallel extension method to the Customers and Orders arrays, as shown here in bold:

```
var orderInfoQuery = from c in
CustomersInMemory.Customers.AsParallel()
    join o in OrdersInMemory.Orders.AsParallel()
    on c.Split(',')[0] equals o.Split(',')[1]
    select new OrderInfo
    {
        CustomerID = c.Split(',')[0],
        CompanyName = c.Split(',')[1],
        OrderID = Convert.ToInt32(o.Split(',')[0]),
        OrderDate =
Convert.ToDateTime(o.Split(',')[2],
            New CultureInfo("en-US"))
    };
```

## Warning

When you join two data sources in this way, they must both be IEnumerable objects or ParallelQuery objects. This means that if you specify the AsParallel method for one source, you should also specify AsParallel for the other. If you fail to do this, your code will not run—it will stop with an error.

12. Run the application several times. Notice that the time taken for Test2 should be significantly less than it was previously. PLINQ can make use of multiple threads to optimize join operations by fetching the data for each part of the join in parallel.

13. Close the application and return to Visual Studio.

These two simple exercises have shown you the power of the AsParallel extension method and PLINQ. Note that PLINQ is an evolving technology, and the internal implementation is very likely to change over time. Additionally, the volumes of data and the amount of processing you perform in a query also have a bearing on the effectiveness of using PLINQ. Therefore, you should not regard these exercises as defining fixed rules that you should always follow. Rather, they illustrate the point that you should carefully measure and assess the likely performance or other benefits of using PLINQ with your own data, in your own environment.

## Canceling a PLINQ query

Unlike with ordinary LINQ queries, you can cancel a PLINQ query. To do this, you specify a CancellationToken object from a CancellationTokenSource and use the WithCancellation extension method of the ParallelQuery.

```
CancellationToken tok = ...;
...
var orderInfoQuery =
    from c in
CustomersInMemory.Customers.AsParallel().WithCancellation(tok)
    join o in OrdersInMemory.Orders.AsParallel()
    on ...
```

You specify WithCancellation only once in a query. Cancellation applies to all sources in the query. If the CancellationTokenSource object used to generate the CancellationToken is canceled, the query stops with an OperationCanceledException exception.

## Synchronizing concurrent access to data

PLINQ is not always the most appropriate technology to use for an application. If you create your own tasks manually, you need to ensure that these tasks coordinate their activities correctly. The .NET Framework class library provides methods with which you can wait for tasks to complete, and you can use these methods to coordinate tasks at a very coarse level. But consider what happens if two tasks attempt to access and modify the same data. If both tasks run at the same time, their overlapping operations might corrupt the data. This situation can lead to bugs that are difficult to correct, primarily because of their unpredictability.

The Task class provides a powerful framework with which you can design and build applications that take advantage of multiple CPU cores to perform tasks in parallel. However, you need to be careful when building solutions that perform concurrent operations, especially if those operations share access to data. You have little control over how parallel operations are scheduled, or even the degree of parallelism that the operating system might provide to an application constructed by using tasks. These decisions are left as run-time considerations and depend on the workload and hardware capabilities of the computer running your application. This level of abstraction was a deliberate design decision on the part of the Microsoft development team, and it removes the need for you to understand the low-level threading and scheduling details when you build applications that require concurrent tasks. But this abstraction comes at a cost. Although it all appears to work magically, you must make some effort to understand how your code runs; otherwise, you can end up with applications that exhibit unpredictable (and erroneous) behavior, as shown in the following example (this sample is available in the ParallelTest project in the folder containing the code for Chapter 24):

```
using System;
using System.Threading;

class Program
{
    private const int NUMELEMENTS = 10;

    static void Main(string[] args)
    {
        SerialTest();
    }

    static void SerialTest()
    {
        int[] data = new int[NUMELEMENTS];
        int j = 0;

        for (int i = 0; i < NUMELEMENTS; i++)
        {
            j = i;
            doAdditionalProcessing();
            data[i] = j;
            doMoreAdditionalProcessing();
        }

        for (int i = 0; i < NUMELEMENTS; i++)
        {
            Console.WriteLine($"Element {i} has value {data[i]}");
        }
    }

    static void doAdditionalProcessing()
    {
        Thread.Sleep(10);
    }

    static void doMoreAdditionalProcessing()
    {
        Thread.Sleep(10);
    }
}
```

The SerialTest method populates an integer array with a set of values (in a rather long-winded way) and then iterates through this list, printing the index of each item in the array together with the value of the corresponding item. The doAdditionalProcessing and doMoreAdditionalProcessing methods simply simulate the performance of long-running operations as part of the processing that might cause the runtime to yield control of the processor. The output of the program method is shown here:

```
Element  0 has value 0
Element  1 has value 1
Element  2 has value 2
Element  3 has value 3
Element  4 has value 4
Element  5 has value 5
Element  6 has value 6
Element  7 has value 7
Element  8 has value 8
Element  9 has value 9
```

Now consider the ParallelTest method, shown next. This method is the same as the SerialTest method except that it uses the Parallel.For construct to populate the data array by running concurrent tasks. The code in the lambda expression run by each task is identical to that in the initial for loop in the SerialTest method.

```
using System.Threading.Tasks;
...
static void ParallelTest()
{
    int[] data = new int[NUMELEMENTS];
    int j = 0;

    Parallel.For (0, NUMELEMENTS, (i) =>
    {
        j = i;
        doAdditionalProcessing();
        data[i] = j;
        doMoreAdditionalProcessing();
    });
    for (int i = 0; i < NUMELEMENTS; i++)
    {
        Console.WriteLine($"Element {i} has value {data[i]}");
    }
}
```

The intention is for the ParallelTest method to perform the same operation as the SerialTest method, except by using concurrent tasks and (with good luck) running a little faster as a result. The problem is that it might not always work as expected. Some sample output generated by the ParallelTest method is shown here:

```
Element  0 has value 1
Element  1 has value 1
Element  2 has value 4
Element  3 has value 8
Element  4 has value 4
Element  5 has value 1
Element  6 has value 4
Element  7 has value 8
Element 8 has value 8
Element 9 has value 9
```

The values assigned to each item in the *data* array are not always the same as the values generated by using the *SerialTest* method. Additionally, further runs of the *ParallelTest* method can produce different sets of results.

If you examine the logic in the *Parallel.For* construct, you should see where the problem lies. The lambda expression contains the following statements:

```
j = i;
doAdditionalProcessing();
data[i] = j;
doMoreAdditionalProcessing();
```

The code looks innocuous enough. It copies the current value of the variable *i* (the index variable identifying which iteration of the loop is running) into the variable *j*, and later on it stores the value of *j* in the element of the data array indexed by *i*. If *i* contains 5, *j* is assigned the value 5, and later on the value of *j* is stored in *data[5]*. But between assigning the value to *j* and then reading it back, the code does more work; it calls the *doAdditionalProcessing* method. If this method takes a long time to execute, the runtime might suspend the thread and schedule another task. A concurrent task running another iteration of the *Parallel.For* construct might run and assign a new value to *j*. Consequently, when the original task resumes, the value of *j* it assigns to *data[5]* is not the value it stored, and the result is data corruption. More troublesome is that sometimes this code might run as expected and produce the correct results, and at other times it might not; it all depends on how busy the computer is and when the various tasks are scheduled. Consequently, these types of bugs can lie dormant during testing and then suddenly manifest in a production environment.

The variable *j* is shared by all the concurrent tasks. If a task stores a value in *j* and later reads it back, it has to ensure that no other task has modified *j* in the meantime. This requires synchronizing access to the variable across all concurrent tasks that can access it. One way in which you can achieve synchronized access is to lock data.

## Locking data

The C# language provides locking semantics through the *lock* keyword, which you can use to guarantee exclusive access to resources. You use the *lock* keyword like this:

```
object myLockObject = new object();
...
lock (myLockObject)
{
    // Code that requires exclusive access to a shared resource
```
