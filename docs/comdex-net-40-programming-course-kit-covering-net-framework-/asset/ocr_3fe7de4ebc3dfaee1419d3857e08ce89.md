writing the class definition. Such classes have no name and are, therefore, called anonymous types. Anonymous types enable you to select any combination of available fields in a query and in any order, without defining a named data type for any element.
The compiler constructs an anonymous types dynamically and assigns a name to it. The name changes each time you build an application and therefore, the name of an anonymous type cannot be used directly in the application.

Anonymous types in LINQ are used in query expressions to combine the columns of data selected by a query. They enable you to write a query that selects any number of columns and in any order.
Perform the following steps to use anonymous types in a LINQ query:

+   1. *Start Visual Studio 2010.*
+   2. *Select* **File→New→Project** *from the menu bar. The* **New Project** *dialog box opens.*
+   3. *Select* **Visual Basic→Windows** *from the* **Installed Templates** *section in the left pane of the* **New Project** *dialog box.*
+   4. *Select* **Windows Forms Application** *in the middle pane to create a Windows Forms application.*
+   5. *Enter the name of the application as* **AnonymousTypes** *(also available on the CD) in the* **Name** *text box and an appropriate location for the application in the* **Location** *combo box.*
+   6. *Click the* **OK** *button to close the* **New Project** *dialog box. The* **AnonymousTypes** *application is created (Fig.VB-7.44).* 
+   7. *Drag and drop a* **ListView** *control on the form from the* **Toolbox** *(Fig.VB-7.44).* 
+   8. *Open the* **Smart Tag** *of the* **ListView** *control by selecting this control in the form and clicking the right arrow button at the top right corner of the control, (Fig.VB-7.44).* 
+   9. *Click the down arrow button of the* **View** *drop-down list in the Smart Tag of the* **ListView** *control and select the* **Tile** *option from the drop down menu, (Fig.VB-7-44).* 
+   10. *Click the* **Dock in Parent Container** *link in the Smart Tag of the* **ListView** *control to dock the* **ListView** *control in its parent container (form), (Fig.VB-7.45).*

![](bbox=[0.182, 0.518, 0.503, 0.714])

![](bbox=[0.52, 0.518, 0.841, 0.714])

+   11. *Double-click* the form in the designer to open Code Editor and *add* the highlighted code snippet shown in Listing 7.21 to Code Editor.

# **Listing 7.21:** Showing the Use of an Anonymous Type in a LINQ Query

```
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
    Dim words As String() = {"APPLE", "BlAckBeRrY", "baNaNa", "oRange", "Mango", "StrawBeRrY"}
    Dim lWords = From w In words Select New With {Key .Upper = w.ToUpper()}
        Key .Lower = w.ToLower()
    For Each w In lWords
        ListView1.Items.Add(w.Upper & " <--> " & w.Lower)
```