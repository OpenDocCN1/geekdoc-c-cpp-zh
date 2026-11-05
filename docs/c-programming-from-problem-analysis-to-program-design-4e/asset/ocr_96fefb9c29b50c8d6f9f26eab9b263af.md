# LABEL, BUTTON, RADIOBUTTON, AND LISTBOX OBJECTS

As shown in Figure 15-19, Label, Button, RadioButton, and ListBox objects were added. You should be able to identify those controls on the form from your work with Windows applications. Event-handler methods for button clicks were written for the three buttons in the center of the form. Other than naming the TextBox controls using the ID property, and sizing them, no other properties were set. Their AutoPostBack property was left unchanged (set as `false`).

> **NOTE**
> 
> The four TextBox objects appear in white in Figure 15-19. They are currently storing values for first name, last name, phone, and student ID.

# SETTING THE PROPERTIES OF THE CONTROLS

The ID properties and the individual Text properties were set for the RadioButton objects. The GroupName property is set for all three RadioButton objects. It is set to the same identifier (Classif) for all three objects. Adding the three objects to a group creates a **mutually exclusive set of controls** (only one can be selected at a time). If they did not belong to a group, all three could be checked. When one of the buttons is selected, a message is displayed in the label below the radio button. So that the message is displayed as soon as the user clicks the RadioButton object, the AutoPostBack property is set to `true`. Without changing its default value, the message would not display until one of the Button objects triggered the postback event.

> **NOTE**
> 
> Remember, by default Button objects automatically trigger a postback.

The only property set for the ListBox object in the upper-right corner of the page is the ID. SelectionMode was left unchanged (set as Single). Thus, only one selection from the list box could be made. Changing the property to Multiple enables multiple selections. The program logic for determining which items were selected would also have to be modified. The AutoPostBack property was left unchanged (set as `false`). It is not necessary to post the page back to the server as soon as a selection is made from this control.

**WIRING EVENT-HANDLER METHODS** All three radio buttons were wired to the same event-handler method. This can be done by first selecting all three buttons. Using the Events icon on the Properties window the `radButtons_CheckedChanged()` method was chosen, as shown in Figure 15-20.