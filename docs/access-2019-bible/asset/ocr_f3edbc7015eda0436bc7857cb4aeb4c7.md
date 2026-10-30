# Using option groups

Option groups let you choose exactly one value from a number of possibilities. Option groups work best when you have a small number of mutually exclusive choices to select from. Figure 18.8 shows an option group next to the Follow-Up Date text box. Option groups most commonly contain option buttons but also work with toggle buttons and check boxes.

# FIGURE 18.8

Using an option group to select a mutually exclusive value.

![](bbox=[0.2, 0.42, 0.65, 0.6])

The easiest and most efficient way to create option groups is with the Option Group Wizard. You can use it to create option groups with multiple option buttons, toggle buttons, or check boxes. When you're through, all your control's property settings are correctly set. To create an option group, switch to Design view and select the Option Group button from the Design tab's Controls group. Make sure the Use Control Wizards command is selected in the Controls group.

Each element in an option group is assigned a number in its Option Value property. When an option group is bound to a field, the Option Value is stored in that field when the record is saved.

Tip
When creating an option group for a Yes/No field (which is actually stored as a number), set the Yes value to -1 and the No value to 0.

# Using combo boxes and list boxes

Access has two types of controls—list boxes and combo boxes—for showing lists of data from which a user can select. The list box always displays as much of the list as possible, whereas the combo box has to be clicked to open the list. A combo box is a combination of a text box and a list box. The text box portion of a combo box is always visible, and the user can enter text into it just like any other text box. The user can also click the drop-down arrow to display the list box portion of the combo box and select an item rather than typing it.