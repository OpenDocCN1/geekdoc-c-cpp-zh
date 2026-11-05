![](bbox=[0.174, 0.096, 0.237, 0.146])

A number of Form properties were set. These properties were set when the Form object was initially created. The Name, BackColor, ForeColor, Text, Font, and Size properties should almost always be set.

# GroupBox Objects

CheckBox objects can be grouped together using the GroupBox control. This is beneficial for visual appearance. It also helps during design because you can move or set properties that impact the entire group. However, it does not provide any additional functionality for CheckBox objects.

A GroupBox control should be placed on the form before you add the RadioButton objects to it. If you add the RadioButton objects first and then try to add the GroupBox control on top of the RadioButton objects, it does not work as smoothly. If you add the GroupBox control last, you need to physically drag the RadioButton objects onto the top of the GroupBox control.

![](bbox=[0.174, 0.394, 0.237, 0.444])

Do not forget about the useful tools on the Format menu. The Align, Make Same Size, Horizontal Spacing, Vertical Spacing, and Center in Form tools save you hours of time. Remember, it does not matter what your interface looks like!

# RadioButton Objects

There are differences between the RadioButton and CheckBox objects, other than their visual representation. RadioButton controls appear as small circles on the Form object. They are used to give users a choice between two or more options. Remember that it is appropriate to select more than one CheckBox object. This is not the case with RadioButton objects. Normally, you group RadioButton objects by placing them on a Panel or GroupBox control. If a radio button is clicked, it is selected and all other radio buttons within the group box are deselected.

# Adding RadioButton Objects

To build on the application developed in the previous section containing the CheckBox objects, a GroupBox control is placed on the form. It should be placed there before adding objects to the group. GroupBox control objects provide an identifiable grouping for other controls. After it is dragged onto the form, a GroupBox control object must usually be resized. Using Visual Studio, you can drag three RadioButton objects on top of the GroupBox.

![](bbox=[0.174, 0.815, 0.237, 0.865])

After the RadioButton objects are placed on the GroupBox, you can set properties of the GroupBox and impact all members of the group. Want to make them invisible? Set the Visible property of the GroupBox. It is not necessary to set all of the members. If you want to change the font color of all radio buttons, just change the GroupBox Font property.