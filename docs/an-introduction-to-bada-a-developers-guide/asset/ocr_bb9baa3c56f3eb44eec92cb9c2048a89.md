Action IDs need to be added to the MainForm for each of the soft keys, so that the soft key action events can be identified when handling events in the OnActionPerformed() event handler:

```
static const int ID_SOFTKEY_LEFT = 101;
static const int ID_SOFTKEY_RIGHT = 102;
```

In the OnActionPerformed() event handler the soft key action events are identified by the action ID, which is registered when the soft key is created, and the relevant processing can be implemented.

The following code snippet is an example of the MainForm's OnActionPerformed() method:

```
void
MainForm::OnActionPerformed(const Osp::Ui::Control& source, int actionId)
{
    switch(actionId)
    {
    case ID_SOFTKEY_LEFT:
    {
        // Add left softkey handling code here
    }
    break;
    case ID_SOFTKEY_RIGHT:
    {
        // Add right softkey handling code here
    }
    break;
    default:
        break;
    }
}
```

The soft keys should be created during initialisation of the MainForm-(OnInitializing()):

+   1. Create an Image object and initialise.
+   2. Decode the image file into the decoded bitmap container, passing the local file path of the image file and colour format parameters.
+   3. Set the left soft key to display an icon and assign the ‘Normal’ and ‘Pressed’ images.
+   4. Set the right soft key to display a text string.
+   5. Assign unique action IDs for both soft keys.
+   6. Register IActionEventListener implemented by the MainForm class with the soft keys.

The following code snippet is an example of code that would be added to the MainForm's OnInitializing() method to create the left and right soft keys: