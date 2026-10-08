# LISTING 10-19: Program.cs

```
using System;

namespace MefGreetings
{
    class Program
    {
        static void Main(string[] args)
        {
            var greetings = new SimpleGreeting();
            Console.WriteLine(greetings.SayHello());
        }
    }
}
```

Code file [Program.cs] available for download at Wrox.com

Run the application, and it does exactly what you expect — it displays the “Hello from Visual Studio 2010” message. Despite the refactoring of the application, the SimpleGreeting and Program are still tightly coupled. Although, the greeting text is decoupled from the console class through the IGreeting interface, the SimpleGreeting class is directly instantiated. Now, let’s turn your application to a “MEFish” one!

# Getting MEF into the Game

To utilize MEF, add a reference to the System.ComponentModel.Composition assembly, because MEF types and attributes are declared here. You are going to turn this application to a dynamically composed one in a few steps.

Decorate the SimpleGreeting with the Export attribute. This attribute will signify that SimpleGreeting is a composable part that has a service offered to the external world. The attribute has a typeof(IGreeting) parameter, which is the identifier of the contract SimpleGreeting is about to export. Listing 10-20 shows SimpleGreetings.cs after this change.

# LISTING 10-20: SimpleGreeting with the Export Attribute

```
using System.ComponentModel.Composition;

namespace MefGreetings
{
    [Export(typeof(IGreeting))]
    class SimpleGreeting : IGreeting
    {
        public string SayHello()
        {
            return "Hello from Visual Studio 2010";
        }
    }
}
```

Code file [SimpleGreetings.cs] available for download at Wrox.com