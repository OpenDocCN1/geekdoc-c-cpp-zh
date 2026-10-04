I know that some readers like to understand how these AsTask methods internally convert a .WinRT Framework Task that can ultimately be awaited. The following code shows the most complicated AsTask method is effectively implemented. The simpler the overload, the simpler than this.

```
public static Task<TResult> AsTask<TResult, TProgress>(n    this IAsyncOperation<TResult, TProgress> withProgress, TProgress asyncOp,
    CancellationToken ct = default(CancellationToken),
    IProgress<T> progress = null) {
    // When CancellationTokenSource is cancelled, cancel the async operation
    ct.Register(() => asyncOp.Cancel());

    // When the async operation reports, it reports it to the progress callback
    asyncOp.Progress = (asyncInfo, p) => progress.Report(p);

    // This TaskCompletionSource monitors the async operation's completion
    var tcs = new TaskCompletionSource<TResult>();

    // When the async operation completes, notify the TaskCompletionSource
    // Code awaiting the TaskCompletionSource regains control when this happens
    asyncOp.Completed = (asyncOp2, asyncStatus) => {
        switch (asyncStatus) {
            case AsyncStatus.Completed: tcs.SetResult(asyncOp2.GetResult()); break;
            case AsyncStatus.C: tcs.SetCanceled(); break;
            case AsyncStatus.Error: tcs.SetException(asyncOp2.ErrorCode); break;
        }
    }
```

// calling await this returned Task, it calls GetAwaiter, which nwraps a SynchronizationContext around the Task ensuring that completionncurs on the SynchronizationContext object's contextnreturn tcs.Task.

# Interoperating Between WinRT classes and .NET Streams

There are many classes that operate on System.IO.Stream types, such as serialization and LINQ to XML. To use a WinRT object that implements WinRT's IStorageFile or IStorageFolder with a . framework class that requires a Stream-derived type, we use extension methods defined in System.Windows.StorageExtensions classes.

```
namespace System.IO {
    // Defined in System.Windows.Runtime.dll
    public static class WindowsRuntimeStorageExtensions {
        public static Task<Stream> OpenStreamForReadAsync(this IStorageFile file);
        public static Task<Stream> OpenStreamForWriteAsync(this IStorageFile file);

        public static Task<Stream> OpenStreamForReadAsync(this IStorageFolder rootDirectory,
            String relativePath);
        public static Task<Stream> OpenStreamForWriteAsync(this IStorageFolder rootDirectory,
            String relativePath, CreationCollisionOption creationCollisionOption);
    }
}
```