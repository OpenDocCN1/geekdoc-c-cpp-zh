a task threw an OperationCanceledException without being treated as an exception?

This time, the answer lies in the task itself. For a task to recognize that an OperationCanceledException exception is the result of canceling the task in a controlled manner and not just an exception caused by other circumstances, it must know that the operation has actually been canceled. It can do this only if it passed this token as a parameter to the method run by the task, but the task doesn't actually check any of the parameters. Instead, you specify the cancellation token when you create and run the task. The code that follows shows an example based on the GraphDemo application. Notice how the token parameter is passed to the generateGraphData method (before) but also as a parameter to the Run method.

Click here to view code image

```
tokenSource = new CancellationTokenSource();
CancellationToken token = tokenSource.Token;

Task first = Task.Run(() => generateGraphData(data, 0, pixelWidth / 4, token), token);
```

Now, when the method run by the task throws an OperationCanceledException exception, the infrastructure beneath the task examines the CancellationToken. If it indicates that the task has been canceled, the infrastructure sets the status of the task to Canceled. If you're using the await operator to wait for the tasks to complete, you also need to be prepared to catch and handle the OperationCanceledException exception. This is what you'll do in the next execute.

# To acknowledge cancellation and handle the OperationCanceledException exception

+   1. In Visual Studio, return to the Code and Editor window displaying the MainPage.xamlcs file. Then, in the plotButton_Click method, modify the statements that create and run the tasks and specify the CancellationToken object as the second parameter to the Run method (and also as a parameter to the generateGraphData method), as shown in the following code:...

Click here to view code image