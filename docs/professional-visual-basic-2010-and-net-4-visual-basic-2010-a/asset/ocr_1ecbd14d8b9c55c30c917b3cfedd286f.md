and passes this path to the child of the ElementHost1 control. Because the child object is in fact an instance of the class WpfInteropCtrl.UserControl1, the generic child property can be cast to this object, which supports the public property defined as part of the user control's definition, discussed earlier.

At this point, if you are following along with the text, you should save, build, and run your project. The project will work, although to be honest at this point it isn't doing too much. It illustrates that you can, in fact, host classes from the System.Windows.Controls namespace in an ElementHost control.

# Custom Display Masking

The next part of this demonstration involves altering the display of the ElementHost content based on code located within the Windows Form. Accordingly, the next block of code uses a geometric shape to overlay a mask above the selected display, making it possible to round the corners or the entire image. The application of the mask occurs based on the second ComboBox control you added to the form.

This control was assigned three values, and when one of the values is selected, it triggers the ComboBox2.SelectedIndexChanged event, which has been handled in this code. The code follows a best practice and calls a private method that implements the appropriate action based on which value was selected. The method ApplyMask uses a Select Case statement to identify which of the three fixed maps has been selected and then either disables the clipping region or enables a clipping region of the appropriate shape.

The clipping region is a WPF property available on WPF controls. The Clip property enables you to overlay a given control with a geometric shape that masks out portions of the targeted control. This example implements two simple masks: an ellipse and a rectangle. Selecting to not have a mask sets the Clip property for the Child object within the control ElementHost1 to Nothing. However, selecting a mask to screen out a portion of the display results in the code calling one of a pair of methods, EllipseMask and RectMask, each of which is focused on a single geometric shape.

These two methods share the majority of their logic, first getting the available display area from ElementHost1's Child property. Both then use the TextBoxMargin to allow the user to change the size of the margin surrounding the clip region. Note that in both cases the margin isn't applied in the same manner as setting a margin in WPF was.

Under WPF, a Margin property is defined as a thickness or distance between the edge of the control and the edge of the display for each of the four sides. Thus, both the left and right or top and bottom values are the same. However, in the case of a clipping region, the code is defining the size of a rectangle. Thus, the size of the rectangle needs to account for the fact that moving the top of the image 10 pixels lower means that the box needs to be 20 pixels smaller on the length of the side so that the 10 pixels from the top balance the 10 matching pixels on the bottom. This is why the margin is doubled when describing the height and width, but not doubled when defining the upper-left corner location. To get this feature you'll want to create an event handler with an implementation similar to what is shown in the following snippet:

```
Private Sub ComboBox2_SelectedIndexChanged(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) _
    Handles ComboBox2.SelectedIndexChanged
    ApplyMask()
End Sub
Private Sub ApplyMask()
    Select Case ComboBox2.SelectedIndex
        Case 0
            ElementHost1.Child.Clip = Nothing
            TextBoxMargin.Enabled = False
            TextBoxRounding.Enabled = False
        Case 1
            EllipseMask()
            TextBoxMargin.Enabled = True
            TextBoxRounding.Enabled = False
        Case 2
            RectMask()
```