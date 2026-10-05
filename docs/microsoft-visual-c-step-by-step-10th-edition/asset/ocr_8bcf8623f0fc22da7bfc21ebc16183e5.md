Click here to view code image

```
private Task doFirstLongRunningOperation()
{
    Task t = Task.Run(() => { /* original code for this method
goes here */ });
    return t;
}
```

It’s also worth considering whether there are opportunities to break the work done by the doFirstLongRunningOperation method into a series of parallel operations. If so, you can divide the work into a set of Task operations, as described in Chapter 23. However, which of these Task objects should you return as the result of the method?

Click here to view code image

```
private Task doFirstLongRunningOperation()
{
    Task first = Task.Run(() => { /* code for first operation *//);

    Task second = Task.Run(() => { /* code for second operation *//);

    return ...; // Do you return first or second?
}
```

If the method returns first, the await operator in the slowMethod will wait only for Task operation to complete and not for the second one. Similar logic applies if the method returns second. The solution is to define the doFirstLongRunningOperation method with async and await each of the Task operations, as shown here:

Click here to view code image

```
private async Task doFirstLongRunningOperation()
{
    Task first = Task.Run(() => { /* code for first operation *//);

    Task second = Task.Run(() => { /* code for second operation *//);

    await first;
    await second;
}
```