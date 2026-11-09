![](bbox=[0.15, 0.07, 0.83, 0.3])

In the .NET Framework, we use the types in the System.Threading.Tasks namespace to simplify performing asynchronous operations. I explain these types and how to use them to perform compute operations in Chapter 27, “Compute-Bound Asynchronous Operations” and how to use them to perform I/O operations in Chapter 28, “I/O-Bound Asynchronous Operations.” In addition, C# offers the async and await keywords which allow you to perform asynchronous operations using a sequential programming model thereby simplifying your code substantially.

The following code is a rewrite of the WinRTAsyncIntro method previously mentioned. However, this version is leveraging some extension methods supplied with the .NET Framework, which turn the WinRT asynchronous programming model into the more convenient C# programming model.

```
```csharp
using System;        // Required for extension methods in WindowsRuntimeSystemExtensions
.
.
.
public async void WinRTAsyncIntro() {
    try {
        StorageFile file = await KnownFolders.MusicLibrary.GetFileAsync("Song.mp3");
        /* Completed... */
    }
    catch (OperationCanceledException) { /* Canceled... */ }
    catch (SomeOtherException ex) { /* Error... */ }
}
```
```

What's happening here is that the use of C#'s await operator causes the compiler to look for a GetAwaiter method on the IAsyncOperation<StorageFile> interface returned from the GetFileAsync method. This interface doesn't provide a GetAwaiter method, and so, the compiler looks for an extension method. Fortunately, the .NET Framework team has provided in System.Runtime.WindowsRuntime.dll a bunch of extension methods callable when you have one of WinRT's IAsyncXxx interfaces:

```
```csharp
namespace System {
```
```