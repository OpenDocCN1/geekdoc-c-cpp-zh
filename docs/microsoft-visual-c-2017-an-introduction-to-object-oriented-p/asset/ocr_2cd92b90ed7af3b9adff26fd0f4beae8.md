# Handling Mouse and Keyboard Events

A MouseDown event can occur without a corresponding Mouseup if the user presses the mouse but switches focus to another control or application before releasing the mouse button.

| MouseEventArgs property | Description |
| --- | --- |
| Button | Specifies which mouse button triggered the event; the value can be Left, Right, Middle, or none |
| Clicks | Specifies the number of times the mouse was clicked |
| X | The x-coordinate where the event occurred on the control that generated the event |
| Y | The y-coordinate where the event occurred on the control that generated the event |

**Table 13-3** Properties of the MouseEventArgs class

MouseClicked and Click are separate events. The Click event takes an EventArgs parameter, but MouseClick takes a MouseEventArgs parameter. For example, if you define a Click event, you do not have the MouseEventArgs properties.

13-21 contains a Form with a single Label name locationLabel that changes as the user continues to click the mouse on. The figure shows how the Label changes in response to a series of clicks. Initially, the Label is empty (that is, the default Text property has been deleted and not replaced), the following code was added to the Form1.cs file:

```
private void MouseClick(object sender, MouseEventArgs e)
{
    locationLabel.Text += "\nclicked at " + e.X + ", " + e.Y;
}
```

Every time the mouse is clicked on the Form, the Label is appended with a new line that contains ‘Clicked at’ and the x- and y-coordinate position where the click occurred on the Form. Figure 13-21 shows the Form after the user has clicked nearer the top left, top right, bottom right, and bottom left areas of the Form.