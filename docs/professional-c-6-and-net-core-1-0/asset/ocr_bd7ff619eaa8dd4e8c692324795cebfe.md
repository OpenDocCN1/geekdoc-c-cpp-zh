```
"Load";
    this.mUILoadButton.WindowTitles.Add("Books Desktop App");
}
    return this.mUILoadButton;
}
}
```

AddNewBook continues with methods created from the recording. First, the mouse is clicked using the static method Mouse.Click. The Mouse.Click method defines several overloads: to click within the screen coordinates—using mouse modifiers—and to click controls. The first click method clicks the Load button. The coordinates defined by the second argument are relative within the control. So if you reposition this control in a newer version, it’s important that you run the test again without big changes; that’s why the control is accessed via its name. Other than the Mouse class, you can use the Keyboard class to send key inputs:

```
public void AddNewBook()
{
    // etc.

    // Click 'Load' button
    Mouse.Click(uILoadButton, new Point(20, 11));

    // Click 'Add' button
    Mouse.Click(uIAddButton, new Point(14, 9));

    // Type 'new book' in first text box next to 'Save' button
    uIItemEdit.Text = this.AddANewBookParams.UIItemEditText;

    // Type '{Tab}' in first text box next to 'Save' button
    Keyboard.SendKeys(uIItemEdit,
    this.AddANewBookParams.UIItemEditSendKeys,
        ModifierKeys.None);

    // Type 'new' in text box numbered 2 next to 'Save' button
    uIItemEdit1.Text = this.AddANewBookParams.UIItemEdit1Text;

    // Click 'Save' button
    Mouse.Click(uISaveButton, new Point(29, 19));
}
```

Input for text controls is saved in a helper class AddNewBookParams, so you can easily change the input in one place:

```
public class AddNewBookParams
{
    public string UIItemEditText ="new book";

    public string UIItemEditSendKeys ="{Tab}";

    public string UIItemEdit1Text ="new";
}
```

After you create the recording, you need to define assertions to check whether the outcome is correct. You can create asserts with the Coded UI Test Builder. Click the Add Assertions button to open the dialog shown in Figure 19.11. With this dialog, you can see the controls of the open window, see its current property values, and add assertions. After