# Figure 1.26

Drop down the list to add a control to a StatusStrip.

![](bbox=[0.07, 0.18, 0.55, 0.48])

# Displaying the Date and Time

You use the properties and methods of the DateTime structure to retrieve and format the current date and time. The Now property holds the system date and time in a numeric format that can be used for calculations. You can format the date and/or time for display using one of the following methods: ToShortDateString, ToLongDateString, ToShortTimeString, or ToLongTimeString. The actual display format of each method depends on the local system settings.

You can set the display value of StatusStripLabels in any procedure; however, the display does not update automatically. Generally, you will set initial values in the Form_Load event procedure and use a Timer component to update the time.

# Using a Timer Component

To use a Timer component, you add the component to the form, set some properties, and write code in the Timer's Tick event handler. Add the Timer component from the Components section of the toolbox. Then in the Properties window, set the Enabled property to true and set the Interval property. The Interval is measured in milliseconds; set the Interval to 1000 to make the Timer's Tick event fire every second.

```
Private Sub Timer1_Tick(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles Timer1.Tick
    ' Update the time in the status bar.

    DateToolStripStatusLabel.Text = Today.ToShortDateString
    TimeToolStripStatusLabel.Text = Now.ToLongTimeString
End Sub
```