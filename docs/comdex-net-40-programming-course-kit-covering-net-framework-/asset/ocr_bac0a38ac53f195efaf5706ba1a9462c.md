+   11. *Double-click* the **Button2** button in **Form1** and *add* the following highlighted code snippet to Code Editor:

```
Private Sub Button2_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button2.Click
    Form2.Show()
End Sub
```

+   12. *Add* one Button control, **Button1**, to **Form2**, as shown in Fig.VB-2.41:

![](bbox=[0.352, 0.234, 0.672, 0.414])

Fig.VB-2.41

+   13. *Double-click* the **Button1** button on **Form2** and *add* the following highlighted code snippet to Code Editor:

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    Me.Hide()
End Sub
```

+   14. Press the F5 key on the keyboard to run the application. As a result, the output is displayed (Fig.VB-2.42).
+   
+   In Fig.VB-2.42, you see that **Button1** button is visible and **Button2** button is not visible. This is due to the fact that **Button2** button is made hidden by setting its **Visible** property to False.

+   15. Click the **Button1** button on **Form1** (Fig.VB-2.42). As a result, **Button1** disappears and **Button2** appears on **Form1** (Fig.VB-2.43).

+   16. Click the **Button2** button on **Form1** (Fig.VB-2.43).
+   
+   As a result, **Form2** is displayed (Fig.VB-2.44).

+   17. Click the **Button1** button on **Form2**, as shown in Fig.VB-2.44:

![](bbox=[0.265, 0.642, 0.412, 0.755])

Fig.VB-2.42

![](bbox=[0.441, 0.642, 0.589, 0.755])

Fig.VB-2.43

![](bbox=[0.612, 0.642, 0.759, 0.755])

Fig.VB-2.44

As a result, **Form2** disappears. In this way, controls and forms can be displayed and hidden in an application.

# Resizing and Moving Forms and Controls at Run Time

You can resize or move forms or controls by using their **Size** or **Location** property, respectively. The form or control can also be resized and moved by calling its **SetBounds** method.