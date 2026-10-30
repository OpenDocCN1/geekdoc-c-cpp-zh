# Part VI: Microsoft Access Programming Fundamentals

This means that a control’s BeforeUpdate is good for validating a single control while the form’s BeforeUpdate is good for validating multiple controls on the form. The form’s BeforeUpdate would be a good place to validate that values in two different controls are in agreement with each other (such as a zip code in one text box and the city in another text box), instead of relying on the BeforeUpdate in each of the controls.

You create event procedures for control events in exactly the same way you create procedures for form events. You select [Event Procedure] in the Property Sheet for the event and then add VBA code to the event procedure attached to the event. Table 26.5 shows each control event property, the event it recognizes, and how it works. As you review the information in Table 26.5, keep in mind that not every control supports every type of event.

| **TABLE 26.5** | **Control Events** |
|---|---|
| **Event** | **When the Event Is Triggered** |
| BeforeUpdate | Before changed data in the control is updated to the underlying recordset |
| AfterUpdate | After changed data is transferred to the form’s recordset |
| Dirty | When the contents of a control change |
| Undo | When the control is returned to a clean state |
| Change | When the contents of a text box change or a combo box’s text changes |
| Updated | When an ActiveX object’s data has been modified |
| NotInList | When a value that isn’t in the list is entered into a combo box |
| Enter | Before a control receives the focus from another control |
| Exit | Just before the control loses focus to another control |
| GotFocus | When a nonactive or enabled control receives the focus |
| LostFocus | When a control loses the focus |
| Click | When the left mouse button is pressed and released (clicked) on a control |
| DblClick | When the left mouse button is pressed and released (clicked) twice on a control or label |
| MouseDown | When a mouse button is pressed while the pointer is on a control |
| MouseMove | When the mouse pointer is moved over a control |
| MouseUp | When a pressed mouse button is released while the pointer is on a control |
| KeyDown | When any key on the keyboard is pressed when a control has the focus or when a SendKeys macro action is used |
| KeyPress | When a key is pressed and released on a control that has the focus or when a SendKeys macro action is used |
| KeyUp | When a pressed key is released or immediately after a SendKeys macro is used |