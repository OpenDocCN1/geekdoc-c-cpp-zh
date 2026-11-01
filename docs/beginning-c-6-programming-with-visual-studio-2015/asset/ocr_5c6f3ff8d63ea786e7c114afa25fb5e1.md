# TABLE 14-1 (continued)

| EVENT | DESCRIPTION |
|---|---|
| GotFocus | Occurs when a control receives focus. Do not use this event to perform validation of controls. Use Validating and Validated instead. |
| LostFocus | Occurs when a control loses focus. Do not use this event to perform validation of controls. Use Validating and Validated instead. |
| MouseDoubleClick | Occurs when a control is double-clicked. |
| MouseDown | Occurs when the mouse pointer is over a control and a mouse button is pressed. This is not the same as a Click event because MouseDown occurs as soon as the button is pressed and before it is released. |
| MouseMove | Occurs continually as the mouse travels over the control. |
| MouseUp | Occurs when the mouse pointer is over a control and a mouse button is released. |

You will see many of these events in the examples in this chapter.

# Handling Events

There are two basic ways to add a handler for an event. One way is to use the Events list in the Properties window, shown in Figure 14-2, which is displayed when you click the lightning bolt button.

![](bbox=[0.15, 0.8, 0.5, 0.9])

# FIGURE 14-2

To add a handler for a particular event, either type the name of the event and press Return, or double-click to the right of the event name in the Events list. This causes the event to be added to the XAML tag. The method signature to handle the event is added to the C# code-behind file.