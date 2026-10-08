# 14.6 GroupBoxes and Panels 603

We set displayButton's Text property to "Show Me" and clear the Text of displayPasswordLabel so that it's clear when the program begins executing. The Border of displayPasswordLabel is set to Fixed3D, giving our Label a three-dimensional appearance. We also changed its Align property to MiddleLeft so that the Label's text is centered between its top and bottom. The password character for inputPasswordField is determined by the user's system settings when you use-SystemPasswordChar to create.

We create an event handler for displayButton by double clicking this control in Design mode. We added line 23 to the event handler's body. When the user clicks the Show Me Button in the caption, line 23 displays the text entered by the user in inputTextBox and displays the text in displayPasswordLabel.

# 14.6 GroupBoxes and Panels

GroupBox and Panel arrange controls on a GUI. GroupBoxes and Panels are typically used to group controls of similar functionality or several controls that are related in a GUI. All of the controls in a GroupBox or Panel move when the GroupBox or Panel is moved. Furthermore, GroupBoxes and Panels can also be used to show or hide a set of controls at once. When you toggle a container's Visible property, it toggles the visibility of all the controls within it.

The difference between these two controls is that GroupBoxes can display a caption (i.e., text) and not include scrollbars, whereas Panels can include scrollbars and not include a caption. GroupBoxes have thin borders by default; Panels can be set so that they also have borders by changing their BorderStyle property. Figures 14.21–14.22 list the common properties of GroupBoxes and Panels, respectively.

# Look-and-Feel Observation 14.2

Panels and GroupBoxes can contain other Panels and GroupBoxes for more complex layouts.

![](bbox=[0.14, 0.553, 0.215, 0.626])

| GroupBox properties | Description |
|---|---||
| Controls | The set of controls that the GroupBox contains. |
| Text | Specifies the caption text displayed at the top of the GroupBox. |

**Fig. 14.21 | [GroupBox properties.](GroupBox properties.)

| Panel properties | Description |
|---|---||
| AutoScroll | Indicates whether scrollbars appear when the Panel is too small to display all of its controls. The default value is false. |
| Border | Sets the border of the Panel. The default value is None; other options are Fixed3D and FixedSingle. |
| Controls | The set of controls that the Panel contains. |

**Fig. 14.22 | [Panel properties.](Panel properties.)