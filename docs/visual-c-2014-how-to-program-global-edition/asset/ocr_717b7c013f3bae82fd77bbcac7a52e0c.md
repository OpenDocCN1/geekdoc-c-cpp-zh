# Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

```
// update Label at every tick
private void clockTimer_Tick(object sender, EventArgs e)
{
    // current time (Now), convert to string
    displayLabel.Text = DateTime.Now.ToLongTimeString();
}
```

![](bbox=[0.278, 0.266, 0.719, 0.351])

Fig. 15.50 | User-defined control with a Timer and a Label.(Part 2 of 2.)

# Timers

Timers (System.Windows.Forms namespace) are non-visual components that generate Tick events at set interval. This interval is set by the Timer's Interval property, defines the number of milliseconds (thousands of a second) between events. By default, timers are disabled and do not generate events.

# Adding a User Control

This app contains a user control (ClockUserControl) and a Form that displays the user control. create a Windows app, create a UserControl by selecting Project > Add User Control... This displays a dialog from which we select the type of item to add—user controls are already selected. We define the name (and the class) ClockUserControl.our empty ClockControl is displayed as a grey rectangle.

# Designing the User Control

You can treat this control like a Windows Form, meaning that you can add controls using the Toolbox and set properties using the Properties window. However, instead of creating an app, you're creating a new window composed of other controls. Add a Label (displayLabel) and a Timer (clockTimer) to the UserControl. Set the Timer interval to 1000 milliseconds and set displayLabel.text with each Tick event (lines 18–22; the fault event). To generate events, clockTimer must be enabled by setting property Enabled in the Properties window.

Structure DateTime (namespace System) contains properties Now, which returns the current time. ToLongTimeString converts Now to a string containing the current hour, minute and second (along with AM or PM, depending on your locale). We use this to show the time in displayLabel in line 21.

Once created, our control appears as an item in the Toolbox in the section Project Components, where ProjectName is your project name. You may need to switch to the app Form before the item appears in the Toolbox. To use, simply drag it to the Form and run the Windows app. We gave the ClockUserControl object a