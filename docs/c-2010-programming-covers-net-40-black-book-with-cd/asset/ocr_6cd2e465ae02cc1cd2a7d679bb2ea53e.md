![](bbox=[0.18, 0.075, 0.79, 0.395])

# Figure 16.6: Displaying the PasswordRecovery Control

# The ChangePassword Control

The ChangePassword control allows the users to change their password. This control prompts users to provide the current password first and then set the new password. If the old password is not correct, the new password cannot be set. This control also facilitates in sending e-mails to users about the new password. The ChangePassword control is provided by the ChangePassword class.

The following code snippet shows the class hierarchy of the ChangePassword class:

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
      System.Web.UI.WebControls.CompositeControl
        System.Web.UI.WebControls.ChangePassword
```

The ChangePassword class contains various methods, properties, and events.

Table 16.13 lists the noteworthy properties of the ChangePassword class:

# Table 16.13: Noteworthy Properties of the ChangePassword Class

| Property | Description |
|---|---|
| BorderPadding | Retrieves or specifies the amount of padding, in pixels, inside the border and the designated area for the ChangePassword control. |
| CancelButtonImageUrl | Retrieves or specifies the URL of an image to display with the Cancel button, if the Cancel button is configured by the CancelButtonType property to be an image button. |
| CancelButtonStyle | Retrieves a reference of style properties to define the look of the Cancel button on the ChangePassword control. |
| CancelButtonText | Retrieves or specifies the text displayed on the Cancel button. |
| CancelButtonType | Retrieves or specifies the type of button to use for the Cancel button when customizing the ChangePassword control. |
| CancelDestinationPageUrl | Retrieves or specifies the URL of the page that the user is shown after clicking the Cancel button in the ChangePassword control. |