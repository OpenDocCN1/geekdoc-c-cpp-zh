
Last, if neither the `Approved` nor `Rejected` event is raised, the `DelayActivity` ultimately completes after its delay expires, and the expense report could then be routed to another manager — potentially looking up that person in Active Directory. In the example, a dialog is displayed to the user when the `RequestApproval` activity is executed, so if the delay executes, you also need to close the dialog, which is the purpose of the activity named `HideDialog` in Figure 57-6.

The code for this example is available in the `02 Listen` directory. Some concepts used in that example have not been covered yet — such as how a workflow instance is identified and how events are raised back into the workflow runtime and ultimately delivered to the right workflow instance. These concepts are covered in the section titled “Workflows.”

## Activity Execution Model

So far, this chapter has discussed the execution of an activity only by the runtime calling the `Execute` method. However, an activity may go through a number of states while it executes — these are presented in Figure 57-7.

![](img/d7d2ffa0a76feaab821930e95daace93_1822_0.png)

FIGURE 57-7

An activity is first initialized by the `WorkflowRuntime` when the runtime calls the activity’s `Initialize` method. This method is passed an `IServiceProvider` instance, which maps to the services available within the runtime. These services are discussed in the “Workflow Services” section later in the chapter. Most activities do nothing in this method, but the method is there for you to do any setup necessary.

The runtime then calls the `Execute` method, and the activity can return any one of the values from the `ActivityExecutionStatus` enum. Typically, you will return `Closed` from your `Execute` method, which indicates that your activity has finished processing; however, if you return one of the other status values, the runtime will use this to determine what state your activity is in.

You can return `Executing` from this method to indicate to the runtime that you have extra work to do — a typical example of this is when you have a composite activity that needs to execute its children. In this case, your activity can schedule each child for execution and then wait for all children to complete before notifying the runtime that your activity has completed.

## CUSTOM ACTIVITIES

So far, you have used activities that are defined within the `System.Workflow.Activities` namespace. In this section, you learn how to create custom activities and extend these activities to provide a good user experience at both design time and runtime.

To begin, you create a `WriteLineActivity` that can be used to output a line of text to the console. Although this is a trivial example, it will be expanded to show the full gamut of options available for custom

In this method, first validate the arguments passed in, and then call the base class Validate method to obtain a ValidationErrorCollection. Although this is not strictly necessary here, if you are deriving from an activity that has a number of properties that also need to be validated, calling the base class method will ensure that these are also checked.

The code then coerces the passed obj parameter into a WriteLineActivity instance, and also checks if the activity has a parent. This test is necessary because the Validate function is called during compilation of the activity (if the activity is within a workflow project or activity library), and, at this point, no parent activity has been defined. Without this check, you cannot actually build the assembly that contains the activity and the validator. This extra step is not needed if the project type is class library.

The last step is to check that the Message property has been set to a value other than an empty string. This uses a static method of the ValidationError class, which constructs an error that specifies that the property has not been defined.

To add validation support to your WriteLineActivity, the last step is to add the ActivityValidation attribute to the activity, as shown in the following snippet:

```
```csharp
[ActivityValidator(typeof(WriteLineValidator))]
public class WriteLineActivity: Activity
{
}
```
```

If you compile the application and then drop a WriteLineActivity onto the workflow, you should see a validation error, as shown in Figure 57-9; clicking this error will take you to that property within the property grid.

If you enter some text for the Message property, the validation error will be removed, and you can then compile and run the application.

Now that you have completed the activity validation, the next thing to do is to change the rendering behavior of the activity to add a fill color to that activity. To do this, you need to define both an ActivityDesigner class and an ActivityDesignerTheme class, as described in the next section.

![](img/d7d2ffa0a76feaab821930e95daace93_1825_0.png)

## Themes and Designers

The onscreen rendering of an activity is performed by using an ActivityDesigner class, and this can also use an ActivityDesignerTheme.

The theme class is used to make simple changes to the rendering behavior of the activity within the Workflow Designer:

```
```csharp
public class WriteLineTheme: ActivityDesignerTheme
{
    /// <summary>
    /// Construct the theme and set some defaults
    /// </summary>
    /// <param name="theme">...</param>
    public WriteLineTheme(WorkflowTheme theme)
        : base(theme)
    {
        this.BackColorStart = Color.Yellow;
        this.BackColorEnd = Color.Orange;
        this.BackgroundStyle = LinearGradientMode.ForwardDiagonal;
    }
}
```
```

A theme is derived from ActivityDesignerTheme, which has a constructor that is passed a WorkflowTheme argument. Within the constructor, set the start and end colors for the activity, and then define a linear gradient brush, which is used when painting the background.

Once you have added the image file and set its build action to Embedded Resource, you can then attribute the activity as shown in the following snippet:

```
[ActivityValidator(typeof(WriteLineValidator))]
[Designer(typeof(WriteLineDesigner))]
[ToolboxBitmap(typeof(WriteLineActivity), "Resources.WriteLine.png")]
public class WriteLineActivity: Activity
{
  .
}
```

The ToolboxBitmap attribute has a number of constructors defined, and the one being used here takes a type defined in the activity assembly and the name of the resource. When you add a resource to a folder, its name is constructed from the namespace of the assembly and the name of the folder the image resides within — so the fully qualified name for the resource here is CustomActivities.Resources.WriteLine.png. The constructor used with the ToolboxBitmap attribute appends the namespace that the type parameter resides within to the string passed as the second argument, so this will resolve to the appropriate resource when loaded by Visual Studio.

The last class you need to create is derived from ActivityToolboxItem. This class is used when the activity is loaded into the Visual Studio toolbox. A typical use of this class is to change the displayed name of the activity on the toolbox — all of the built-in activities have their names changed to remove the word “Activity” from the type. In your class, you can do the same by setting the DisplayName property to “WriteLine.”

```
[Serializable]
public class WriteLineToolboxItem: ActivityToolboxItem
{
    /// <summary>
    /// Set the display name to WriteLine - i.e. trim off
    /// the 'Activity' string
    /// </summary>
    /// <param name="t"></param>
    public WriteLineToolboxItem(Type t)
        : base(t)
    {
        base.DisplayName = "WriteLine";
    }

    /// <summary>
    /// Necessary for the Visual Studio design time environment
    /// </summary>
    /// <param name="info"></param>
    /// <param name="context"></param>
    private WriteLineToolboxItem(SerializationInfo info,
        StreamingContext context)
    {
        this.Deserialize(info, context);
    }
}
```

The class is derived from ActivityToolboxItem and overrides the constructor to change the display name; it also provides a serialization constructor that is used by the toolbox when the item is loaded into the toolbox. Without this constructor, you will receive an error when you attempt to add the activity to the toolbox. Note that the class is also marked as [Serializable].

The toolbox item is added to the activity by using the ToolboxItem attribute as shown:

```
[ActivityValidator(typeof(WriteLineValidator))]
[Designer(typeof(WriteLineDesigner))]
[ToolboxBitmap(typeof(WriteLineActivity), "Resources.WriteLine.png")]
[ToolboxItem(typeof(WriteLineToolboxItem))]
public class WriteLineActivity: Activity
{
  .
}
```
