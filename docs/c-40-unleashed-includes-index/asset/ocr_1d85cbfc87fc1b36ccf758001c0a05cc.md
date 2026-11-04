In the command prompt instance that shows up, enter exit 5 to exit the prompt with exit code 5. Our application should observe this through the ExitCode property. In some cases, you can't afford to block the parent process while waiting for the child process to terminate. Instead, the use of an event seems more appealing. This too is possible, as shown here:

```
var cmd = new Process
{
    EnableRaisingEvents = true,
    StartInfo = new ProcessStartInfo("cmd.exe")
};
cmd.Exited += (o, e) => Console.WriteLine(cmd.ExitCode);
cmd.Start();

while (true)
{
    Thread.Sleep(500);
    Console.Write(".");
}
```

Here we're using the ProcessStartInfo object in conjunction with the Process class's constructor. This is done to avoid a race condition that would exist if we were to use Process.Start, in which case it's possible the process exits before we get a chance to attach an event handler to the Exited event. Running the preceding code prints dots to the screen, even while the child process is running. If the child process terminates, the event handler code (here specified using a lambda expression) is executed. Although printing dots is not the most appealing application, it clearly shows the asynchronous nature that's realized through the use of an event.

ProcessStartInfo has plenty of other rich capabilities, such as the capability to control how the spawn process's window looks or even to hide it to avoid distracting pop-ups seen by the user. The following example shows a useful trick to redirect a process's “standard output” to our process (for example, to log what another process is doing in a UI of ours). Similarly, we could interact with the process's standard input or error output:

```
var tlist = new Process
{
    StartInfo = new ProcessStartInfo("tasklist.exe")
    {
        RedirectStandardOutput = true,
        UseShellExecute = false
    }
};
tlist.Start();
Console.WriteLine(tlist.StandardOutput.ReadToEnd());
```