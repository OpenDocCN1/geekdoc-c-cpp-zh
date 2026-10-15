```
''' <param name="propertyName"></param>
''' <param name="value"></param>
''' <remarks>A change of this property requires the form hosting this
''' control to adjust the clipping region, so the Property Mapper
''' in the Integration library is used to map an "event" handler.</remarks>
Private Sub OnEHSizeChange(ByVal h As Object, _
    ByVal propertyName As String, ByVal value As Object)
    ApplyMask()
End Sub
```

Code snippet from Form1

The second method in the preceding block of code is the actual OnEHSizeChange method. Note that this method has three parameters:

+   > The first is the actual object that has been changed.
+   > The second is the name of the property, so multiple properties could call the same delegate in your Windows Forms code.
+   > The third is the new value of that property.

For the purposes of this demonstration, because this method will only be called for a single property on a single object, and because the new value will already be assigned within the control, the only thing this method needs to do is call the same ApplyMask method that is called elsewhere to correctly apply the mask to the image.

Save, build, and run your example code again and notice how the mapping of the property has enabled your form to detect when a property on control ElementHost1, or potentially even on one of the WPF controls within your ElementHost control, has changed. As an exercise, consider changing this example to detect when the image hosted in control Image1 changes.

This example illustrates how you can create a new WPF component that can be incorporated into an existing Windows Forms application. You can start the process of migrating your application to WPF while still focusing the majority of your available resources on adding new capabilities to your existing application. Migration in this context means you are not forced to spend the majority of your cycles rewriting your entire existing interface. Instead, you can integrate these two display methodologies. The preceding example demonstrates one way of working with a WPF control within a Windows Forms application.

Other methods for carrying out the same tasks, including adding WPF controls within the context of the same project, are also possible. However, defining WPF controls within a Windows Forms project reduces your ability to migrate your control into a larger WPF model. Using the method demonstrated in this chapter makes that transition easy, as you’ll just be hosting Windows Forms controls in WPF.

# HOSTING WINDOWS FORMS CONTROLS IN WPF

In the case of WPF hosting Windows Forms controls, you might choose to do this if you have an existing application that relies on certain controls that have not yet been implemented in WPF. For example, the following table lists some of the controls that are not directly supported in WPF:

| BindingNavigator | DataGridView | DateTimePicker |
| ErrorProvider | HelpProvider | ImageList |
| LinkLabel | MaskedTextBox | MonthCalendar |
| NotifyIcon | PrintDocument | PropertyGrid |

In addition to these controls that aren’t directly supported, still other controls may behave differently in this release. For example, the ComboBox control in WPF doesn’t provide built-in support for autocomplete. In other cases, such as the HelpProvider (F1 Help), a control isn’t supported because WPF provides an alternative implementation. Even if you have an application in which the existing user interface takes