```
private void btnShowDataDataContextValue_Click(object sender,
    RoutedEventArgs e)
{
    Car dc = this.DataContext as Car;
    MessageBox.Show("Car Make: " + dc.Make + " \nCar Model: " 
        + dc.Model);
}

private void btnChangeDataDataContextValue_Click(object sender,
    RoutedEventArgs e)
{
    Car dc = this.DataContext as Car;
    dc.Make = "Changed Make";
    dc.Model = "Changed Model";
}
```

+   4. In the MainWindow(), ensure that you can
tGenerateData() method immediately following the
InitializeComponents() call.

+   5. Run this application.
You values from the DataContext display properly in
t TextBox controls. Feel to change the values in the TextBox con-
trolls. For instance, change the Make value to Akron X, and the model
to ABC. When you are finished with your edits, click the Show Current
DataContext Value button. The changes you made to the values in the
TextBox are now reflected in the underlying DataContext object. (See
Figure 3-2).

![](bbox=[0.258, 0.565, 0.643, 0.768])

Figure 3-2:
Editing data using a TwoWay
binding mode.

+   6. Click the OK button to get rid of the message box.
You if look in the Click event handler of the Change DataContext Value
With Code-Behind button (btnChangeDataDataContextValue_Click),
You will note that the DataContext Car object properties will be
changed to and Changed Model, respectively.