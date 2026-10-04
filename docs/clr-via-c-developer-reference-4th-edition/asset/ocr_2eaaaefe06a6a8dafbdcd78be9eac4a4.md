The following code is a rewrite of the WinRTAsyncIntro method previously mentioned. However, this version is leveraging some methods supplied with the .NET Framework, which turn the WinRT asynchronous programming model into the more convenient C# programming model.

using System; // Required for extension methods in WindowsRuntimeExtensions

```
public async void WinRTAsyncIntro()
    try {
        StorageFile file = await NewFolders.MusicLibrary.GetFileAsync("Song.mp3");
        /* Completed... */
    }
    catch (OperationCanceledException) { /* Canceled... */ }
    catch (OtherException ex) { /* Error... */ }
```

What's happening here is that the use of C#'s await operator allows the compiler to look for a GetAwait method on the IAsyncOperation<StorageFile> interface returned from the GetFileAsync method. This interface does not provide a GetAwait method, and so, the compiler looks for an extension method. Fortunately, the .NET framework has provided in System.Runtime.dll bunch of extension methods when you have one of WinRT IAsyncXXX interfaces.

```
namespace System {
    public static class WindowsRuntimeExtensions {
        public static TaskAwait GetAwaiter(this IAsyncAction source);
        public static TaskAwait GetAwaiter<TProgress>(this IAsyncActionWithProgress<TProgress> source);
        public static TaskAwait<TResult> GetAwaiter<TResult>(this IAsyncOperation<TResult> source);
        public static TaskAwait<TResult> GetAwaiter<TResult>(this IAsyncOperationWithProgress<TResult, TProgress> source);
    }
```

Internally, all methods construct a TaskCompletionSource and the IAsyncXXX object to invoke a callback that sets the TaskCompletionSource's final state when the asynchronous operation completes. The TaskAwaiter returned from these extension methods ultimately returns C# await. When the asynchronous operation completes, the TaskAwaiter ensures that the code continues executing via the SynchronizationContext (discussed in Chapter 28) that is associated with the original thread. Then, the thread executes generated code, which queries the TaskCompletionSource's Result property, which returns the result (a StorageFile in my example), throws an OperationCanceledException in case of cancellation, or throws other exception if a failure occurred. For an example of how these methods work internally, see the code at the end of this section.