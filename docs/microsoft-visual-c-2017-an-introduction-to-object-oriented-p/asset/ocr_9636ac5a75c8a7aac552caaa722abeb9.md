# Compiling and Executing a C# Program

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using static System.Console;
namespace Hello
{
    class Program
    {
        static void Main(string[] args)
        {
            WriteLine("Hello, world!");
        }
    }
}
```

Figure 1-17 The Hello application editing window after the code has been added

+   1. Save the project by clicking File on the menu bar and clicking Save All, or by clicking the Save All button (which shows two disks) on the toolbar, or by typing Ctrl + Shift + S.
2. To compile the project, click Build on the menu bar, and then click Build Solution. You should receive no error messages, and the words Build succeeded should appear near the lower-left edge of the window.
3. Click Debug on the menu bar, and then Start Without Debugging. Figure 1-18 shows the output; you see Hello, world! followed by the message Press any key to continue. Press any key to close the output screen.

![](bbox=[0.188, 0.688, 0.626, 0.796])

Figure 1-18 Output of the Hello application in Visual Studio