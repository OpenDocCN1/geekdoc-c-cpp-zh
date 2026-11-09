+   9. Add one Label and one TextBox control and set the Text property of the Label1 control to Select Date.

+   10. Set the Width property of TextBox1 as 341px.

+   11. Set the Caption property of the Calendar control. In our case, we have set it to Welcome to Calendar control.

+   12. Click the smart tag (>) and select the Auto Format option for the Calendar control, as shown in Fig.ASP-2.61:

![](bbox=[0.316, 0.234, 0.706, 0.453])

Fig.ASP-2.61

The AutoFormat dialog box appears (Fig.ASP-2.62).

+   13. Select a Calendar format from the Select a scheme pane. In our case, we have selected Professional2 (Fig.ASP-2.62).

+   14. Click the OK button to save the settings, as shown in Fig.ASP-2.62:

![](bbox=[0.356, 0.542, 0.667, 0.73])

Fig.ASP-2.62

+   15. Double click the Default.aspx form and add the code given in Listing 2.12 to the Load event of the page.

# Listing 2.12: Illustrating the Code for Load Event of the Default.aspx Page

```
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    Calendar1.SelectedDate = DateTime.Now;
    TextBox1.Text = "Current date and time is: " + Calendar1.SelectedDate;
}
```
```