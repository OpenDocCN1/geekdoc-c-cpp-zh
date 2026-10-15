
In order to demonstrate this in the code, return to the Design view for your form. Select the Images button and position your cursor just after the word Button, which names this node. Press the spacebar. You'll see that you have IntelliSense, indicating which properties and events are available on this control. Typing a c adjusts the IntelliSense display so that you see the click event. Select this event by pressing Tab and you'll see the display shown in Figure 17-3.

![](img/d99870e80390742f93963da7be0b2e61_635_0.png)

## FIGURE 17-3

As shown here, not only does the XAML editor support full IntelliSense for selecting properties and events on a control, when an event is selected, it displays a list of possible methods that can handle this event. Of particular note is the first item in the list, which enables you to request that a new event handler be created in your code. Selecting this item tells Visual Studio to generate the same event handler stub that you created by double-clicking on the control; however, instead of placing the Handles clause on this method, the definition of this method as an event handler is kept in the XAML.

This causes two issues. First, if you are looking only at the code, then nothing explicitly indicates whether a given method in your code is in fact an event handler. This makes maintaining the code a bit (not a lot) more difficult to maintain. Second, if you have handled an event that is specific to Windows as opposed to the Web, then your XAML won't be portable. Neither of these side effects is desirable. Thus, given the VB syntax for defining events as part of the method declaration, the code in this chapter avoids the embedded XAML style of declaring standard Windows event handlers.

At this point, you could run your application. It won't do anything except allow you to close it, but you can verify that it behaves as expected and save your work.

## Adding Behavior

It's almost time to make this UI do something, but there is one more step before you start working with code. As part of this application, you want to allow users to select the directory from which images should be displayed. In theory, you could (and in practice, at some time probably would) write a custom interface for selecting or navigating to the images directory. However, for this application that isn’t important, and you want a quick and easy solution.

Unfortunately, WPF doesn’t offer any native control that supports providing a quick and easy view into the file system. However, Windows Forms does, and in this case you want to leverage this control. The good news is that you can, and the even better news is that you don’t need the Windows interop library in order to do so. Because something like the Browse Folders dialog isn’t a control hosted on your form, you can reference it from your code. Thus, although you need the Windows Forms Integration Library and the `WindowsFormsHost` control discussed in Chapter 16 for any UI-based controls, in this case the code just needs to reference the `System.Windows.Forms` library.

Because the `System.Windows.Forms` library isn’t automatically included as a reference in a WPF application, you need to manually add a reference to this library. Keep in mind that this library isn’t going to be available to you outside of WPF’s rich client implementation. Thus, this feature is limited to WPF running on the client; for other scenarios you would change how you select an image. Open the My Project display and select the References tab. Click the Add button to open the Add Reference dialog and then select the `System.Windows.Forms` library, as shown in Figure 17-4. You can’t add controls to your WPF form without leveraging the `Windows.Forms.Integration` library, but you can, behind the scenes, continue to reference controls and features of Windows Forms.

![](img/d99870e80390742f93963da7be0b2e61_636_0.png)

FIGURE 17-4

With this additional reference, you can begin to place some code into this application. Start with the `window_loaded` event. This event is where you’ll define the default path for the image library, set up the label for the Prev button, and change the default property of the grid control so that it handles the images the way you want:

```
Private Sub MainWindow_Loaded(ByVal sender As System.Object, _
    ByVal e As System.Windows.RoutedEventArgs) _
    Handles MyBase.Loaded

' Append the << to the text for the button since these are _
' reserved characters within XAML
ButtonPrev.Content = "<< " & ButtonPrev.Content.ToString()
' Set the default path from which to load images
TextBox1.Text = _
    Environment.GetFolderPath(Environment.SpecialFolder.MyPictures)
' Have the images maintain their aspect ration
Image1.Stretch = Stretch.Uniform
End Sub
```

*Code snippet from MainWindow.vb*

The preceding implementation handles these three tasks. It takes the content of the `ButtonPrev` control and appends the two less than symbols to the front of the string so that both buttons are displayed uniformly. Of course, long term, this code is going to be disposed of, but for now it helps to illustrate that while controls such as `Button` may seem familiar from Windows Forms, these controls are in fact different. The WPF version of the `Button` control doesn’t have a `text` property; it has a `content` property. The `content` property is, in fact, an untyped object reference. In the case of this application, you know this content is a string to which you can append additional text. However, this code is neither a good idea nor easily maintained, so this is just a temporary solution.

Next, the code updates the text property of the TextBox control used on the form. This text box displays the folder for the images to display. In order to provide a dynamic path, the code leverages the Environment class to get a folder path. To this shared method the code passes a shared environment variable: Environment.SpecialFolder.MyPictures. This variable provides the path to the current user’s My Pictures folder (or the User’s Pictures folder on Windows 7 and Vista). By using this value, the code automatically points to a directory where the current user would be expected to have images.

Finally, to again demonstrate that any of the WPF classes can be modified within your code, this code sets a property on the Image control. Specifically, it updates the Stretch property of the Image control to ensure that images are resized with their aspect maintained. Thus, if an image is square, then when your image control becomes a rectangle, the image remains square. The Stretch.Uniform value indicates that the aspect should be maintained, while other members of the Windows.Stretch enumeration provide alternative behavior.

The next step is to implement your first button handler, the ButtonBrowse_Click handler. When this button is clicked, the application should open the Folder Browse dialog, displaying the currently selected folder as the default. The user should be allowed to navigate to an existing folder or create a new folder. When the dialog is closed, the application should, if the user selected a new folder, update the folder’s text box to display this new location:

```
Private Sub ButtonBrowse_Click(ByVal sender As System.Object, _
    ByVal e As System.Windows.RoutedEventArgs) _
    Handles ButtonBrowse.Click

Dim folderDialog As System.Windows.Forms.FolderBrowserDialog = _
    New System.Windows.Forms.FolderBrowserDialog()
folderDialog.Description = "Select the folder for images."
folderDialog.SelectedPath = TextBox1.Text
Dim res As System.Windows.Forms.DialogResult = _
    folderDialog.ShowDialog()

If res = System.Windows.Forms.DialogResult.OK Then
    TextBox1.Text = folderDialog.SelectedPath
End If
End Sub
```

Code snippet from MainWindow.vb

The preceding code block declares an instance of the System.Windows.Forms.FolderBrowserDialog control. As noted when the reference was added, this control isn’t part of your primary window display, so you can create an instance of this dialog without needing the Windows.Forms.Interface library. It then sets a description, indicating to users what they should do while in the dialog, and updates the current path for the dialog to reflect the currently selected folder. The dialog is then opened and the result assigned directly into the variable res. This variable is of type System.Windows.Forms.DialogResult and is checked to determine whether the user selected the OK button or the Cancel button. If OK was selected, then the currently selected folder is updated.

Now it’s time to start working with the images. That means you need to retrieve a list of images and manipulate that list as the user moves forward and backward through it. You could constantly return to the source directory to find the next and previous images, but you will get much better performance by capturing the list locally and keeping your current location in the list. This implies two local variables; and because you want these variables available across different events, you need to declare them as member variables to your class:

```
Class MainWindow
    Private m_imageList As String() = {}
    Private m_curIndex As Integer = 0
    Private Sub MainWindow_Loaded(ByVal sender As System.Object, _
        ByVal e As System.Windows.RoutedEventArgs) _
        Handles MyBase.Loaded

        ' Append the << to the text for the button since these are _
        ' reserved characters within XAML
        ButtonPrev.Content = "<< " + ButtonPrev.Content.ToString()
```
