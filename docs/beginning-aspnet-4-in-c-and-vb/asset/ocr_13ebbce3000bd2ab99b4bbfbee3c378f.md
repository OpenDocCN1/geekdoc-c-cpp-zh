Some concepts used in that example have not been covered yet — such as how to write custom activities or waiting on external events; however, we cover these topics later in the chapter.

# CUSTOM ACTIVITIES

So far, you have used activities that are defined within the System.Activities namespace. In this section, you learn how to create custom activities and extend these activities to provide a good user experience at both design time and runtime.

To begin, you create a DebugWrite activity that can be used to output a line of text to the console in debug builds. Although this is a trivial example, it will be expanded to show the full gamut of options available for custom activities using this example. When creating custom activities, you can simply construct a class within a workflow project; however, it is preferable to construct your custom activities inside a separate assembly, because the Visual Studio design-time environment (and specifically workflow projects) will load activities from your assemblies and can lock the assembly that you are trying to update. For this reason, you should create a simple class library project to construct your custom activities within. The code for this example is available in the 04_CustomActivities project.

A simple activity, such as the DebugWrite activity, will be derived directly from the CodeActivity base class. The following code shows a constructed activity class and defines a Message property that is displayed when the activity is executed:

```
```csharp
using System;
using System.Activities;
using System.Diagnostics;

namespace Activities
{
    public class DebugWrite : CodeActivity
    {
        [Description("The message output to the debug stream")]
        public InArgument<string> Message { get; set; }

        protected override void Execute(CodeActivityContext context)
        {
            Debug.WriteLine(Message.Get(context));
        }
    }
}
```
```

code download 04_CustomActivities

When a CodeActivity is scheduled for execution, its Execute method is called — this is where the activity actually needs to do something.

In the example, we have defined the Message property, which looks like a regular .NET property; however, its usage inside the Execute method may be unfamiliar. One of the many changes made in Workflow 4 is where state data is stored. Within Workflow 3.x, it was common to use standard .NET properties and store activity data within the activity itself. The problem with that method was that this storage was effectively opaque to the workflow runtime engine, and so in order to persist a workflow, it was necessary to perform binary persistence on all constructed activities in order to faithfully restore their data.

With Workflow 4, all data is stored outside of the individual activities — so the model here is that in order to get the value of an argument, you ask the context for the value, and in order to set the value of an argument, you provide the new value to the context. In this way, the workflow engine can track changes to state as the workflow executes and potentially stores only the changes between persistence points rather than the entire workflow data.