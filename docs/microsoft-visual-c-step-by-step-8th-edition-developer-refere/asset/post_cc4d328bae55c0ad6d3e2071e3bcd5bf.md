
type parameter, TResult, specifies the type of the result.

You create and start a Task<TResult> object in a similar way as for an ordinary Task. The primary difference is that the code you execute should return a value. For example, the method named calculateValue shown in the code example that follows generates an integer result. To invoke this method by using a task, you create and run a Task<int> object. You obtain the value returned by the method by querying the Result property of the Task<int> object. If the task has not finished running the method and the result is not yet available, the Result property blocks the caller. This means that you don’t have to perform any synchronization yourself, and you know that when the Result property returns a value, the task has completed its work.

Click here to view code image

```
Task<int> calculateValueTask = Task.Run(() => calculateValue(...));
...
int calculatedData = calculateValueTask.Result; // Block until
calculateValueTask completes
...
private int calculateValue(...)
{
    int someValue;
    // Perform calculation and populate someValue
    ...
    return someValue;
}
```

The generic Task<TResult> type is also the basis of the mechanism for defining asynchronous methods that return values. In previous examples, you saw that you implement asynchronous void methods by returning a Task. If an asynchronous method actually generates a result, it should return a Task<TResult>, as shown in the following example, which creates an asynchronous version of the calculateValue method:

Click here to view code image

```
private async Task<int> calculateValueAsync(...)
{
    // Invoke calculateValue using a Task
    Task<int> generateResultTask = Task.Run(() =>
calculateValue(...));
    await generateResultTask;
    return generateResultTask.Result;
}
```

This method looks slightly confusing inasmuch as the return type is specified as Task<int>, but the return statement actually returns an int. Remember that when you define an async method, the compiler performs some refactoring of your code, and it essentially returns a reference to Task that runs the continuation for the statement return generateResultTask.Result;. The type of the expression

returned by this continuation is *int*, so the return type of the method is *Task<int>*.

To invoke an asynchronous method that returns a value, use the *await* operator, like this:

Click here to view code image

```
int result = await calculateValueAsync(...);
```

The *await* operator extracts the value from the *Task* returned by the *calculateValueAsync* method, and in this case assigns it to the *result* variable.

## Asynchronous method gotchas

The *async* and *await* operators have been known to cause confusion amongst programmers. It is important to understand that:

- Marking a method as *async* does not mean that it runs asynchronously. It means that the method can contain statements that may run asynchronously.
- The *await* operator indicates that a method should be run by a separate task, and the calling code is suspended until the method call completes. The thread used by the calling code is released and can be reused. This is important if the thread is the user interface thread, as it enables the user interface to remain responsive.
- The *await* operator is not the same as using the *Wait* method of a task. The *Wait* method always blocks the current thread and does not allow it to be reused until the task completes.
- By default, the code that resumes execution after an *await* operator attempts to obtain the original thread that was used to invoke the asynchronous method call. If this thread is busy, the code will be blocked. You can use the *ConfigureAwait(false)* method to specify that the code can be resumed on any available thread and reduce the chances of blocking. This is especially useful for web applications and services that may need to handle many thousands of concurrent requests.
- You shouldn’t use *ConfigureAwait(false)* if the code that runs after an *await* operator must execute on the original thread. In the example discussed earlier, adding *ConfigureAwait(false)* to each awaited operation will result in the likelihood that the continuations the compiler generates will run on separate threads. This includes the continuation that attempts to set the *Text* property for *message*, causing the exception “The application called an interface that was marshaled for a different thread” again.

Click here to view code image

```
private async void slowMethod()
{
    await doFirstLongRunningOperation().ConfigureAwait(false);
    await doSecondLongRunningOperation().ConfigureAwait(false);
    await doThirdLongRunningOperation().ConfigureAwait(false);
    message.Text = "Processing Complete";
}
```

Careless use of asynchronous methods that return results and that run on the user interface thread can generate deadlocks, causing the application to freeze. Consider the following example:

Click here to view code image

```
private async void myMethod()
{
    var data = generateResult();
    ...
    message.Text = $"result: {data.Result}";
}

private async Task<string> generateResult()
{
    string result;
    ...
    result = ...
    return result;
}
```

In this code, the generateResult method returns a string value. However, the myMethod method does not actually start the task that runs the generateResult method until it attempts to access the data.Result property; data is a reference to the task, and if the Result property is not available because the task has not been run, then accessing this property will block the current thread until the generateResult method completes. Furthermore, the task used to run the generateResult method attempts to resume the thread on which it was invoked when the method completes (the user interface thread), but this thread is now blocked. The result is that the myMethod method cannot finish until the generateResult method completes, and the generateResult method cannot finish until the myMethod method completes.

The solution to this problem is to await the task that runs the generateResult method. You can do this as follows:

Click here to view code image

```
private async void myMethod()
{
    var data = generateResult();
    ...
    message.Text = $"result: {await data}";
}
```

## Asynchronous methods and the Windows Runtime APIs

The designers of Windows 8 and later versions wanted to ensure that applications were as responsive as possible, so they made the decision when they implemented WinRT that any operation that might take more than 50 milliseconds to perform should be available only through an asynchronous API. You might have noticed one or two instances of this approach already in this book. For example, to display a message to a user, you can use a MessageDialog object. However, when you display this message, you must use the ShowAsync method, like this:

Click here to view code image

```
using Windows.UI.Popups;
...
MessageDialog dlg = new MessageDialog("Message to user");
await dlg.ShowAsync();
```

The MessageDialog object displays the message and waits for the user to click the Close button that appears as part of this dialog box. Any form of user interaction might take an indeterminate length of time (the user might have gone for lunch before clicking Close), and it is often important not to block the application or prevent it from performing other operations (such as responding to events) while the dialog box is displayed. The MessageDialog class does not provide a synchronous version of the ShowAsync method, but if you need to display a dialog box synchronously, you can simply call dlg.ShowAsync() without the await operator.

Another common example of asynchronous processing concerns the FileOpenPicker class, which you saw in Chapter 5, “Using compound assignment and iteration statements.” The FileOpenPicker class displays a list of files from which the user can select. As with the MessageDialog class, the user might take a considerable time browsing and selecting files, so this operation should not block the application. The following example shows how to use the FileOpenPicker class to display the files in the user’s Documents folder and wait while the user selects a single file from this list:

Click here to view code image

```
using Windows.Storage;
using Windows.Storage.Pickers;
...
FileOpenPicker fp = new FileOpenPicker();
fp.SuggestedStartLocation = PickerLocationId.DocumentsLibrary;
fp.ViewMode = PickerViewMode.List;
fp.FileTypeFilter.Add("*");
StorageFile file = await fp.PickSingleFileAsync();
```

The key statement is the line that calls the PickSingleFileAsync method. This is the method that displays the list of files and allows the user to navigate around the file system and select a file. (The FileOpenPicker class also provides the PickMultipleFilesAsync method by which a user can select more than one file.) The value returned by this method is Task<StorageFile>, and the await operator extracts the StorageFile object from this result. The StorageFile class provides
