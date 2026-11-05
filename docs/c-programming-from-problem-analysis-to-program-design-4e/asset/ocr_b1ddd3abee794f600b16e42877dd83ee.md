```
catch (DirectoryNotFoundException exc)
{
    lblError.Text = "Invalid directory"
        + exc.Message;
}
catch (InvalidDataException exc)
{
    lblError.Text = "Invalid format in data stream"
        + exc.Message;
}
catch (System.IO.IOException exc)
{
    lblError.Text = exc.Message;
}
}
private void FrmWaterDepth_FormClosing(object sender,
    FormClosingEventArgs e)
{
    try
    {
        fil.Close( );
    }
    catch (IOException exc)
    {
        lblError.Text = exc.Message;
    }
}
public void ClearForm( )
{
    txtBxLocation.Text = string.Empty;
    txtBxState.Text = string.Empty;
    txtBxMile.Text = string.Empty;
    txtBxLow1.Text = string.Empty;
    txtBxLow2.Text = string.Empty;
    txtBxLow3.Text = string.Empty;
    txtBxLow4.Text = string.Empty;
    txtBxHi1.Text = string.Empty;
    txtBxHi2.Text = string.Empty;
    txtBxHi3.Text = string.Empty;
    txtBxHi4.Text = string.Empty;
    lblError.Text = string.Empty;
    txtBxLocation.Focus( );
}
}
```

When the form is loaded, objects of the ShoalArea and StreamWriter classes are instantiated. When the form is closing, the file is closed. A special method was added to store the data in the file. This method is called from the button-click event handler. Much of the functionality for the application is written in this method. Values are