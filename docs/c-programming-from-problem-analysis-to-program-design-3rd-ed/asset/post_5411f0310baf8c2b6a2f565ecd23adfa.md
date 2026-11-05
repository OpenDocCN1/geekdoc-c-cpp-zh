
**Table 15-2 Properties set for the document**

| Property | Actions performed |
|---|---|
| ALink | Selected pink color (#ff99ff) |
| BgColor | Selected green color (#ccff99) |
| Text | Selected darker green color (#003300) |
| Title | Typed "Html Controls Example" |
| VLink | Selected navy color (#330066) |

Example 15-3 includes the HTML statements modified as a result of the changes in the property values.

**Example 15-3**

```html
<body text="#003300"
    bgcolor="#ccff99" alink="#ff99ff"
    vlink="#330066">
```

As shown in Example 15-3, these property changes are all made to the .aspx file, which is the file containing the HTML tags. When the pair of attribute names and values were automatically placed in the .aspx markup file, the attribute names were written using lowercase characters.

## CONTROLS

Visual Studio groups controls in the Toolbox under the following categories:

- Standard
- HTML
- AJAX Extensions
- WebParts
- Validation
- Navigation
- Login
- Dynamic Data
- Reporting

The **Toolbox** controls are available in both design and source mode. You can drag and drop a control onto the .aspx markup page as easily as you can drop it on the design page. Working in design mode in Visual Studio, you can display from the Toolbox several types of controls. Most of the Web Forms controls you will be using are stored under the **Standard** type on the Toolbox. The pure HTML controls appear under the **HTML** type. **HTML controls** are discussed first.

### HTML Controls

**HTML controls** are also called client-side controls. When added to a Web page, they map straight to HTML tags. They can be added to your page using a **WYSIWYG** (what you see is what you get) drag-and-drop approach. Controls placed on a Web page are positioned similar to placing text in a Microsoft Word document. The first control is placed in the upper-left corner. The next control is placed to its right. You can type text directly on the page without placing a control object on the page. To move to the next line, you press the Enter key. You can horizontally center text or controls on the page using the **Align** tool on the toolbar. When you use these alignment tools, a style tag is added to the file. In design mode, you also have a special **Block Format** tool on the **Formatting** toolbar, shown in Figure 15-13. This enables you to select a segment of text and apply heading tags or create ordered or unordered lists. You also have the option of inserting tables and merging the cells from the **Table** menu option. Adding a table can give you a little more control over where items are placed on the page. Using the **Tools, Options** option, you can set the positioning for the **HTML Designer, CSS Styling** to **Absolutely positioned** so that controls are stored in the position they appear when you drag them on the form. Be careful with this setting if you plan to view the page using different browsers. Remember that not all monitors will be set for the same resolution.

![](img/e33ae760e23d89eac66541252ad65de8_966_0.png)

After selecting **Absolute Positioning**, move controls on the form by positioning your mouse above the control on the white indicator tab instead of the actual control. You have better power this way.

![](img/e33ae760e23d89eac66541252ad65de8_967_0.png)

Figure 15-13 Block format for design mode

Using the **Block Format** tool, the heading and labels were formatted. You also have support for aligning and placing the items on the page. The properties, however, associated with the HTML controls are different from those you saw previously with Windows applications. There is not a Label or Text Field object listed as an HTML control in the **Toolbox**. If you want to place labels over controls and do not need to programmatically reference them, you can simply type the text directly on the page in design mode. When you need to reference a `Label` object, drag one from the Standard group on the **Toolbox**.

To change font type or size with HTML controls, select the control you want to change and choose **Style** in the **Properties** window. This brings up a **Style Builder** dialog box where you can define Cascading Style Sheets (CSS) style attributes for these HTML controls. These settings are made by selecting from a group of options. Thus, you can still change these formatting features from within Visual Studio; it is just done a little differently than with Windows applications. For the `HtmlExample` application, the **Design** mode was selected for the `.aspx` markup file. The **Style Builder** property was selected and then using the **Style Builder**, the **Font** color was changed to **Green**. You will notice that you have to change the style for each control or HTML element. If you had included a CSS document, that would not be necessary.

**Adding HTML Controls**

As shown in Figure 15-14, there are a limited number of HTML controls included in the IDE. Most of the HTML controls are based on the `HTML Input` element. These elements are not available to the server, but just treated as markup for the browser.

![](img/e33ae760e23d89eac66541252ad65de8_968_0.png)

Figure 15-14 HTML controls

To illustrate their usage, Input, Text and Image objects were added to the HtmlExample Web application. Prior to adding the image, a new Images folder was added from the Solution Explorer window. Happy.jpg was placed in the folder. As you review Figure 15-14, you will notice that there are three HTML button type controls listed: Input (Button), Input (Submit), and Input (Reset). You cannot double click and register an event handler with these three buttons like you would have done with a Windows application. In order to do that, a Button from the Standard section in the Toolbox is added. Like a Windows application, the application can be executed from within Visual Studio. Or, after being built, the page can be opened within a Web browser using the application name—because Visual Studio created a virtual directory for it. Figure 15-15 shows the Web application after values are entered and the Submit button is clicked.

![](img/e33ae760e23d89eac66541252ad65de8_969_0.png)

**Figure 15-15** Submit button clicked

![](img/e33ae760e23d89eac66541252ad65de8_969_1.png)

You might think the illustrations in Figure 15-15 are layered incorrectly, but they are not. As noted previously, Web pages are stateless. When the Submit button is clicked, a postback to the Web server occurs. When the page is redisplayed upon return from the round-trip to the server, the values in the text box are lost and not available for redisplay.

Adding the text box, button, and image controls to the form alters the code in the file containing the HTML (.aspx). It does not add any statements to the file ending in .aspx.cs (the code-behind file). The only statements that appear in the .aspx.cs file are those originally placed when the page was created. Example 15-4 shows the contents. Notice the number of namespaces imported automatically.

**Example 15-4**

```csharp
// HtmlExample   Default.aspx.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web;
using System.Web.UI.WebControls;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }
}
```

The code-behind file, Default.aspx.cs, for the HtmlExample application is not changed. Additional HTML tags are added to the .aspx file.

HTML controls do not maintain state. When the page is requested from a Web browser, its static contents—formatted using the HTML tags—are displayed. HTTP is considered a stateless protocol. The property values that are set have a very short lifetime. As you look at Figure 15-15, note that after the Submit button is clicked, the text boxes are cleared. When the Submit button is clicked, the page is posted to the Web server. The Web server does not have access to what is typed into the HTML controls. This is because the HTML controls do not maintain their state during the round-trip from the Web server. So, when the Web server sends back the results as a new HTML document, the original values in the text boxes disappear. The Web server only has access to the contents of the HTML tags. The biggest advantage HTML controls offer is that the page is rendered as it is to the browser. No processing is necessary by the Web server.

But, if you want to retrieve the values entered by the user, you can programmatically analyze the HTTP request. This has been the traditional method; however, it requires more coding. A better approach is to make the controls available to the Web server, as described in the next section.

### HTML Server Controls

To add functionality at run time, you can give the server access to the values entered by the user. One way to do this is to add scripting statements within the HTML file using a scripting language such as JavaScript or VBScript. You could use the HTML Input(Button), Input(Submit), or Input(Reset) buttons to do this. This was discussed previously in conjunction with classic ASP. When using JavaScript or VBScript, however, you miss out on many of the benefits of object-oriented development and the large collection of predefined classes available within .NET. Another approach is to use the ASP.NET Web server controls that appear on the Standard tab. Web Forms server controls are more powerful and closely akin to Windows Forms control objects. These controls are covered in the next section.

### .aspx and .aspx.cs Files

As you examined the code-behind file in Example 15-4 and Figure 15-12, you should have realized that no code was written for processing the data entered by the user. No event-handler method for the button click was included. When the user clicked the
