# 612 Chapter 14 Graphical User Interfaces with Windows Forms: Part I

```
// display information == Icon
else if (sender == informationRadioButton)
{
    IconType = MessageIcon.Information;
}
// display question mark Icon
else if (sender == questionRadioButton)
{
    IconType = MessageIcon.Question;
}
// display stop Icon
else if (sender == stopRadioButton)
{
    IconType = MessageIcon.Stop;
}
// // only one option left--display warning Icon
else{
    IconType = MessageIcon.Warning;
}

// display MessageBox and Button pressed
private void displayButton_Click(Object sender, EventArgs e)
{
    // display MessageBox and store
    // the value of the Button was pressed
    DialogResult result = MessageBox.Show("This is your Custom MessageBox.", "Custom MessageBox", ButtonType, IconType);

// to check which Button was pressed in the MessageBox
// change text displayed accordingly
switch (result)
{
    case DialogResult.OK:
        displayLabel.Text = "OK was pressed.\n        break;
    case DialogResult.Cancel:
        displayLabel.Text = "Cancel was pressed.\n        break;
    case DialogResult.Abort:
        displayLabel.Text = "Abort was pressed.\n        break;
    case DialogResult.Retry:
        displayLabel.Text = "Retry was pressed.\n        break;
    case DialogResult.Ignore:
        displayLabel.Text = "Ignore was pressed.\n        break;
    case DialogResult.Yes:
        displayLabel.Text = "Yes was pressed.\n        break;
}
```

Fig. 14.28 | Using RadioButtons to set message-window options. (Part 3 of 4)