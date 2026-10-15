```
namespace Class1
{
    class Class1
    {
        public void Greeting(string name)
        {
            System.Console.WriteLine("Class One says Hi : " + name);
        }
    }
}
```

2. Save the file as Class1.cs. Similarly, create a new file called Class2.cs and add the code in the file as shown in Listing 33.12:

# Listing 33.12: Showing the Code for Class2.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Class2
{
    class Class2
    {
        public void Greeting(string name)
        {
            System.Console.WriteLine("Class Two says Hi : " + name);
        }
    }
}
```

The two classes that we have created, each having a simple function called Greeting, displays a message on the console window.

3. Create a third file called SimpleClient.cs, as shown in Listing 33.13:

# Listing 33.13: Showing the Code for SimpleClient.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace SimpleClient
{
    class SimpleClient
    {
        public static void Main()
        {
            Class1.Class1 c1 = new Class1.Class1();
            c1.Greeting("SimpleClient");
            Class2.Class2 c2 = new Class2.Class2();
            c2.Greeting("SimpleClient");
        }
    }
}
```

The SimpleClient class has the Main function that we need to execute our assembly. Now we need to compile the three files.

4. Open the .NET console window with Start→All Programs→Microsoft Visual Studio 2010→Visual Studio Tools→Visual Studio Command Prompt (2010). Move to the folder to the location where you have saved these class files and type the following command:

csc /t:module Class1.cs

The preceding command creates a file called Class1.netmodule, which is a compiled version of the Class1.cs class. There is no way of creating netmodule files directly through .NET IDE. Therefore, we have to use csc.exe, which is a command-line compiler for Visual C# applications to compile the files.

If you open any of the .netmodule files in Ildasm.exe, you would see that there is no .assembly attribute in their manifest (the .assembly extern attributes are different from .assembly attributes; they indicate the