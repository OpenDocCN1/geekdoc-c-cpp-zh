allow for canceling before the process ever starts, as well as an attempt to close the application's main window (if there is one). A more aggressive approach would be to call Process.Kill(), but this method could potentially cause problems for the program that is executing.

Notice that we don't register for the cancellation event until after the process is started. This avoids any race conditions that might occur if cancellation is triggered before the process actually begins.

One last feature to consider supporting is a progress update. Listing 19.20 is the full version of RunProcessAsync() with just such an update.

# LISTING 19.20: Implementing a Custom Asynchronous Method with Progress Support

```
```
using System;
using System.Diagnostics;
using System.Threading;
using System.Threading.Tasks;
class Program
{
    static public Task<Process> RunProcessAsync(
        string fileName,
        string arguments = null,
        CancellationToken cancellationToken =
            default(CancellationToken),
        IProgress<ProcessProgressEventArgs> progress =
            null,
        object objectState = null)
    {
        TaskCompletionSource<Process> taskCS =
            new TaskCompletionSource<Process>();

        Process process = new Process()
        {
            StartInfo = new ProcessStartInfo(fileName)
            {
                UseShellExecute = false,
                Arguments = arguments,
                RedirectStandardOutput =
                    progress != null
            },
            EnableRaisingEvents = true
        };

        process.Exited += (sender, localEventArgs) =>
        {
            taskCS.SetResult(process);
        };
```
```