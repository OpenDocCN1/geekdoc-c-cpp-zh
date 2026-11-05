![](bbox=[0.19, 0.111, 0.596, 0.302])

**Figure 10-32** Message displayed from Place Order menu option

The ComboBox object allows special requests to be typed. Any new selections set new values for the instance of the Order class. When users type values in the text area of the ComboBox object, the keyPress() event is fired. Figure 10-33 illustrates a typed entry for the ComboBox object. The MessageBox.Show() method is used to display messages from the menu options. Figure 10-33 is displayed from the File, Display Order option.

![](bbox=[0.19, 0.526, 0.642, 0.734])

**Figure 10-33** Message displayed from Current Order menu option

When events are raised from the Edit menu, the event-handler methods display a message indicating the selections are being cleared. Then, the control on the form GUI is cleared and the Order instance data member is set back to its default value. Figure 10-34 shows the result of selecting the Edit, Special Requests menu option.