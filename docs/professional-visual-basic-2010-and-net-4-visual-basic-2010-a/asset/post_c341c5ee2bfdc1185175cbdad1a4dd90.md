
' whether margin is set or not. if the actual size is greater than the
' size of the image reset margins to the max size of the image.
Dim imgH As Double = image.Height
Dim ctrlH As Double = Me.ActualHeight
Dim marginHorizontal As Double
If imgH > ctrlH Then
    marginHorizontal = 0
Else
    marginHorizontal = (ctrlH - imgH) / 2
End If

Dim imgW As Double = image.Width
Dim ctrlW As Double = Me.ActualWidth
Dim marginSide As Double
If imgW > ctrlW Then
    marginSide = 0
Else
    marginSide = (ctrlW - imgW) / 2
End If
Image1.Margin = New Thickness(marginSide, marginHorizontal, marginSide, marginHorizontal)

End Sub
End Class

Code snippet from UserControl1.xaml

The remaining custom code is in fact the ResizeMargins method. This method is reasonably simple. It takes the size of the image itself and compares this to the size of the control Image1. Note that this code references the ActualHeight property. Unlike the Height property, which for controls that are docked doesn’t provide a valid size, the ActualHeight property reflects the current size of the Image1 control. If the control size is larger than the original size of the image, then the code adjusts the margins to fill in around the image.

This completes the definition of your sample WPF control library, so compile your application to ensure that no errors are pending.

## The Windows Forms Application

The next step is to customize the Windows Forms application. Begin by adding the five required references that enable you to embed and manipulate this control. They are the four framework libraries — WindowsFormsIntegration, PresentationCore, PresentationFramework, and WindowsBase — and a project reference to your custom WpfInteropCtrl library. Open the project properties for your ProVBWinForm_Interop project and go to the References tab.

Choose Add References, and in the list of available .NET libraries you’ll find all four framework references available. Other presentation libraries are also available from this screen; and depending on what you intend to do in your application, you can choose to add other library references to your project as well. Finally, switch to the Project References tab and add a reference to your local project.

### Laying Out Controls on the Form

Now go to the Design mode for the Form1.vb file that was created by the Windows Forms template when you created this project. Extend the default size of the design surface with the size of your control in mind, allocating enough room to align three rows of Windows Forms controls above your custom user control.

Starting at the top, you are going to add a new Button control to the upper-left corner of the form. The label on this button will be “Select Folder”; to change this you will update the Text property on the control. Ensure the button is sized to display fully. Next, add a FolderBrowserDialog control to your window; this control doesn’t have a display element and will be shown below your form. Now add a Label control below your button and change its text property to “Image..” Once this is in place, add a ComboBox control to the right of this label. Accept the default name of ComboBox1, and using the properties for the control, select

the anchor property and add a binding to the right side of the container in addition to the default top and left bindings. This tells the control to expand as the containing form is widened.

Next, add a Label control to the right of your button, and use the text “Mask:”. To the right of the “Mask:” label, add a new combo box, ComboBox2, in the sample code. Go to the context menu for this ComboBox and select Edit Items to open the edit window. Within this screen add the three options that will make up the image mask options: No Mask, Ellipse, and Rectangle. Ensure that this control is also bound to the form’s width.

Below the image ComboBox, in a third row on your Windows Form, add a Label control with the text “Margin:” and a TextBox control with the name TextBoxMargin. Set the default value for this TextBox to 10 and limit its length to 4 characters in the properties display. Similarly, alongside this text box, add another Label control with the text “Corner Radius,” and a second TextBox control called TextBoxRounding. Set the default value for this second text box to 50.

At this point, drag and drop your UserControl1 directly onto the form surface. This is a change from Visual Studio 2008. With Visual Studio 2010, you drag the targeted WPF control onto the form and the designer automatically encapsulates the WPF control with an Element Host control. The controls then allow you to resize the Element Host to fill the available area, and then using the anchor property of the element host, anchor it to all four sides to ensure it resizes with the form.

The Design view for Form1 should look similar to the one shown in Figure 16-2. Note the expanded Properties pane. This is currently set to display/edit the properties for ElementHost1, focusing on its reference to the user control.

![](img/d99870e80390742f93963da7be0b2e61_614_0.png)

# FIGURE 16-2

### Adding Custom Code to the Form

The next step is to add some custom code to this form. The form will allow you to select a folder containing images and then display any of those images. Additionally, you will have the capability to place a mask over the image to provide a custom “frame” around the displayed image. The goal is to demonstrate not only

adding a control, but also a scenario in which you need to map one of the ElementHost’s properties within your code.

The next listing provides the basis for your customization. The first item is to hold onto the current directory path. The private value is defined on the form class, and a default path for images on Windows 7 is assigned to this property. Next, the Load event for the form is handled. Within the Load event, the code will get the list of files from the default directory and then load ComboBox1 with this list of files. It will select the first file from the list, and then ensure that no mask is selected. Finally, the sample code calls the method AddPropertyMapping. This call is currently commented on, and you will uncomment it after the reason for mapping a property is illustrated.

The next method shown in this code block is the event handler for the button’s Click event. This event handler opens a folder browsing dialog using the control FolderBrowserDialog1. It uses the current path as the default for this dialog, and if the user selects a new directory for images, it loads the new list of files into the ComboBox. Note that it doesn’t change the selected image, so a user won’t see a new image automatically displayed when the list of files is loaded. You should update Form1.vb with the code in the following snippet:

```
Public Class Form1
    ' The default directory path is native to Windows 7.
    ' On other operating systems select an appropriate directory.
    Private m_path As String = "C:\Users\Public\Pictures\Sample Pictures"
    Private Sub Form1_Load(ByVal sender As System.Object, _
                           ByVal e As System.EventArgs) _
                           Handles MyBase.Load
        For Each filename As String In System.IO.Directory.GetFiles(m_path)
            ComboBox1.Items.Add(filename)
        Next
        ComboBox1.SelectedIndex = 0
        Me.ComboBox2.SelectedIndex = 0
        'AddPropertyMapping()
    End Sub
    Private Sub Button1_Click(ByVal sender As System.Object, _
                              ByVal e As System.EventArgs) _
                              Handles Button1.Click
        FolderBrowserDialog1.SelectedPath = m_path
        If (FolderBrowserDialog1.ShowDialog() = _
            Windows.Forms.DialogResult.OK) Then
            If Not m_path = FolderBrowserDialog1.SelectedPath Then
                m_path = FolderBrowserDialog1.SelectedPath
                ComboBox1.Items.Clear()
                For Each filename As String In _
                    System.IO.Directory.GetFiles(m_path)
                    ComboBox1.Items.Add(filename)
                Next
            End If
        End If
    End Sub
    Private Sub ComboBox1_SelectedIndexChanged(_
        ByVal sender As System.Object, ByVal e As System.EventArgs) _
        Handles ComboBox1.SelectedIndexChanged
        Dim x As WpfInteropCtrl.UserControl1 = _
            CType(ElementHost1.Child, WpfInteropCtrl.UserControl1)
        x.Image = ComboBox1.SelectedItem.ToString
    End Sub
End Class
```

Code snippet from Form1

Finally, the preceding code includes the SelectedIndexChanged event handler, which is called when a user selects a new item from the list of available image files. This event handler retrieves the selected image path
