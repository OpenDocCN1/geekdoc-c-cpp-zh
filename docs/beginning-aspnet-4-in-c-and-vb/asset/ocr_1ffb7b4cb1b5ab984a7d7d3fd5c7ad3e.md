# ACTIVITIES

Everything in a workflow is an activity, including the workflow itself. The workflow is a specific type of activity that typically allows other activities to be defined within it — this is known as a composite activity, and you see other composite activities later in this chapter. An activity is just a class that ultimately derives from the Activity class.

The Activity class defines a number of overridable methods, and arguably the most important of these is the Execute method, shown in the following snippet:

```
protected override ActivityExecutionStatus Execute
( ActivityExecutionContext executionContext )
{
    return ActivityExecutionStatus.Closed;
}
```

When the runtime schedules an activity for execution, the Execute method is ultimately called, and that is where you have the opportunity to write custom code to provide the behavior of the activity. In the simple example in the previous section, when the workflow runtime calls Execute on the CodeActivity, the implementation of this method on the code activity will execute the method defined in the code-behind class, and that displays the message on the console.

The Execute method is passed a context parameter of type ActivityExecutionContext. You will see more about this as the chapter progresses. The method has a return value of type ActivityExecutionStatus, and this is used by the runtime to determine whether the activity has completed successfully, is still processing, or is in one of several other potential states that can describe to the workflow runtime what state the activity is in. Returning ActivityExecutionStatus.Closed from this method indicates that the activity has completed its work and can be disposed of.

Numerous standard activities are provided with WF, and the following sections provide examples of some of these together with scenarios in which you might use these activities. The naming convention for activities is to append Activity to the name; so for example, the code activity previously shown in Figure 57-2 is defined by the CodeActivity class.

All of the standard activities are defined within the System.Workflow.Activities namespace, which in turn forms part of the System.Workflow.Activities.dll assembly. There are two other assemblies that make up WF — these are System.Workflow.ComponentModel.dll and System.Workflow.Runtime.dll.

# IfElseActivity

As its name implies, this activity acts like an If-Else statement in C#.

When you drop an IfElseActivity onto the design surface, you will see an activity as displayed in Figure 57-3. The IfElseActivity is a composite activity in that it constructs two branches (which themselves are types of activity, in this case IfElseBranchActivity). Each branch is also a composite activity that derives from SequenceActivity — this class executes each activity in turn from top to bottom. The Designer adds the "Drop Activities Here" text to indicate where child activities can be added.

The first branch, as shown in Figure 57-3, includes a glyph indicating that the Condition property needs to be defined. A condition derives from ActivityCondition and is used to determine whether that branch should be executed.

When the IfElseActivity is executed, it evaluates the condition of the first branch, and if the condition evaluates to true the branch is executed. If the condition evaluates to false, the IfElseActivity

![](bbox=[0.7, 0.68, 0.95, 0.94])