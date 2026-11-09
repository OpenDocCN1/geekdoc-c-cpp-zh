```
```xml
<sdk:TreeViewItem Header="Ruby" FontFamily="Courier New"
                 FontSize="10" Foreground="MidnightBlue">
</sdk:TreeViewItem>
</sdk:TreeViewItem>
</sdk:TreeViewItem>
</sdk:TreeViewItem>
</Grid>
</UserControl>
```
```

+   12. Press **F5** to run the **SilverlightTreeView** application. The output appears, (Fig.ASP-11.28).
+   13. Click the triangular glyph on the left side of the root node, Programming Languages, to expand it and view its child nodes. The output after expanding the root node appears, (Fig.ASP-11.29).

![](bbox=[0.187, 0.299, 0.499, 0.494])

![](bbox=[0.528, 0.299, 0.835, 0.494])

As you can see in Fig.ASP-11.29, the root node of the TreeView control displays its child nodes. You can further expand the child nodes to view their child nodes.

# Using the RichTextBox control

The RichTextBox control is one of the new controls in Silverlight 4.0. It is similar to the simple TextBox control that enables you to display the rich content including the formatted text, paragraphs, inline images, and hyperlinks. You can also edit the content of this control dynamically. You can change the font-size, weight, and color of a particular text. To edit the small chunk of text in the RichTextBox control, you can use the Run element, which is derived from the Inline element.

Perform the following steps to use the RichTextBox control in your application:

+   1. *Open* **Microsoft Visual Studio 2010 IDE** and select **File→New→Project**. The New Project dialog box appears.
+   2. *Select* **Visual C#→Silverlight** from the **Installed Templates** pane in the New Project dialog box.
+   3. *Select* **Silverlight Application** from the middle pane.
+   4. *Specify* the name of the application as **RichTextBoxExample** (also available on CD) in the Name text box and the appropriate location in the Location combo box.
+   5. *Click* the **OK** button. The **New Silverlight Application** dialog box appears.
+   6. *Select* the Host the Silverlight application in a new Web site check box.
+   7. *Select* the **ASP.NET Web Application Project option** from the **New Web project type** drop down box.
+   8. *Select* **Silverlight 4** from the **Silverlight Version** drop down box.
+   9. *Select* the **Enable WCF RIA Services** check box.