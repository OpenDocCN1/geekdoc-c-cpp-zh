(continued)

| CONTROL | DESCRIPTION |
|---|---|
| RibbonComboBox | A combo box (combined text entry with drop-down list of items). Use the Items property for items, the Text property for the entered text, and the TextChanged event to respond to changed. |
| RibbonDropDown | A container that can contain RibbonDropDownItem and RibbonButton items, in Items and Buttons properties respectively. The buttons and items are formatted into a drop-down list. You use the SelectionChanged event to respond to interaction. |
| RibbonEditBox | A text box that users can use to enter or edit text in the Text property. This control has a TextChanged event. |
| RibbonGallery | As with RibbonDropDown, this control can contain RibbonDropDownItem and RibbonButton items, in Items and Buttons properties respectively. This control uses Click and ButtonClick events rather than the SelectionChanged event that RibbonDropDown has. |
| RibbonLabel | Simple text display, set with the Label property. |
| RibbonMenu | A pop-up menu that you can populate with other controls, such as RibbonButton and nested RibbonMenu controls, when it is open in design view. Handle events for the items on the menu. |
| RibbonSeparator | A simple separator used to customize control layout in groups. |
| RibbonSplitButton | Control that combines a RibbonButton or RibbonToggleButton with a RibbonMenu. Set the button style with ButtonType, which can be RibbonButtonType.Button or RibbonButtonType.ToggleButton. Use the Click event for the main button or individual button Click events in the menu to respond to interaction. |
| RibbonToggleButton | A button that can be in a selected or unselected state, as indicated by the Checked property. This control also has a Click event. |

You can also set the DialogBoxLauncher property of a group so that an icon appears in the bottom right of the group. You can use this to display a dialog box as its name suggests, or to open a task pane, or to perform any other action you want. You add or remove this icon through the GroupView Tasks menu, as shown in Figure 49-9, which also shows some of the other controls in the previous table as they appear on a ribbon in design view.

![](bbox=[0.13, 0.9, 0.75, 0.96])

FIGURE 49-9

To set the image for a control, for example a RibbonButton control, you can either set the Image property to a custom image and ImageName to a name for the image (so that you can optimize image loading in an OfficeRibbon.LoadImage event handler), or you can use one of the built-in Office images. To do this, you set the OfficeImageId property to the ID of the image.