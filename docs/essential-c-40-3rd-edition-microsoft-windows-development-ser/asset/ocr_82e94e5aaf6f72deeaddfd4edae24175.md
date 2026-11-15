```
else
{
    if (commandLine.Priority !=
        ProcessPriorityClass.Normal)
    {
        // Change thread priority
    }
    // ...
}

private static void DisplayHelp()
{
    // Display the command-line help.
    Console.WriteLine(
        "Thankyou for contacting the help text");
}
```

```
using System;
using System.Diagnostics;

public partial class Program
{
    private class CommandLineInfo
    {
        [CommandLineSwitchAlias("?")]
        public bool Help
        {
            get { return _Help; }
            set { _Help = value; }
        }

        private bool _Help;

        [CommandLineSwitchRequired]
        [CommandLineSwitchAlias("FileName")]
        public string Out
        {
            get { return _Out; }
            set { _Out = value; }
        }

        private string _Out;

        public ProcessPriorityClass Priority
        {
            get { return _Priority; }
            set { _Priority = value; }
        }
    }
}
```