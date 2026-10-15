# HelpProvider

The HelpProvider enables controls to have associated context-sensitive help available by pressing F1. When a HelpProvider is added to a form, all controls on the form get the new properties shown in Table 14-3, which show up in the controls’ Properties window.

# TABLE 14-3: Properties of the HelpProvider Component

| PROPERTY | USAGE |
|---|---|
| HelpString on HelpProvider1 | Provides a pop-up ToolTip for the control when F1 is pressed while the control has the focus. If the HelpKeyword and HelpNavigator properties (described later) are set to provide a valid reference to a help file, then the HelpString value is ignored in favor of the help file information. |
| HelpKeyword onHelpProvider1 | Provides a keyword or other index to use in a help file for context-sensitive help for this control. The HelpProvider1 control has a property that indicates which help file to use. This replaces the HelpContextID property in VB6. |
| HelpNavigator onHelpProvider1 | Contains an enumerated value that determines how the value in HelpKeyword is used to refer to the help file. There are several possible values for displaying elements such as a topic, an index, or a table of contents in the help file. |
| ShowHelp onHelpProvider1 | Determines whether the HelpProvider control is active for this control |

Filling in the HelpString property immediately causes the control to provide ToolTip help when F1 is pressed while the control has the focus. The HelpProvider control has a property to point to a help file (either an HTML help file or a Win32 help file), and the help topic in the HelpTopic property points to a topic in this file.

# ErrorProvider

The ErrorProvider component presents a simple, visual way to indicate to a user that a control on a form has an error associated with it. The added property for controls on the form when an ErrorProvider is used is called Error on ErrorProvider1 (assuming the ErrorProvider has the default name of ErrorProvider1). Setting this property to a string value causes the error icon to appear next to a control. In addition, the text appears in a ToolTip if the mouse hovers over the error icon.

Figure 14-20 shows a screen with several text boxes, one of which has an error icon next to it (with a ToolTip). The error icon and ToolTip are displayed and managed by an ErrorProvider.

The ErrorProvider component’s default icon is a red circle with an exclamation point. When the Error property for the text box is set, the icon blinks for a few moments, and hovering over the icon causes the ToolTip to appear. Writing your own code to set the Error property is explained in the section “Working with Extender Providers in Code.”

![](bbox=[0.62, 0.64, 0.88, 0.73])

# FIGURE 14-20

# Properties of Extender Providers

In addition to providing other controls with properties, extender providers also have properties of their own. For example, the ErrorProvider has a property named BlinkStyle. When it is set to NeverBlink, the blinking of the icon is stopped for all controls affected by the ErrorProvider.

Other properties of the ErrorProvider enable you to change things such as the icon used and where the icon appears in relation to the field containing the error. For instance, you might want the icon to appear on the left side of a field instead of the default right side. You can also have multiple error providers on your form. For example, you might wish to give users a warning, rather than an error. A second error provider with a yellow icon could be used for this feature.