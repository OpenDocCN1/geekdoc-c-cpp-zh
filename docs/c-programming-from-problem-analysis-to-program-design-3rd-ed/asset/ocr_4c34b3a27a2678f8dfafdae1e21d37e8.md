The first statement in the menuFont_Click( ) method retrieves the current Font setting from the Label object's Font property. This value is shown as the selected option when the dialog box is displayed. The first statement in the menuColor_Click( ) method retrieves the current ForeColor property setting for the Label object. Again, this value is used when the Color dialog box is displayed. For this example, the Color dialog box originally has a box around the yellow color, which is the value set as the ForeColor on the Form property. The If statement in Example 10-19 is checking to make sure the Cancel button has not been clicked. If it has been clicked, no change is made; otherwise, the Font and ForeColor are set to the selections made by the user.

Launching the program and selecting the Color menu option, after changing the Font, displays a window, as shown in Figure 10-14. Clicking on the pink color changes the ForeColor for the Label to that selection.

![](bbox=[0.177, 0.475, 0.634, 0.691])

Figure 10-14   Color dialog box menu option

The Font dialog box displayed from the Format menu in the Gardening Guide is shown in Figure 10-15. It contains the styles, sizes, effects, and a sample output window for viewing. Notice that Informal Roman, Bold Italic, 28 point, and underline effects were all chosen. The Label object containing the text “Add water!” is changed to reflect these selections.