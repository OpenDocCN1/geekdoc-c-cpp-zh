
Perform the following steps to resize and move forms and controls:

- 1. *Start Visual Studio 2010.*
- 2. *Select* **File→New→Project** *from the menu bar. The **New Project** dialog box opens.*
- 3. *Select* **Visual Basic→Windows** *from the Installed Templates section in the left pane of the New Project dialog box.*
- 4. *Select* **Windows Forms Application** *in the middle pane to create a Windows Forms application.*
- 5. *Enter the name of the application as* **RESIZEMOVE** *(also available on the CD) in the* **Name** *text box and an appropriate location for the application in the* **Location** *combo box.*
- 6. *Click the* **OK** *button to close the* **New Project** *dialog box. The* **RESIZEMOVE** *application is created, (Fig.VB-2.45)*
- 7. *Add a* **Button** *control to the form from the Toolbox, (Fig.VB-2.46)*

![](img/9862a98a1a2d3bb14334137965a1ec60_103_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_103_1.png)

Fig.VB-2.45

Fig.VB-2.46

- 8. *Double-click* the **Button1** control on **Form1** *and add the highlighted code snippet shown in Listing 2.5 to Code Editor.*

## Listing 2.5: Resizing and Moving Forms and Controls

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
        Size = New Size(200, 300)
        Location = New Point(0, 0)
        Button1.Size = New Size(80, 60)
        Button1.Location = New Point(0, 0)
End Sub
```

In Listing 2.5, you set the **Size** and **Location** properties of **Form1** and **Button1** inside the Click event handler of **Button1**. Next, create a new **Size** object with width as 200 and height as 300. After that, assign this new **Size** object to the **Size** property of the form. Moreover, create a new **Point** object with both X and Y coordinate values as 0 and assign this new **Point** object to the **Location** property of the form. Finally, set the **Size** and **Location** properties of the **Button1** button in the same way as you set the properties of the form.

- 9. *Press the F5 key on the keyboard to run the application. The output is displayed (Fig.VB-2.47).*
- 10. *Click the* **Button1** *button (Fig.VB-2.47). As a result, the size and location of the button and form changes, as shown in Fig.VB-2.48.*

![](img/9862a98a1a2d3bb14334137965a1ec60_103_2.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_103_3.png)

Fig.VB-2.47

Fig.VB-2.48

In this section, you learned about the different operations that you can perform on forms in a Windows Forms application. Let’s now move ahead and learn how to create message boxes.

## Creating Message Boxes

A message box is a kind of form that is used to display a message to the user at run time. Visual Basic 2010 provides you the following two ways to create a message box:

- Using the **MsgBox** function
- Using the **MessageBox.Show** function

Let’s learn how to use each of these functions to create a message box, one by one.

## Using the MsgBox Function

The MsgBox function allows you to display a message box when you run a Windows Forms application. The syntax of the MsgBox function is as follows:

```vb
Public Function MsgBox(Prompt As Object,
    [Buttons As Microsoft.VisualBasic.MsgBoxStyle = MsgBoxStyle.DefaultButton1],
    [Title As Object=Nothing]) As Microsoft.VisualBasic.MsgBoxResult
```

The parameters in the preceding syntax are:

- **Prompt:** Represents a string expression that is displayed as a message in the message box. The maximum length of the string expression is 1024 characters.
- **Buttons:** Represents a set of values specifying the number and type of buttons to display, the icon style to use, the identity of the default button, and the modality of the message box. The default value for the Buttons argument is zero.
- **Title:** Represents a string expression that is displayed in the title bar of the message box. If the title is not specified, then the application name is placed in the title bar.

Table 2.5 shows the possible constants that can be used for the **Buttons** argument with the **MsgBox** function:

| Constant | Value | Description |
|---|---:|---|
| OKOnly | 0 | Displays the OK button only |
| OKCancel | 1 | Displays the OK and Cancel buttons |
| AbortRetryIgnore | 2 | Displays the Abort, Retry, and Ignore buttons |
| YesNoCancel | 3 | Displays the Yes, No, and Cancel buttons |
| YesNo | 4 | Displays the Yes and No buttons |
| RetryCancel | 5 | Displays the Retry and Cancel buttons |
| Critical | 16 | Displays the critical message icon |
| Question | 32 | Displays a warning message in the form of a question |
| Exclamation | 48 | Displays the warning message icon |
| Information | 64 | Displays the information message icon |
| DefaultButton1 | 0 | The First button is default |
| DefaultButton2 | 256 | The second button is default |
| DefaultButton3 | 512 | The third button is default |
| ApplicationModal | 0 | Requires that the user respond to the message box before continuing work in the current application |
| SystemModal | 4096 | Makes all applications unavailable until the user dismisses the message box |
| MsgBoxSetForeground | 65536 | Specifies the message box window as the foreground window |
| MsgBoxRight | 524288 | Ensures that the text is right-aligned |
| MsgBoxRtlReading | 1048576 | Specifies that the text should appear right-to-left on Right to Left (RTL) systems such as Hebrew and Arabic |

The **MsgBox** function returns a value from the **MsgBoxResult** enumeration. The values in the **MsgBoxResult** enumeration indicate which button in the message box the user has clicked. The members of the **MsgBoxResult** enumeration are as follows:

- OK
- Cancel
- Abort
- Retry
- Ignore
- Yes
- No

Perform the following steps to create a message box by using the **MsgBox** function:

- 1. *Start* **Visual Studio 2010**.
- 2. *Select* **File**➤**New**➤**Project** from the menu bar. The **New Project** dialog box opens.
- 3. *Select* **Visual Basic**➤**Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Windows Forms Application** in the middle pane to create a Windows Forms application.
- 5. *Enter* the name of the application as **MSGAPPLICATION** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
- 6. *Click* the **OK** button to close the **New Project** dialog box. The **MSGAPPLICATION** application is created (Fig.VB-2.49).
- 7. *Add* a **Button** control and a **TextBox** control to the form from the **Toolbox** and resize them, as shown in Fig.VB-2.50:

![](img/9862a98a1a2d3bb14334137965a1ec60_105_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_105_1.png)

- 8. *Select* the **Button** control in the form and *set* its **Text** property to **Show Message Box** in the **Properties** window, as shown in Fig.VB-2.51:

![](img/9862a98a1a2d3bb14334137965a1ec60_106_0.png)

Fig.VB-2.51

- 9. **Double-click** the **Button** control in the form and add the highlighted code snippet shown in Listing 2.6 to Code Editor:

## Listing 2.6: Using the MsgBox Function

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    Dim Result As Integer
    Result = MsgBox("This is a message box!", MsgBoxStyle.OkCancel +
    MsgBoxStyle.Information + MsgBoxStyle.SystemModal, "Message Box")
    If (Result = MsgBoxResult.Ok) Then
        TextBox1.Text = "You have clicked OK"
    End If
End Sub
```

In Listing 2.6, you create a message box and store the result of the selection in an **Integer** variable named, **Result**. If the user clicks the **OK** button at run time, the text **You have clicked OK** is added to the text box present on the form.

- 10. Press the F5 key on the keyboard to run the application. As a result, the output is displayed (Fig.VB-2.52).
- 11. Click the **Show Message Box** button (Fig.VB-2.52). A message box displaying the message, **This is a message box!**, appears (Fig.VB-2.53).
- 12. Click the **OK** button in the message box (Fig.VB-2.53). As a result, the text, **You have clicked OK**, appears in the text box present on the form, as shown in Fig.VB-2.54:

![](img/9862a98a1a2d3bb14334137965a1ec60_106_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_106_2.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_106_3.png)

Fig.VB-2.52

Fig.VB-2.53

Fig.VB-2.54

## Using the MessageBox.Show Function

Similar to the MsgBox function, the MessageBox.Show function also allows you to display a message box when you run a Windows Forms application. The syntax of the MessageBox.Show function is as follows:

```vb
Public Shared Function Show (
    text As String, …
```
