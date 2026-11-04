The first method (select a tool and then click and drag to create a control) is probably used most often, but some of the other methods are particularly useful for creating groups of similar controls.

For example, the form in Figure 2-1 displays five rows, each of which holds a Label and a TextBox. You could easily build all of these controls individually, but you can build them even faster by using copy and paste. First place one Label and TextBox on the form, arrange them next to each other, and give them any property values that you want all of the Labels or TextBoxes to share. (For example, you may want to set their fonts or colors.) Now click and drag to select both controls, copy and paste, and drag the new controls into position. Repeat this three more times and you'll have all of the controls in position. You'll still need to change the Labels' text but the basic arrangement will be done without going back and forth to the Toolbox.

![](bbox=[0.626, 0.136, 0.913, 0.282])

# ## SETTING CONTROL PROPERTIES

After you've added controls to a form, you can use the Properties window to view and change their property values. If you have more than one control selected, the Properties window shows only the properties that the controls have in common.

For example, if you select a TextBox and a Label, the Properties window shows the Text property because both Labels and TextBoxes have a Text property. However, it won't display the Multiline property because the TextBox control has that property but the Label control does not.

The Properties window provides special support for many control properties. For example, Figure 2-2 shows the Properties window when a TextBox is selected.

![](bbox=[0.09, 0.54, 0.395, 0.827])

Notice that the Font property contains its own sub-properties: Name, Size, Unit, Bold, and so forth. Click the plus or minus sign next to a property to expand or collapse it and show or hide its sub-properties.