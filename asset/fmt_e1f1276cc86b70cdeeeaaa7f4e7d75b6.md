
![](img/d99870e80390742f93963da7be0b2e61_618_0.png)

图16-3

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

The second method in the preceding block of code is the actual `OnEHSizeChange` method. Note that this method has three parameters:

- The first is the actual object that has been changed.
- The second is the name of the property, so multiple properties could call the same delegate in your Windows Forms code.
- The third is the new value of that property.

For the purposes of this demonstration, because this method will only be called for a single property on a single object, and because the new value will already be assigned within the control, the only thing this method needs to do is call the same `ApplyMask` method that is called elsewhere to correctly apply the mask to the image.

Save, build, and run your example code again and notice how the mapping of the property has enabled your form to detect when a property on control `ElementHost1`, or potentially even on one of the WPF controls within your `ElementHost` control, has changed. As an exercise, consider changing this example to detect when the image hosted in control `Image1` changes.

This example illustrates how you can create a new WPF component that can be incorporated into an existing Windows Forms application. You can start the process of migrating your application to WPF while still focusing the majority of your available resources on adding new capabilities to your existing application. Migration in this context means you are not forced to spend the majority of your cycles rewriting your entire existing interface. Instead, you can integrate these two display methodologies. The preceding example demonstrates one way of working with a WPF control within a Windows Forms application.

Other methods for carrying out the same tasks, including adding WPF controls within the context of the same project, are also possible. However, defining WPF controls within a Windows Forms project reduces your ability to migrate your control into a larger WPF model. Using the method demonstrated in this chapter makes that transition easy, as you’ll just be hosting Windows Forms controls in WPF.

### HOSTING WINDOWS FORMS CONTROLS IN WPF

In the case of WPF hosting Windows Forms controls, you might choose to do this if you have an existing application that relies on certain controls that have not yet been implemented in WPF. For example, the following table lists some of the controls that are not directly supported in WPF:

| `BindingNavigator` | `DataGridView` | `DateTimePicker` |
| `ErrorProvider` | `HelpProvider` | `ImageList` |
| `LinkLabel` | `MaskedTextBox` | `MonthCalendar` |
| `NotifyIcon` | `PrintDocument` | `PropertyGrid` |

In addition to these controls that aren’t directly supported, still other controls may behave differently in this release. For example, the `ComboBox` control in WPF doesn’t provide built-in support for autocomplete. In other cases, such as the `HelpProvider` (F1 Help), a control isn’t supported because WPF provides an alternative implementation. Even if you have an application in which the existing user interface takes advantage of one of the preceding control’s features, it is understandable that you might be interested in integrating your existing investment in the next version of your application.

However, there is a real possibility that if you have heavily leveraged a `DataGridView` control, you will want to reuse your existing control, rather than attempt to design a custom replacement.

To walk through the process of using the `WindowsFormsHost` control, create a new WPF Application called `ProVB_WPFInterop`; a copy of the completed project is available with this name as part of the code download. Once you have done that, select `File Add` to add a second project to this solution. This time, pick a Windows Control Library and give it the name `WinFormInteropCtrl`. Again, Visual Studio will execute the template to create a new project. At this point you will have access to a new control called `UserControl1`. Go to the designer for this new user control and add a `Button` control and a `DataGridView` control to the design surface, as shown in Figure 16-4.

![](img/d99870e80390742f93963da7be0b2e61_620_0.png)

FIGURE 16-4

Figure 16-4 shows one way to arrange these controls. For the purposes of this demonstration, the `Button` control is static; it is there to demonstrate a formatting issue. Next, manually add the two columns shown in the grid through Visual Studio 2010. You can do this using the context menu available in the upper-right corner of the control’s display. Simply select `Add Column` for each of the two columns, calling the first `File Path` and the second `Size`. The first column will wind up holding lengthy string values representing the available images, so ensure you add a decent default length to this column. This control represents a complex grid but it is not meant to be one. Resize the grid to fit within the display area of your user control. This demonstration focuses on display characteristics, so there is no need to edit the default code-behind or provide an action for the click event of the button.

After you have created a new `UserControl1`, build the project so that the `WinFormInteropCtrl` has been compiled and then close this window. The next step is to update your WPF project with the appropriate references. Three references need to be added. From the Project Settings window, select the References tab. Add references to the .NET assemblies `System.Windows.Forms` and `WindowsFormsIntegration`. Finally, add a reference to the `WinFormInteropCtrl` project. After adding these three references, close the Project Settings window and recompile the project.

Having created a new user control and added the references, open the `MainWindow.xaml` file that’s created with this template. In that XAML file you’ll see the `Window` declaration. This declaration in Visual Studio imports a few namespaces, as discussed in Chapter 17. You’ll want to change the title attribute of the window in XAML to reflect the new form title, Pro VB WPF Interop.

Next, switch to Design view and add a button to the upper-left corner of the display. This button will illustrate two concepts. First, just like the Windows Forms example, where the code leveraged some of the WPF classes outside the context of the interop form, this WPF form is going to leverage the same `FolderBrowseDialog` that was used in the preceding Windows form. Second, it will help show that although WPF and Windows Forms share the same control, a button, the default display of that control is very different, a problem that can be corrected. Label this button “Select Folder.” Note technically the text shown on the button is part of the `content` property. In this case you can implicitly reference that property by putting the desired text directly into the XAML between the open and close tags of the buttons.

Next, add a second button to the upper-right corner of the display. Align the buttons, label this as a Close button. Next, drag and drop a `WindowsFormsHost` control onto the display. The control should be docked to the bottom bounds of the display below the two buttons.

Unlike the Windows Forms project earlier in this chapter, the WPF design surface currently does not support adding your custom user control to this display. At this point you can review the XAML view within Visual Studio to compare your XAML to the XAML shown in the following listing. Your overall display should look similar to Figure 16-5.

```
<Window x:Class="MainWindow"
```
