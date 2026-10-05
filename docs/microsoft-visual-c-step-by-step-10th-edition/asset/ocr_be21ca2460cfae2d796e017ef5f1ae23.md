Return to the XAML markup for the customersTabularView Grid control and set the Visibility property to Visible as follows:

Click here to view code

```
<Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Visible">
```

In the XAML markup for the customersColumnarView Grid control, set the Visibility property to Collapsed as follows:

Click here to view code

```
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Collapsed">
```

The Design window would display the original tabular layout of the Customers form. This is the default view that will be used by the app.

You have now defined the layout that will appear in the narrow view. You might be concerned that in essence all you have done is duplicated many of the controls and laid them out in a different manner. If you run the form and switch