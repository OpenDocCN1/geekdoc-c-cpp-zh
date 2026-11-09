+   1. *Start* Visual Studio 2010.
+   2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box opens.
+   3. *Select* **Visual Basic→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
+   4. *Select* **Windows Forms Application** in the middle pane to create a Windows Forms application.
+   5. *Enter* the name of the application as **GroupingOperator** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
+   6. *Click* the **OK** button to close the **New Project** dialog box and the **GroupingOperator** application is created (Fig.VB-7.21).
+   7. *Drag and drop* a **Label** control, a **ListBox** control, and a **Button** control on the form from the **Toolbox** (Fig.VB-7.21).
+   8. *Set* the **Text** properties of the **Label** and **Button** controls to **List of words:** and **Group Data**, respectively, as shown in Fig.VB-7.21.

![](bbox=[0.335, 0.342, 0.688, 0.544])

Fig.VB-7.21

+   9. *Double-click* the form to create the event handler for its **Load** event and add the highlighted code snippet shown in Listing 7.14 to Code Editor:

# **Listing 7.14:** Handling the Load Event of the Form

```
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
    Dim words() As String = {"apple", "banana", "cherry", "pineapple",
    "apricot", "papaya",
    "blueberry", "abacus", "parrot", "black"}
    For Each w In words
        ListBox1.Items.Add(w.ToString())
    Next
End Sub
```

Listing 7.14 shows the code for the event handler of the **Load** event of **Form1**. In the highlighted code snippet, we first declare an array of **String** type, words, and initialize the array with a set of words. Then, we add the elements of the words array to the **Items** collection of the **ListBox1** control present on the form, by using a **For Each** loop.

+   10. *Double-click* the **Group Data** button in the form to create the event handler for its **Click** event and add the highlighted code snippet shown in Listing 7.15 to Code Editor:

# **Listing 7.15:** Handling the Click Event of the Button1

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
System.EventArgs) Handles Button1.Click
    Dim words(9) As String
    For index = 0 To 9
        words(index) = ListBox1.Items(index)
```