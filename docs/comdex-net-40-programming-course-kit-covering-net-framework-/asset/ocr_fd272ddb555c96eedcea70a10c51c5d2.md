![](bbox=[0.2447, 0.1364, 0.5, 0.2673])

![](bbox=[0.5235, 0.1364, 0.7788, 0.2673])

Fig.VB-4.31 shows the **StatusStrip1** control in the form after adding items to it:

![](bbox=[0.3412, 0.3109, 0.6824, 0.5273])

+   26. *Double-click* the **TextBox** control in the form and add the highlighted lines of code, as shown in Listing 4.3, to the Code Editor:

# Listing 4.3: Showing the Code for the TextBox1_TextChanged Event Handler

```
Private Sub TextBox1_TextChanged(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles TextBox1.TextChanged
        Dim str() As String = TextBox1.Text.Split(" "c, ControlChars.NewLine)
        ToolStripStatusLabel1.Text = ("Words: " & str.Length & ", " &
        "Characters (with spaces): " & TextBox1.TextLength)
    End Sub
```

Listing 4.3 shows the code for the event handler of the TextChanged event of the TextBox control. This event handler executes when text is entered or changed in the text box at runtime. In the highlighted lines, we have declared an array of String type, named str, which stores words that are delimited by a whitespace or new line from the text entered in the text box. The number of words (number of elements in the str array) and number of characters entered in the text box are displayed in the ToolStripStatusLabel control.

+   27. *Double-click* the **StatusStrip** control in the form and add the highlighted line of code, as shown in Listing 4.4, to the Code Editor:

# Listing 4.4: Showing the Code to Handle the ItemClicked Event of the StatusStrip Control

```
Private Sub StatusStrip1_ItemClicked(ByVal sender As System.Object, ByVal e As
System.Windows.Forms.ToolStripItemClickedEventArgs) Handles StatusStrip1.ItemClicked
    MessageBox.Show("Item clicked: " & e.ClickedItem.Name)
End Sub
```