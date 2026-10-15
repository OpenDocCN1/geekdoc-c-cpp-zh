
This technique is best presented with an example. The standard ComboBox control does not have a way for users to reset to a “no selection” state. Once an item is selected, setting to that state requires code that sets the SelectedIndex to -1.

This exercise creates a ComboBox that has a button to reset the selection state back to “no selection.” That enables users to access that capability directly. Now that you have worked with several controls in the examples, rather than proceed step by step, we’ll just show the code for such a ComboBox and discuss how the code works:

```
Public Class SpecialComboBox
    Inherits ComboBox
    Dim WithEvents btnEmbeddedButton As Button
    Public Sub New()
        Me.DropDownStyle = ComboBoxStyle.DropDownList
        ' Fix up the embedded button.
        btnEmbeddedButton = New Button
        btnEmbeddedButton.Width = SystemInformation.VerticalScrollBarWidth
        btnEmbeddedButton.Top = 0
        btnEmbeddedButton.Height = Me.Height - 4
        btnEmbeddedButton.BackColor = SystemColors.Control
        btnEmbeddedButton.FlatStyle = FlatStyle.Popup
        btnEmbeddedButton.Text = "*"
        Dim fSpecial As New Font("Wingdings 3", Me.Font.Size - 1)
        btnEmbeddedButton.Font = fSpecial
        btnEmbeddedButton.Left = Me.Width - btnEmbeddedButton.Width - SystemInformation.VerticalScrollBarWidth
        Me.Controls.Add(btnEmbeddedButton)
        btnEmbeddedButton.Anchor = CType(AnchorStyles.Right Or AnchorStyles.Top Or AnchorStyles.Bottom, AnchorStyles)
        btnEmbeddedButton.BringToFront()
    End Sub

    Private Sub btnEmbeddedButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnEmbeddedButton.Click
        Me.SelectedIndex = -1
        Me.Focus
    End Sub
    Private Sub BilllysComboBox_DropDownStyleChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.DropDownStyleChanged
        If Me.DropDownStyle <> ComboBoxStyle.DropDownList Then
            Me.DropDownStyle = ComboBoxStyle.DropDownList
            Throw New InvalidOperationException("DropDownStyle must be DropDownList")
        End If
    End Sub
End Class
$$

```

Code snippet from SpecialCombo

Like the first example in the chapter, this example inherits from a built-in control. Thus, it immediately gets all the capabilities of the standard ComboBox. All you need to add is the capability to reset the selected state.

To do that, you need a button for the user to press. The class declares the button as a private object named btnEmbeddedButton. Then, in the constructor for the class, the button is instantiated, and its properties are set as necessary. The size and position of the button need to be calculated. This is done using the size of the ComboBox and a special system parameter called SystemInformation.VerticalScrollBarWidth. This parameter is chosen because it is also used to calculate the size of the button used to drop down a combo box. Thus, your new embedded button will be the same width as the button that the regular ComboBox displays for dropping down the list.

Of course, you need to display something in the new button to indicate its purpose. For simplicity, the preceding code displays a lowercase “t” using the WingDings 3 font (which all Windows systems should have installed). This causes a left-pointing triangle to appear, as shown in Figure 15-9, which is a screenshot of the control in use.

The button is then added to the Controls collection of the ComboBox. You may be surprised to learn that a ComboBox even has a Controls collection for embedded controls, but all controls in Windows Forms have one.

Finally, the Anchor property of the new button is set to maintain the position if the SpecialComboBox is resized by its consumer.

Besides the constructor, only a couple of small routines are needed. The Click event for the button must be handled, and in it the SelectedIndex must be set to -1. In addition, because this functionality is only for combo boxes with a style of DropDownList, the DropDownStyleChanged event of the ComboBox must be trapped, and the style prevented from being set to anything else.

![](img/d99870e80390742f93963da7be0b2e61_607_0.png)

## SUMMARY

This chapter discussed how to create custom controls in Windows Forms, enabling you to consolidate logic used throughout your user interfaces. The full inheritance capabilities in .NET and the classes in the Windows Forms namespace enable several options for creating controls. It is probably best to start by overriding these controls in order to learn the basics of creating properties and coordinating them with the designer, building controls and testing them, and so on. These techniques can then be extended by creating composite controls, as illustrated by the examples in this chapter.

We also discussed creating a control from scratch, using the base Control class. In the course of writing a control from scratch, it was necessary to discuss the basics of GDI+, but if you are going to do extensive work with GDI+, you need to seek out additional resources to aid in that effort.

The key concept that you should take away from this chapter is that Windows Forms controls are a great way both to package functionality that will be reused across many forms and to create more dynamic, responsive user interfaces much more quickly with much less code.

## 16

## User Controls Combining WPF and Windows Forms

### WHAT YOU WILL LEARN IN THIS CHAPTER

- The Windows Forms Integration Library
- Using WPF controls in Windows Forms
- Using Windows Forms controls in WPF
- Integration library limitations

Chapter 15 looked at advanced features of Windows Forms. One of these features goes well beyond Windows Forms: user controls. User controls are used in Windows Forms, ASP.NET, WPF, and Silverlight. The concepts around user controls reflect a best practice for encapsulating application logic within a reusable component. Within an application, smaller components that encapsulate functionality and communicate via a method such as events provide a robust architecture. This chapter acts as a bridge to the next chapter which deals with WPF and also references using a user control.

The same concept is used to provide a migration path from Windows Forms to Windows Presentation Foundation (WPF). WPF was first introduced in .NET 3.0 as Microsoft’s next-generation solution to graphical user-interface development. In terms of user interfaces, the transition to this new model will be similar in significance and paradigm shift to the shift from COM-based Visual Basic to Visual Basic .NET. The core paradigms and syntax familiar to developers of Windows applications are changing, and most of the changes are not backwardly compatible.

As a result, developers will need to transition existing application source code to a new technology paradigm. Perhaps not this year or next, but at some point the WPF paradigm will be used to update the look and feel of existing applications. How will this transition compare to the last major .NET-related transition—the one from COM? The original version of Visual Studio .NET included a tool to aid in migrating code from the COM-based world to .NET. No migration tool will be provided to transition existing user interfaces to WPF, which should be considered a good thing, considering the history of the current migration tools.

Instead, Microsoft learned the lesson that migration is both difficult and time consuming and is best done at the developer’s pace. Therefore, instead of trying to automatically process code based on a procedural paradigm to work under a declarative paradigm, the tool of choice is one that enables components built in the respective paradigms to communicate. After all, in some cases a change like this results in a complete rewrite of an application or the application UI, and the migration library will never be used.

This same interoperability paradigm is repeated in the Power Pack tools for Visual Basic, which Microsoft first released in 2006. These tools, covered in Appendix B, are similar in concept to the Interop methodology that Microsoft has chosen to follow with WPF.

Microsoft is providing libraries that enable user-interface developers to integrate these two user-interface models (WPF and Windows Forms). In the long run, Windows Forms to WPF integration will probably go the way of COM-Interop, which is to say it will be available for many years, but its limitations and ties to an older technology will reduce its influence, and eventually it will be forced into retirement with the older technology.

The focus of this chapter is how to use the Windows Forms Integration Library to best enable you to both leverage WPF with your existing code and leverage your existing code and related forms-based code with your new WPF applications. Just as with COM-Interop, the point of the integration library is to help you, the developer, transition your application from Windows Forms to WPF gradually, while working with the time and budget constraints that all developers face and potentially waiting for a control that isn’t available in WPF.

## THE INTEGRATION LIBRARY

WindowsFormsIntegration library enables WPF applications to host Windows Forms controls and vice versa. The library is contained in the WindowFormsIntegration.dll which supports the System.Windows.Forms.Integration namespace. This namespace provides the tools necessary for using WPF and Windows Forms in a single application. At the core of this namespace are the two classes ElementHost and WindowsFormsHost. These two classes provide for interoperability in the WPF and the Windows Forms environment, respectively.

The WindowsFormsIntegration.dll is located with the other .NET assemblies and is imported like any other common namespace. After you add a reference and import the namespace you’ll find the appropriate control class for your project type — ElementHost or WindowsFormsHost — in the list of tools in the Toolbox window for the designer.

Table 16-1 describes the classes and the delegate that make up the Windows.Forms.Integration namespace, a similar list is available from MSDN: http://msdn.microsoft.com/en-us/library/system.windows.forms.integration.aspx.

## TABLE 16-1: Windows.Forms.Integration Classes and Delegate

| CLASS | DESCRIPTION |
|---|---|
| ChildChangedEventArgs | This class is used when passing event arguments to the ChildChanged event. This event occurs on both the WindowsFormsHost and ElementHost classes when the content of the Child property is changed. |
| ElementHost | This is the core class for embedding WPF controls within Windows Forms. Using the Child property, you identify the top-level object (probably some type of panel) that will be hosted, and via this object define an area that will be controlled by that object. The object referenced by the host can contain other controls but the host references only this one. |
| IntegrationExceptionEventArgs | This is the base class for the Integration and Property Mapping exception classes. It provides the common implementation used by these classes. |
| LayoutExceptionEventArgs | This class enables you to return information related to a Layout error within a host class to the hosting environment, Windows Forms, or WPF. |
