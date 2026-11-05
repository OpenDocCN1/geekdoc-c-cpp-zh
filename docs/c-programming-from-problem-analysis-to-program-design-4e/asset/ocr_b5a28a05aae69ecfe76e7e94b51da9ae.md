```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ProgrammingMessage
{
class Program
{
static void Main(string[] args)
{
}
}
}
```

Can delete these using statements

Change the name

Can replace with static void Main()

# FIGURE 1-24 Recommended deletions

The only lines that you had to type were found in the Main() body.

```
Console.WriteLine("Programming can be");
Console.WriteLine("FUN!");
Console.ReadKey();
```

The final program listing looks like this:

```
/* Programmer: [supply your name]
Date: [supply the current date]
Purpose: This class can be used to send messages
to the output screen.
*/
using System;
namespace ProgrammingMessage
{
class ProgrammingMessage
{
static void Main()
{
Console.WriteLine("Programming can be");
Console.WriteLine("FUN!");
Console.ReadKey();
}
}
}
```

At the beginning of your program, identify the author of the code, and as a minimum specify the purpose of the project. Note that the statements inside the Main() method are executed in sequential order. The ReadKey() method is executed after the two WriteLine() methods. ReadKey() is used in a program to keep the