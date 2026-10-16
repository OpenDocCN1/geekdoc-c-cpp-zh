System.Net.Http

MyApplicatonEvents

# Namespaces

System

System.Collections.Generic

System.Diagnostics.Tracing

System.Net.Http

System.Threading.Tasks

static System.Console

The ParallelRequestSample method invokes the RequestStart and RequestStop methods to start and stop the activity. Between these calls, a parallel loop is created using Parallel.For. The Parallel class uses multiple tasks to run concurrently by calling the delegate of the third parameter. This parameter is implemented as a lambda expression to invoke the ProcessTaskAsync method (code file ClientApp/Program.cs):

```
private static void ParallelRequestSample()
{
    SampleEventSource.Log.RequestStart();
    Parallel.For(0, 20, x =>
    {
        ProcessTaskAsync(x).Wait();
    });
    SampleEventSource.Log.RequestStop();
    WriteLine("Activity complete");
}
```

> NOTE The Parallel class is explained in detail in Chapter 21, "Tasks and Parallel Programming."

The method ProcessTaskAsync writes traces using ProcessingStart and ProcessingStop. Here, an activity is started within another activity. As you can see from the output analyzing the logs, activities can be hierarchical (code file ClientApp/Program.cs):

```
private static async Task ProcessTaskAsync(int x)
{
    SampleEventSource.Log.ProcessingStart(x);
    var r = new Random();
    await Task.Delay(r.Next(500));

    using (var client = new HttpClient())
    {
        var response = await client.GetAsync("http://www.bing.com");
    }
    SampleEventSource.Log.ProcessingStop(x);
}
```

Previously, you have used the PerfView tool to open an ETL log file. PerfView can also analyze running applications. You can run PerfView