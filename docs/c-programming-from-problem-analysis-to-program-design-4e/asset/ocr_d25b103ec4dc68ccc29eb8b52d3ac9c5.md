![](bbox=[0.185, 0.12, 0.746, 0.442])

**FIGURE 10-8**  KeyPress and SelectedIndexChanged events fired

Sunflower was not placed in the collection list at design time; it is typed when the program is launched. The KeyPress() event-handler method fired (multiple times). Remember KeyPress() is fired for each and every character pressed. Thus, it is fired when the character S is typed; it is fired again when the character u is typed, and so on. So the KeyPress() method is executed multiple times to get the characters from the combo box and display them in the text box. This KeyPress() method uses the Text property of the ComboBox to get the selection and the Text property of the TextBox object to set the value for display purposes.

Two selections were made from the ListBox object. The SelectionMode for the ListBox object was set to MultiExtended. The SelectedIndexChanged() method set the text of the TextBox object by concatenating (+=) the selections into the Text property.

Most Windows applications include a number of menu options. In the next section, you will add menus to this application and learn how easy it is to add traditional menus found on most Windows applications.

# # MenuStrip Control Objects

Menus offer the advantage of taking up minimal space on your window. They enable you to add more functionality to your application through offering additional options to the user. In the System.Windows.Forms namespace, a number of classes are available that enable you to add layers of menus to your applications.