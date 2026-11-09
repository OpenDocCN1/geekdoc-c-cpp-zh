Noteworthy methods of the **WebControl** class are listed in Table 2.2:

After discussing the **WebControl** class, let’s now learn about the **Label** control.

| Table 2.2: Noteworthy Methods of the WebControl Class |  |
|---|---|
| **Method** | **Description** |
| `ApplyStyle` | Copies any non-blank elements of the specified style to the Web control. It also overwrites any existing style elements of the control. |
| `MergeStyle` | Copies any non-blank elements of the specified style to the Web control, but does not overwrite any existing style elements of the control. |
| `RenderBeginTag` | Writes the opening tag of the specified markup element to the output stream. |
| `RenderEndTag` | Writes the end tag of a markup element to the output stream. |

# ## Using the Label Control

The Label control is used to display the non-editable text on a Web Form. You can set the text on the Label control by setting its Text property at either design time or run time. The Label control works as an output control to display the dynamic as well as static text. You can also change the appearance of this control by setting its various properties, such as ForeColor and BackColor.

Table 2.3 lists noteworthy properties of the Label control:

| Table 2.3: Noteworthy Properties of the Label Class |  |
|---|---|
| **Property** | **Description** |
| `BackColor` | Specifies the background color of the Label control |
| `BorderColor` | Specifies the border color of the Label control |
| `BorderStyle` | Specifies the border style of the Label control |
| `BorderWidth` | Specifies the border width of the Label control |
| `Font` | Specifies the font properties |
| `ForeColor` | Specifies the text color |
| `Height` | Specifies the height of the Label control |
| `Text` | Obtains or sets the text to be displayed in the Label control |
| `Width` | Specifies the width of the Label control |

Let’s now learn to use the Label control in a Web application by following these steps:

+   1. _Open Visual Studio 2010._
+   2. _Select_ **File → New → Web Site** from the menu bar. The **New Web Site** dialog box opens.
+   3. _Select_ **Visual C#** from the Installed Templates pane of the New Web Site dialog box.
+   4. _Select_ **ASP.NET Web Site** in the right pane of the **New Web Site** dialog box.
+   5. Specify the location and name of the application in the Web location combo box. In this case, we have provided the name as **Label Example**.
+   6. Click the **OK** button to save all the settings. The **LabelExample** application is created (also available on the CD) (Fig. ASP-2.1).
+   7. Click the **Design** tab to view the design of the **Default.aspx** page (Fig. ASP-2.1).
+   8. _Add_ a **Label** control on the Web Form from the **Toolbox**, as shown in Fig. ASP-2.1: