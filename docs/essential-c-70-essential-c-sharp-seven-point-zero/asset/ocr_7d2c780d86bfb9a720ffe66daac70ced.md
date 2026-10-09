```
if(taskCanceledException != null){
			Console.WriteLine($@"Canceled: {
				taskCanceledException.Message }");
		}
		else
		{
				/// ...
		}
		}
	else
	{
		task.Wait();
		Console.ForegroundColor = ConsoleColor.Green;
		Console.Write("Completed successfully");
	}
	Console.ForegroundColor = originalColor;
}
```

**OUTPUT 19.11**
Canceled: A task was canceled.

As with a parallel loop or task, canceling a PLINQ query requires a CancellationToken, which is available from a CancellationTokenSource. However, rather than overloading every PLINQ query to support the cancellation token, the ParallelQuery<T> object returned by IEnumerable's AsParallel( ) method includes a WithCancellation( ) extension method that simply takes a CancellationToken. As a result, calling Cancel( ) on the CancellationTokenSource object will request the parallel query to cancel—because it checks the IsCancellationRequested property on the CancellationToken.

As mentioned, canceling a PLINQ query will throw an exception in place of returning the complete result. One common technique for dealing with a possibly canceled PLINQ query is to wrap the query in a try block and catch the OperationCanceledException. A second common technique, used in Listing 19.35, is to pass the CancellationToken both to ParallelEncrypt( ) and as a second parameter on Run( ). This will cause task.Wait( ) to throw an AggregateException whose InnerException property will be set to a TaskCanceledException. The aggregating exception can then be caught, just as you would catch any other exception from a parallel operation.