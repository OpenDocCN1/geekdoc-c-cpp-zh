```
```csharp
static void Main( )
{
    Application.Run(new ClubForm( ));
}

private void lstBoxEvents_SelectedIndexChanged
                 (object sender, System.EventArgs e)
{
    // Single selection option
    // this.txtBoxResult.Text =
    //     this.lstBoxEvent.Text;
    string result = " ";
    foreach (string activity in
             lstBoxEvents.SelectedItems)
    {
        result += activity + "   ";
    }
    this.txtBoxResult.Text = result;
}

private void btnNew_Click(object sender,
                          System.EventArgs e)
{
    lstBoxEvents.Items.Add(txtBoxNewAct.Text);
    txtBoxNewAct.Clear( );
}
}
```
```

To add functionality, the btnNew Button object was set as the value for the AcceptButton property of the Form object. This enables the user to press the Enter key after typing in new entries. Now the Enter key functions in the same way as clicking the left mouse button on the btnNew Button object. The btnNew_Click() event is fired when the user clicks the mouse or presses the Enter key. In the btnNew_Click() event-handler method, the TextBox object was also cleared using the Clear() method. This was done after the value was typed into the TextBox object, retrieved, and added to the ListBox object. Table 10-1 includes a list of properties set for the ListBoxExample application.