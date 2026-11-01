```
>assembly=System.Activities.Presentation"
>
<sap:ActivityDesigner.Resources>
  <sadc:ArgumentToExpressionConverter x:Key="argConverter"/>
  <sap:ActivityDesigner.Resources>
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

# Custom Composite Activities

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