# Performance Counter Builder

The sample application PerformanceCounterDemo is a simple Windows application with just two buttons to demonstrate writing performance counts. With the handler of one button, a performance counter category is registered; with the handler of the other button, a performance counter value is written. In a similar way to the sample application, you can add performance counters to a Windows Service (see Chapter 25, "Windows Services"), to a network application (see Chapter 24, "Networking"), or to any other application from that you would like to receive live counts.

Using Visual Studio, you can create a new performance counter category by selecting the performance counters in the Server Explorer and by selecting the menu entry Create New Category on the context menu. This launches the Performance Counter Builder (see Figure 19-7).

![](bbox=[0.48, 0.13, 0.9, 0.57])

FIGURE 19-7

> To create a performance counter category with Visual Studio, Visual Studio must be started in elevated mode.

Set the name of the performance counter category to Wrox Performance Counters. The following table shows all performance counters of the quote service.

| NAME | DESCRIPTION | TYPE |
|---|---|---|
| # of button clicks | Total # of button clicks | NumberOfItems32 |
| # of button clicks/sec | # of button clicks in one second | RateOfCountsPerSecond32 |
| # of mouse move events | Total # of mouse move events | NumberOfItems32 |
| # of mouse move events/sec | # of mouse move events in one second | RateOfCountsPerSecond32 |

The Performance Counter Builder writes the configuration to the performance database. This can also be done dynamically by using the Create() method of the PerformanceCounterCategory class in the System.Diagnostics namespace. An installer for other systems can be added later using Visual Studio.

The following code snippet shows how a performance category can be added programmatically. With the tool from Visual Studio, you can only create a global performance category that doesn't have different values for different processes of running applications. Creating a performance category programmatically allows you to monitor performance counts from different applications, which is also done here.

First, a const for the category name is defined, as well as SortedList<TKey, TValue>, which contains the names of the performance counts:

```
private const string performanceCounterCategoryName = "Wrox Performance Counters";
private SortedList<string, Tuple<string, string>> perfCountNames;
```

code snippet PerformanceCounterDemo/MainWindow.xaml.cs