# There's more...

After the user gives the input, control is returned to the application. Only now can the application continue the execution. In order to overcome such an issue, we can create concurrent threads that will handle the user input. In this way, the application does not stall and is responsive all the time. After a thread handles its task, it can signal that a user has performed the requested operation to the application.

Every time we have an operation that needs to be executed separately from the main execution flow, we have to think about a separate thread. The simplest example is when we have some calculations, and we want to have a progress bar where the calculation progress will be shown. If the same thread probably wouldn't work. This occurs because, if both work and a UI update are performed from a single thread, such threads cannot interact with OS painting adequately; so almost always, the UI thread separate from the working threads.

Let's review the following example. Assume that we have created a function that we will calculate something, for example, sines or cosines of some angle, and we want to display progress in every step of the calculation:

```
void calculateSomething(int iCount)
{
    int iCounter = 0;
    while (iCounter++ < iCount)
    {
        //make calculation
        //update progress bar
    }
}
```

![](bbox=[0.239, 0.147, 0.76, 0.366])