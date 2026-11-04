5 Click the OK button. The AliasClass application is created.

6 Add the highlighted code shown in Listing 2.1 to the Program.cs file:

# Listing 2.1: Using the Scope Resolution Operator with Global Identifier

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace AliasClass
{
    class AliasClass
    {
        public class System
        {
            public void Print()
            {
                global::System.Console.WriteLine("This is an example of :: operator");
            }

            // Define a constant 'Console'
            const string Console = "Hello";
            const string str1 = "World";
            static void Main(string[] args)
            {
                // Error accesses TestApp.Console
                System sys = new System();
                sys.Print();
                global::System.Console.WriteLine(Console);
                global::System.Console.WriteLine(str1);
                global::System.Console.ReadLine();
            }
        }
    }
}
```
```

In Listing 2.1, the :: operator is used with the global identifier. This ensures that the types and namespaces are not affected by the inclusion of the new types and members.

7 Select Build→Build Solution to build the solution, as shown in Fig.C+2.2:

![](bbox=[0.28, 0.62, 0.68, 0.68])

Fig.C+2.2

8 Select Debug→Start Debugging. The output appears, as shown in Fig.C+2.3:

![](bbox=[0.28, 0.73, 0.7, 0.81])

Fig.C+2.3