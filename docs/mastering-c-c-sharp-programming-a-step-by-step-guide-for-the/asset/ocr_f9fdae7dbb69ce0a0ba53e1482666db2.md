We’ll start by creating a method. When you open a new project you will see code that looks like:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
using System.Net;

namespace MethodsLesson
{
    public class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Remember our very first code – the Hello World! program. We used the template code for that and it already has a method defined in it – the Main method. Looking at the code you can see that this method is in a class named Program – we’ll start discussing classes in the next section. As you can see, you’ve already had a little practice using methods without realizing it.

In a nutshell, every method belongs to a class. When you create a method you will add it to a class – we’re going to add to the Program class, the same place as the Main method is found.