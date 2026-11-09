+   7. Click the OK button (Fig.VS-2.41). The **FirstWindowsFormsApplication** application is created, as shown in Fig.VS-2.42:

![](bbox=[0.334, 0.172, 0.688, 0.356])

Fig.VS-2.42

In Fig.VS-2.42, you see that the application has a rectangular area with **Form1** displayed on the upper-left corner. The Minimize, Maximize, and Close buttons are displayed on the upper-right corner of **Form1**. This rectangular area is the form where you design the UI for the application.

> > You learn more about Windows Forms in Chapter 2, Windows Forms, of Visual Basic 2010 section.

+   8. Double-click the form in the designer. The **Form1.vb** file opens in code editor, as shown in Fig.VS-2.43:

![](bbox=[0.334, 0.5, 0.688, 0.648])

Fig.VS-2.43

+   9. Type the highlighted line of code shown in Listing 2.2 in code editor:

```
**Listing 2.2:** Showing the Code to Display a Message Box

```vb
Public Class Form1
    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
        MessageBox.Show("First Windows Forms Application")
    End Sub
End Class
```
```

In Listing 2.2, the **Form1** class represents the Form1 form of the application. Any functionality that you want to add to **Form1** needs to be added in the **Form1** class. You see that the **Show** method of the **MessageBox** class is accessed in the **Form1_Load** method, which is the event handler for the Load event of the **Form1** form. The Show method displays the message, First Windows Forms Application, when **Form1** is loaded at run time.