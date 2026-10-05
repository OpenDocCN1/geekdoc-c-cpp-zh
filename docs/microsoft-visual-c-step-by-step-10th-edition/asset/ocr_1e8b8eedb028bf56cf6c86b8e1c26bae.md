```
Microsoft Visual Studio Debug Console
Calculator being created
Unhandled exception. System.DivideByException: Attempted to divide by zero.
at GarbageCollection.Calculator.Divide(Int32 first, Int32 second) in C:\Users\nChapter 14)GarbageCollection - Complete(GarbageCollection)Calculator.cs:line 26
at GarbageCollection.Program.dword() in C:\student\Documents\Microsoft
 - Complete(GarbageCollection)Program.cs:line 11
at at GarbageCollection.Program.Main(String[] args) in C:\student\Documents
GbageCollection - Complete(GarbageCollection)Program.cs:line 21
Calculator being disposed
C:\Users\student\Documents\Microsoft\VCSB\Chapter 14\GarbageCollection -
6.0\GarbageCollection.exe (process 1512) exited with code -1873741676.
Press any key to close this window . . .
```

6. In the console window, press Enter and return to Visual Studio 2022.

# Handling asynchronous disposal

The Dispose method of the Disposable interface is synchronous. If resource disposal takes a significant amount of time, the thread calling the Dispose method will be blocked until disposal is complete. If this is the thread that handles the user interface, then your application can become unresponsive and frustrating to use. To combat this, you can implement asynchronous disposal.

To indicate that an object should be disposed asynchronously, you use the await operator with the using statement that creates the resource, like this:

Click here to view code image

```
await using (BigDisposable myObject = new BigDisposable())
{
  ...
}
```

While the object is being disposed, at the end of the using block, the current thread will be freed to perform other work. When the disposal is complete, the thread can switch back to the first statement after the closing brace.