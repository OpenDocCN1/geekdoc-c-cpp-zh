
The `[Description]` attribute defined on the `Message` property is used within the property grid in Visual Studio to provide extra information about the property, as shown in Figure 44-8.

As it stands, the activity is perfectly usable; however, there are several areas that should be addressed to make this more user-friendly. As you have seen with activities such as the `Pick` earlier in the chapter, an activity may have some mandatory properties that, when not defined, produce an error glyph on the design surface. To get the same behavior from your activity, you need to extend the code.

![](img/d7d2ffa0a76feaab821930e95daace93_1378_0.png)

## Activity Validation

When an activity is placed on the design surface, the Designer will look in two places for validation information. The simplest form of validation is to add a `[RequiredArgument]` attribute to the argument property. If the argument is not defined, the exclamation mark glyph is shown to the right of the activity name, as in Figure 44-9.

![](img/d7d2ffa0a76feaab821930e95daace93_1378_1.png)

If you hover over the glyph, a tooltip is displayed that states “Value for a required activity argument ‘Message’ was not supplied.” This is a compilation error, so you need to define a value for this argument before you can execute your application.

In the case where there are multiple properties that may be related, you can override the `CacheMetadata` method to add on some extra validation code. This method is called prior to the activity being executed; within it you can check that mandatory arguments are defined and optionally add extra metadata to the passed argument. You can also add extra validation errors (or warnings) by calling one of the `AddValidationError` overrides on the `CodeActivityMetadata` object passed to the `CacheMetadata` method.

Now that you have completed the activity validation, the next thing to do is to change the rendering behavior of the activity, as the current Designer experience is provided for you, and it could stand to be made more interesting.

## Designers

When an activity is rendered onscreen, it is typical to associate a designer with the activity. The job of the designer is to provide the on-screen representation of that activity, and in Workflow 4 this representation is done in XAML. If you haven’t used XAML before we recommend looking at Chapter 35, “Core WPF,” before continuing.

The design-time experience for an activity is typically created in a separate assembly from the activity itself, as this design experience is unnecessary at runtime. Visual Studio includes an Activity Designer Library project type that is an ideal starting point, as when you create a project using this template you’re provided with a default activity designer that you can then alter as appropriate.

Within the XAML for your designer, you can provide anything you wish — including animations, if so desire. Less is usually more when it comes to user interfaces, and we suggest looking at the preexisting activities in order to get a feel for what is appropriate.

First, we’ll create a simple designer and associate this with the `DebugWrite` activity. The code that follows shows the template created for you when you add an activity designer to your project (or when you construct a new activity designer library project). Again, this code is available in the 04_CustomActivities solution.

```
<sap:ActivityDesigner x:Class="Activities.Presentation.DebugWriteDesigner"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:sap="clr-namespace:System.Activities.Presentation;
assembly=System.Activities.Presentation"
xmlns:sapv="clr-namespace:System.Activities.Presentation.View;
assembly=System.Activities.Presentation"

<Grid>

</Grid>
</sap:ActivityDesigner>
```

The XAML created simply constructs a grid and also includes some imported namespaces, which may be needed by your activity. Obviously, there is little content within the template, so to begin we add in a label and a text box that will be used to define the message.

```
<Grid>
  <Grid.ColumnDefinitions>
    <ColumnDefinition Width="Auto"/>
    <ColumnDefinition Width="*"/>
  </Grid.ColumnDefinitions>
  <TextBlock Text="Message" Margin="0,0,5,0"/>
  <TextBox Text="{Binding Path=ModelItem.Message, Mode=TwoWay}" Grid.Column="1"/>
</Grid>
```

The XAML here constructs a binding between the Message property of the activity and the text box. Within the designer XAML, you can always reference the activity being designed by using the ModelItem reference.

In order to associate the designer defined above with the DebugWrite activity, you also need to alter the activity and add on a Designer attribute (you can also implement the IRegisterMetadata interface but we don't cover that further in this chapter).

```
[Designer("Activities.Presentation.DebugWriteDesigner, Activities.Presentation")]
public class DebugWrite : CodeActivity
{
  ...
}
```

Here, we've used the [Designer] attribute to define the link between the designer and the activity. It's good practice to use the string version of this attribute, as that ensures that there is no reference to the design assembly within the activity assembly.

Now when you use an instance of the DebugWrite activity within Visual Studio, you'll see something like Figure 44-10

![](img/d7d2ffa0a76feaab821930e95daace93_1379_0.png)

The problem with this, however, is the Message property — it's not showing the value defined within the property grid, and if you try to set a value by typing it into the text box, you'll receive an exception.

The reason is that you're trying to bind a simple text value to an InArgument<string> type, and in order to do that, you need to use another couple of built-in classes that come with Workflow 4 — the ExpressionTextBox and the ArgumentToExpressionConverter. The full XAML for the designer is now as follows. We have added boldface to the lines that have been added or modified.

```
<sap:ActivityDesigner x:Class="Activities.Presentation.DebugWriteDesigner"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:sap="clr-namespace:System.Activities.Presentation;
assembly=System.Activities.Presentation"
xmlns:sapv="clr-namespace:System.Activities.Presentation.View;
assembly=System.Activities.Presentation"
xmlns:sadc="clr-namespace:System.Activities.Presentation.Converters;
assembly=System.Activities.Presentation"
>
<sap:ActivityDesigner.Resources>
  <sadc:ArgumentToExpressionConverter x:Key="argConverter"/>
</sap:ActivityDesigner.Resources>
<Grid>
  <Grid.ColumnDefinitions>
    <ColumnDefinition Width="Auto"/>
    <ColumnDefinition Width="*"/>
  </Grid.ColumnDefinitions>
  <TextBlock Text="Message" Margin="0,0,0,0" />
  <sapv:ExpressionTextBox Grid.Column="1"
    Expression="{Binding Path=ModelItem.Message, Mode=TwoWay,
      Converter={StaticResource argConverter},
      ConverterParameter=In}"
    OwnerActivity="{Binding ModelItem}"/>
</Grid>
</sap:ActivityDesigner>
```

*code download 04_CustomActivitiesFirst*

We have included a new namespace in the file — the System.Activities.Presentation.View. This includes the converter used to convert between an expression onscreen and the Message property of the activity — this is the ArgumentToExpressionConverter, which has been added to the resources of the XAML file.

Then we replaced the standard TextBox control with an ExpressionTextBox. This control is used to permit the user to enter expressions as well as simple text, so the DebugWrite activity could include an expression combining many values from the running workflow, rather than just a simple text string. With those changes in place, the activity behaves much more like the built-in activities.

## Custom Composite Activities

A common requirement with activities is to create a composite activity — that is, an activity that contains other child activities. You have already seen examples, such as the Pick activity and the Parallel activity.

The execution of a composite activity is entirely up to the programmer — you could, for example, have a random activity that only schedules one of its children, or an activity that bypasses some children based on the current day of the week. The simplest execution pattern would be to execute all children, but as the developer you can decide how child activities are executed and also when your activity is complete.

The first type of composite activity we create is a "retry" activity. It is quite common to try an operation, and if it fails, retry it a number of times before having it fail. The pseudo-code for this activity is as follows:

```
int iterationCount = 0;
bool looping = true;
while ( looping )
{
  try
  {
    // Execute the activity here
    looping = false;
  }
  catch (Exception ex)
  {
    iterationCount += 1;
    if ( iterationCount >= maxRetries )
      rethrow;
  }
}
```
