
(continued)

| Event | Description |
| --- | --- |
| Leave | Occurs when a control is left |
| LocationChanged | Occurs when the Location property value has changed |
| LostFocus | Occurs when a control loses focus |
| MouseDown | Occurs when the mouse pointer hovers over a control and a mouse button is pressed |
| MouseEnter | Occurs when the mouse pointer enters a control |
| MouseHover | Occurs when the mouse pointer hovers over a control |
| MouseLeave | Occurs when the mouse pointer leaves a control |
| MouseMove | Occurs when the mouse pointer moves over a control |
| MouseUp | Occurs when the mouse pointer hovers over a control and a mouse button is released |
| MouseWheel | Occurs when the mouse wheel moves while a control has focus |
| Move | Occurs when a control is moved |
| Resize | Occurs when a control is resized |
| TextChanged | Occurs when the Text property value has changed |
| VisibleChanged | Occurs when the Visible property value has changed |

Table 13-1 Some Control public instance events

You have used the IDE to create event-handling methods. These methods have been the events generated when double-click a Control in the IDE. For example, you have created a Click() method for a Button and a LinkClicked() method for a LinkLabel. A Form can contain any number of Controls that may have events associated with them. Additionally, a single Control might be able to raise any number of events. For example, in addition to creating a Button's default Click event, you might want to define various actions when the user's mouse rolls over the button. Table 13-1 lists only few of the many events available with Controls; any Control could conceivably raise any of the available events.

Suppose you want to create a project that has a different set of actions when the mouse is over a Button when the mouse is clicked. Figure 13-18 shows a project that has been started in the IDE. The following actions have been:

- * The Form was resized.
- The Form's Text property was changed.
- A Button was dragged onto the Form, and its Text was set to Click me.
- A Label was added to the Form, its Text was set to Hello, and its Font was increased.

## Handling Control Component Events

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_649_0.png)

Figure 13-1 Start of the ButtonTwoEvents project in the IDE

When you double-click the Button on the Form in the IDE, you generate the shell of a Click() method. You can change the method's identifier to start with an uppercase letter, and then you can add statements to change the Label's text and color when the user clicks the Button, as follows:

```sharp
private void Button1_Click(object sender, EventArgs e)
{
    label1.Text = "Button was clicked";
    label1.BackColor = Color.CornflowerBlue;
}
```

> Color.CornflowerBlue is one of C#'s predefined color properties. A complete list appears in Table 12-5 in Chapter 12.

With the Button selected on the right side of the screen, you can click the Events icon in the Properties window at. Events icon looks like a lightning bolt. Figure 13-19 shows that the Properties window displays events instead of properties and that the Click event has an associated method.

## CHAPTER 13 Handling Events

If you scroll through the Events listed in the Properties window, you can see a wide variety of Events choices. If you scroll down to MouseEnter and double-click, you can view the code for an event handler in the Form1.cs file as:

```sharp
private void button1_MouseEnter(object sender, EventArgs e)
{
}
```

When you are viewing events in the Properties window, you can return to the list of properties by clicking the Properties icon. This icon is to the immediate left of the Events icon.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_650_0.png)

Figure 13-19 The Properties window displaying events

You can rename the method to start with an uppercase letter, and you can type any statements you want within this method: For example, you might write the following method:

```sharp
private void Button1_MouseEnter(object sender, EventArgs e)
{
  label1.Text = "Go ahead";
  button1.BackColor = Color.Red;
}
```

When you run the program with the two new methods, different events can occur:

- When you enter the button with the mouse (that is pass mouse over), the Label’s Text changes to Go ahead, and the button turns red, as shown on the left in Figure 13-20.
- After the button is clicked, the Label’s Text changes again to Button was clicked, and the Label becomes blue, as shown on the right in Figure 13-20.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_650_1.png)

Figure 13-20 The OneEvents program when the mouse enters the button and after the button is clicked

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-02-200-252.
