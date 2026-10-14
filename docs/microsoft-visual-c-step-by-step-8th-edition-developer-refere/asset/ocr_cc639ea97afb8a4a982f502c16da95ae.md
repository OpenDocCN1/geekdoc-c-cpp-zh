```
Parallel.Invoke(
    doWork,
    doMoreWork,
    doYetMoreWork
);
```

You should bear in mind that the Parallel class determines the actual degree of parallelism appropriate for the environment and workload of the computer. For example, if you use Parallel.For to implement a loop that performs 1,000 iterations, the Parallel class does not necessarily create 1,000 concurrent tasks (unless you have an exceptionally powerful processor with 1,000 cores). Instead, the Parallel class creates what it considers to be the optimal number of tasks that balances the available resources against the requirement to keep the processors occupied. A single task might perform multiple iterations, and the tasks coordinate with each other to determine which iterations each task will perform. An important consequence of this is that you cannot guarantee the order in which the iterations are executed, so you must ensure that there are no dependencies between iterations; otherwise, you might encounter unexpected results, as you will see later in this chapter.

In the next exercise, you will return to the original version of the GraphDemo application and use the Parallel class to perform operations concurrently.

# Use the Parallel class to parallelize operations in the GraphDemo application

+   1. Using Visual Studio 2015, open the GraphDemo solution, which is located in the \Microsoft Press\VCSBS\Chapter 23\Parallel GraphDemo folder in your Documents folder.
+      This is a copy of the original GraphDemo application. It does not use tasks yet.
+   2. In Solution Explorer, in the GraphDemo project, expand the MainPage.xaml node, and then double-click MainPage.xaml.cs to display the code for the form in the Code and Text Editor window.
+   3. Add the following using directive to the list at the top of the file:
+      using System.Threading.Tasks;
+   4. Locate the generateGraphData method. It looks like this:

Click here to view code image

```
private void generateGraphData(byte[] data)
{
    int a = pixelWidth / 2;
    int b = a * a;
    int c = pixelHeight / 2;

    for (int x = 0; x < a; x++)
```