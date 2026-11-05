# The common control events

| Event | Attribute | Controls |
|---|---|---|
| Click | OnClick | Button, image button, link button, image map |
| Command | OnCommand | Button, image button, link button |
| TextChanged | OnTextChanged | Text box |
| SelectedIndexChanged | OnSelectedIndexChanged | Drop-down list, list box, radio button list, check box list. |
| CheckedChanged | OnCheckedChanged | Check box, radio button |

# Postback events and non-postback events

Certain events cause the form to be posted back to the server immediately, which are called the postback events. For example, the click event such as, Button.Click.

Some events are not posted back to the server immediately, these are called non-postback events.

For example, the change events or selection events such as CheckBox.CheckedChanged. The nonpostback events could be made to post back immediately by setting their AutoPostBack property to true.

# Default Events

Every control has a default event. The default event for the Page object is Load event and default event for the button control is the Click event. The default event handler could be created in Visual Studio, just by double clicking the control in design view.

# Default events for common controls

| Control | Default Event |
|---|---|
| AdRotator | AdCreated |
| BulletedList | Click |
| Button | Click |
| Calender | SelectionChanged |
| CheckBox | CheckedChanged |
| CheckBoxList | SelectedIndexChanged |