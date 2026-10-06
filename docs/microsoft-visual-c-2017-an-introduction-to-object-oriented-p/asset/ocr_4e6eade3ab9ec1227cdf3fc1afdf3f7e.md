# Managing Multiple Controls

When Forms contain multiple Controls, you often want one to have focus. You also might want several actions to a single, shared consequence. For example, you might want the same action to occur whether the user clicks a button or presses the Enter key, or you might want multiple buttons to generate the same event when they are clicked.

# Defining Focus

When users encounter multiple GUI Controls on a Form, usually one Control has focus. For example, when a Button has focus, a user expects that clicking the button or pressing the Enter will raise an event.

TabStop is a Boolean property of a Control that identifies whether the Control will serve as a stopping place—that is, a place where focus receive—in a sequence of Tab keys. The default value for Button is true, but the default value for Label is false because Labels are not expected to be part of a tabbing sequence. TabIndex is a numeric property that indicates the order in which the Control will receive focus when the user presses the Tab key. Programmers typically use small for Tab values, beginning with 0. When a Control's TabStop is true and the Control has the lowest TabIndex of a Form's Controls, it receives focus when the Form is initialized.

> Setting the TabIndex values of two or more Controls to 0 does not cause an error. Only one Control will receive focus, however.

![](bbox=[0.104, 0.532, 0.153, 0.574])

Figure 13-24 shows a Form that contains three Buttons and a Label. Each Button is associated with a Click() event as the following:

```
private void Button1_Click(object sender, EventArgs args)
{
    Label.Text = "Button1 selected";
}
```

In the program showing in Figure 13-24, each Button has been assigned a TabIndex value in ascending order. Whether the application starts, the first Button (labeled I) has focus. Whether the user clicks that button or presses Enter, the message appears as shown on the left. In the next part of the figure, the user has pressed Tab and Enter button2, it has focus, and the Label's Text property has changed. Alternatively, the user could have clicked button2 to achieve the same result. The user could then select either of the other Buttons by clicking them as usual or by pressing Tab until the desired button has focus and then pressing Enter.