like this:

Click here to view code image

```
Task.WaitAll(task, task2); // Wait for both task and task2 to complete
Task.WaitAny(task, task2); // Wait for either task or task2 to complete
```

# Using the Task class to implement parallelism

In the next exercise, you will use the Task class to parallelize processor-intensive code in an application, and you will see how this parallelization reduces the time taken for the application to run by spreading the computations across multiple processor cores.

The application, called GraphDemo, consists of a page that uses an Image control to display a graph. The application plots the points for the graph by performing a complex calculation.

# Note

The exercises in this chapter are intended to be run on a computer with a multicore processor. If you have only a single-core CPU, you will not observe the same effects. Also, you should not start any additional programs or services between exercises because these might affect the results that you see.

# Examine and run the GraphDemo single-threaded application

+   1. Start Microsoft Visual Studio 2015 if it is not already running.
+   2. Open the GraphDemo solution, which is located in the \Microsoft Press\VCSBS\Chapter 23\GraphDemo folder in your Documents folder. This is a Universal Windows Platform app.
+   3. In Solution Explorer, in the GraphDemo project, double-click the file MainPage.xaml to display the form in the Design View window.

Apart from the Grid control defining the layout, the form contains the following important controls:

+   - An Image control called graphImage. This image control displays the graph rendered by the application.
+   - A Button control called plotButton. The user clicks this button to generate the data for the graph and display it in the graphImage control.