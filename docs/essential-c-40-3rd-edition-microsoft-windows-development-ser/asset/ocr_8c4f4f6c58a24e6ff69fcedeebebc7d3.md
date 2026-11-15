```
```
DisplayHelp();
}
else
{
    if (commandLine.Priority !=
        ProcessPriorityClass.Normal)
    {
        // Change thread priority
    }
}
// ...
}

private static void DisplayHelp()
{
    // Display the command-line help.
}
```
```

```
```
using System;
using System.Diagnostics;

public partial class Program
{
    private class CommandLineInfo
    {
        public bool Help { get; set; }

        public string Out { get; set; }

        public ProcessPriorityClass Priority
        {
            get { return _Priority; }
            set { _Priority = value; }
        }

        private ProcessPriorityClass _Priority =
            ProcessPriorityClass.Normal;
    }
}
```
```

```
```
using System;
using System.Diagnostics;
using System.Reflection;

public class CommandLineHandler
{
```
```