
```csharp
// Event handler to be used by all three CheckBoxes.
private void ComputeCost_CheckedChanged(object sender, System.EventArgs e)
{
    decimal cost = 0;
    if (this.ckBxSwim.Checked)
    {
        cost += 50;
    }
    if (this.ckBxSnorkel.Checked)
    {
        cost += 25;
    }
    if (this.ckBxDive.Checked)
    {
        cost += 100;
    }
    this.txtBxResult.Text = cost.ToString("C");
}
```

> NOTE: Notice that a nested `if` statement is not used here because the user might click one, two, or all three. A nested `if` would exit the selection statement as soon as one condition evaluated to `true`.

## Wiring One Event Handler to Multiple Objects

The Swim CheckBox `object` is wired to the `ComputeCost_CheckedChanged()` method. You can change the name associated with the event-handler method. Now with two clicks you can wire the other events. First select the Snorkel CheckBox `object`, as shown in Figure 10-16. Using the Visual Studio **Properties** window, click on the **Events** icon (lightning bolt). Move down to the CheckedChanged event. Click the down arrow associated with that event and select `ComputeCost_CheckedChanged`. Follow the same steps for the Dive CheckBox `object`.

> NOTE: Actually, this is the only event-handler method written so far; thus, it is the only one available to choose.

When you launch the application, changes to any of the CheckBox objects fire the `ComputeCost_CheckedChanged()` method.

> NOTE: A number of Form properties were set. These properties were set when the Form `object` was initially created. The Name, BackColor, ForeColor, Text, Font, and Size properties should almost always be set.

## GroupBox Objects

CheckBox objects can be grouped together using the GroupBox control. This is beneficial for visual appearance. It also helps during design because you can move or set properties that impact the entire group. However, it does not provide any additional functionality for CheckBox objects.

A GroupBox control should be placed on the form before you add the RadioButton objects to it. If you add the RadioButton objects first and then try to add the GroupBox control object on top of the RadioButton objects, it does not work as smoothly. If you add the GroupBox control object last, you need to physically drag the RadioButton objects onto the top of the GroupBox control object.

> **NOTE**
> Do not forget about the useful tools on the **FORMAT** menu. The **Align, Make Same Size, Horizontal Spacing, Vertical Spacing,** and **Center in Form** tools save you hours of time. Remember, it does matter what your interface looks like!

## RadioButton Objects

There are differences between the RadioButton and CheckBox objects, other than their visual representation. RadioButton controls appear as small circles on the Form object. They are used to give users a choice between two or more options. Remember that it is appropriate to select more than one CheckBox object. This is not the case with RadioButton objects. Normally, you group RadioButton objects by placing them on a Panel or GroupBox control. If a radio button is clicked, it is selected and all other radio buttons within the group box are deselected.

### Adding RadioButton Objects

To build on the application developed in the previous section containing the CheckBox objects, a GroupBox control is placed on the form. It should be placed there before adding objects to the group. GroupBox control objects provide an identifiable grouping for other controls. After it is dragged onto the form, a GroupBox control object must usually be resized. Using Visual Studio, you can drag three RadioButton objects on top of the GroupBox.

> **NOTE**
> After the RadioButton objects are placed on the GroupBox, you can set properties of the GroupBox and impact all members of the group. Want to make them invisible? Set the Visible property of the GroupBox. It is not necessary to set all of the members. If you want to change the font color of all radio buttons, just change the GroupBox Font property.

Setting the Text property for the GroupBox adds a labeled heading over the group of radio buttons without you having to add an additional Label object. Whatever value you type for the Text property for RadioButton objects is used to label the control. By default, the text appears to the right of the small circle, as shown in Figure 10-16. If you want the text in the label to display to the left of the small circle, set the RightToLeft property to Yes for the RadioButton control. For this example, the GroupBox Text property is set to "Skill level"; RadioButton Text properties are set to "Beginner", "Intermediate", and "Advanced". An extra Label object is added to the bottom right to display messages regarding special discounts or extra charges associated with different skill levels. The new Label object's Text property is set to "". Figure 10-16 shows the form in Design view after the Text properties are set for the newly added GroupBox and RadioButton objects.

![](img/36e48639a06772bcb0fa1ea2525b33a3_662_0.png)

**FIGURE 10-16** GroupBox and RadioButton objects added

> NOTE: Notice the box drawn around the RadioButton objects. This is added by the GroupBox control object. The heading that appears over the radio buttons is the Text property for the GroupBox.

The middle RadioButton object is set as the default by selecting true for its Checked property. This is done during design using the Checked property, located in the Properties window list of properties. You change the value by selecting true from the drop-down list. Double-clicking on the property name also toggles the setting between false (default) and true. The Visual Studio Form Designer inserts the following line of code in your program:

```csharp
this.radIntern.Checked = true;
```

> NOTE: If you plan to have more than one set of RadioButton objects on your form, each set must be associated with a different Panel or GroupBox control object. This is necessary to allow mutually exclusive selections from different categories. For example, if you had one set of buttons for skill level and another set for age group (1 to 5 years; 6 to 10 years; over 10 years), to allow selection from both categories, the two categories of radio buttons must be connected to two different group boxes or panels.

### Registering RadioButton Object Events

Like CheckBox objects, RadioButton objects raise a number of events, including `Click()` and `CheckedChanged()` events. For this application, the skill level helps determine the cost of the lessons. The prices shown on the form are actually for registrants of intermediate skill level. Those with an advanced skill level are discounted $15; beginners are charged an extra $10. Because the skill level is used to determine the cost of lessons, the RadioButton Click event is wired to the same event-handler method that was written for the CheckBox objects. Modifications are made to the method to reflect the additional problem specification.

Wire the Click event for each of the RadioButton objects—just as you wired the Scuba and Dive CheckBox objects. This can be done in Visual Studio by displaying the list of events (click on the Event lightning bolt icon) in the Properties window. Select the `Click()` event and then use the down arrow to select the event-handler method `ComputeCost_CheckedChanged()`. This is still the only event-handler method available to be displayed, as shown in Figure 10-17. No other event-handler methods have been written for this application. Figure 10-16 shows the `ckBxSnorkel` CheckBox object being wired to the `ComputeCost_CheckedChanged()` method. That same method, `ComputeCost_CheckedChanged()`, is wired to the other CheckBox objects. The Click event for the RadioButton objects is also wired to the `ComputeCost_CheckedChanged()` method shown in Figure 10-17.

![](img/36e48639a06772bcb0fa1ea2525b33a3_663_0.png)

**FIGURE 10-17** Wired Click event

Additional statements are added to the end of the `ComputeCost_CheckedChanged()` method to take the skill level into consideration. The Checked property is used again. This time, it is inspected to determine which RadioButton object is selected. This is shown next.

```csharp
if (this.radBeginner.Checked)
{
    cost += 10;
    this.lblMsg.Text = "Beginner - Extra $10 charge";
}
else
    if (this.radAdvanc.Checked)
    {
        cost -= 15;
        this.lblMsg.Text = "Advanced Discount $15";
    }
    else
    {
        this.lblMsg.Text = " ";
    }
```

> **NOTE**
> Notice that a nested `if` statement is used here with the RadioButton objects. Unlike the CheckBox objects, only one selection is possible. Thus, as soon as an expression evaluates to `true`, there is no need to test the other expressions.

Example 10-21 includes the RegForm program listing. First the RegForm.Designer.cs file is shown followed by the contents of the RegForm.cs file. Although it seems long, the Form Designer in Visual Studio generates much of the code.

### EXAMPLE 10.21

```csharp
/* RegForm.Designer.cs
 * The code in the .Designer.cs file
 * is auto generated by Visual Studio.
 */

namespace RegistrationApp
{
    partial class RegForm
    {
        // Required designer variable.
        private System.ComponentModel.IContainer
            components = null;

        // Clean up any resources being used.
        protected override void Dispose(bool disposing)
        {
            if (disposing && (components != null))
```
