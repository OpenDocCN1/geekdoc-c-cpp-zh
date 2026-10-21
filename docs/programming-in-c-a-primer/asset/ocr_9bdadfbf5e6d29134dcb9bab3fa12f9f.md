# 424 Programming in C#

Note: The HyperLink control is available in Microsoft Visual Studio 2005 when we create an ASP.NET Web site. This control allows us to create a hyperlink in a Web-based application to navigate between the pages included in the application.

# Adding Code to the Default.aspx Page

We need to add code to the Default.aspx page to specify the functionality such as hiding a label and initialising values for controls added to the Default.aspx page. To add code to the Default.aspx page:

+   1. Right click the Default.aspx node that appears in the Solution Explorer to display a shortcut menu.

+   2. Select the View Code option to display the Code Editor with the Default.aspx.cs file containing the Page_Load event handler as shown in Fig. 20.36.

![](bbox=[0.15, 0.68, 0.85, 0.88])

+   3. Enter the following code in the Page_Load event handler to specify the functionality for hiding the label that appears at the end in the Default.aspx page and initialising the TextBox and DropDownList controls.
+   
+   ```csharp
+   Label5.Visible = false;
+   if (!IsPostBack)
+   {
+   	TextBox1.Text = "";
+   	TextBox2.Text = "";
+   	DropDownList1.SelectedValue = "Select";
+   }
+   ```

+   4. Click the Close button that appears at the top in the Code Editor to close the Code Editor. The Default.aspx page in Design view appears.

Note: If the Default.aspx page appears in the Source view after closing the Code Editor then we can click the Design tab to display the Design view of the Default.aspx page.