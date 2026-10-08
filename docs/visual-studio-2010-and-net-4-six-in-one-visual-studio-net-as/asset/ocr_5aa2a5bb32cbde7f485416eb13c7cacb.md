# Creating a Simple Item Template

You can make the BaseConsole application more sophisticated by creating classes responsible for processing commands and creating an item template for the command processor classes. First, let's make a small change in the application architecture, and add the CommandProcessor.cs file shown in Listing 4-2 to the BaseConsole project.



```
namespace ConsoleBase
{
    internal abstract class CommandProcessor
    {
        public abstract void ProcessCommand(string pars);
    }
}
```

> Code file [CommandProcessor.cs] available for download at Wrox.com

This will be the base class of types responsible for processing a simple command. You associate a class with the related command using the DisplayName attribute. Create a new CommandProcessorItem.cs file to project with the source code shown in Listing 4-3.



> Code file [CommandProcessorItem.cs] available for download at Wrox.com

CommandProcessorItem.cs will be the base of the project item you will export. In its current form, it acts as a working class responsible for processing the command "list". To prepare the application for the command processor semantics, let's modify the Program.cs file. Add the following using directives to the top of the file: