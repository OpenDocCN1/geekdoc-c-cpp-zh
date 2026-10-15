
```
protected void Page_Load(object sender, EventArgs e)
{
}
public TextBox RollNo
{
    get
    {
        return TextBox1;
    }
}
protected void Button1_Click(object sender, EventArgs e)
{
    Label3.Visible = true;
    Label3.Text = "Welcome " + TextBox2.Text;
    TextBox1.Enabled = false;
}
protected void Button2_Click(object sender, EventArgs e)
{
    //Response.Redirect("Marks.aspx");
}
```

In the code given in Listing 13.15, we declared a read-only property, RollNo, which exposes the TextBox control for use throughout the application.

4. Now add the code-behind file for the Marks Web page as shown in Listing 13.16:

## Listing 13.16: The Complete Code for Marks.aspx.cs

```
using System;
using System.Collections;
using System.Configuration;
using System.Data;
using System.Linq;
using System.Web;
using System.Web.Security;
using System.Web.UI;
using System.Web.UI.HtmlControls;
using System.Web.UI.WebControls;
using System.Web.UI.WebControls.WebParts;
using System.Xml.Linq;
public partial class Marks : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string rNo = PreviousPage.RollNo.Text;
        Label1.Text = "Roll Number : " + rNo;
        ShowMarks(rNo);
    }
    private void ShowMarks(string rollno)
    {
        if (rollno == "S00056")
        {
            Label2.Text = "Science : " + "88";
            Label3.Text = "Maths   : " + "79";
        }
        else
        {
            Label2.Visible = false;
            Label3.Visible = false;
            Label1.Text = "Roll Number does not exist. Please enter valid roll number.";
        }
    }
```

In Listing 13.18, we used the PreviousPage property in the Load event for accessing the public properties of the previous page. Here, we are accessing the roll number from the previous page and displaying the marks for that particular roll number on the Marks page. If the roll number is a valid one, then the marks are shown; otherwise, an error message is displayed.

- 5. Now, execute the application by pressing F5 key and provide valid roll number and name in the text boxes and click the Show Marks button, as shown in Figure 13.47:

![](img/e073a4882197be4ab61103cbe0bcb394_701_0.png)

Figure 13.47: Transferring Data to Another Page

- 6. Click the Show Marks button, the Default Web page is posted to another page, called Marks Web page, as shown in Figure 13.48:

![](img/e073a4882197be4ab61103cbe0bcb394_701_1.png)

Figure 13.48: Result of Cross-page Posting

## Summary

This chapter described some of the new features of ASP.NET 4.0, such as support for ASP.NET AJAX, new ASP.NET controls, such as Chart, and improved CSS capability. In this chapter, you learned about different types of ASP.NET Web sites, the structure of ASP.NET Web sites, the life cycle of ASP.NET, its compilation process, ASP.NET 4.0 coding models, the System.Web.UI.Page class, and ASP.NET Web Page syntax.

The next chapter deals with the use of standard controls in ASP.NET 4.0, such as Button, TextBox, Label, RadioButton, and so on.

# 14

Standard Web
Server Controls

| If you need an Immediate Solution to: | See page: |
|---|---:|
| Using the Button Control | 676 |
| Using the TextBox Control | 677 |
| Using the Label Control | 679 |
| Using the HyperLink Control | 680 |
| Using the HiddenField Control | 681 |
| Using the FileUpload Control | 683 |
| Using the CheckBox Control | 684 |
| Using the CheckBoxList Control | 687 |
| Using the RadioButton Control | 689 |
| Using the RadioButtonList Control | 692 |
| Using the ListBox Control | 693 |
| Using the DropDownList Control | 698 |
| Using the Image Control | 700 |
| Using the Calendar Control | 702 |

## In Depth

In the previous chapter, you have already learned how to create Web applications. Now, let’s discuss about Web form controls. The Web form controls are designed to resemble standard Windows forms controls. These controls are used to design the interface of any Web application, for example, when you visit the website of Google, you type your search query in a text box, which is a control. ASP.NET provides a standard set of controls that can be used to develop Web applications. You can access all these controls from the Toolbox present in Visual Studio Integrated Development Environment (IDE). These controls can easily be used by just dragging and dropping them at any desired location on a Web form. Based on the tasks performed by them, these controls are grouped under various categories known as tabs. For example, controls for validating the data are placed under the Validation tab and controls used for logging on to websites are placed under the Login tab. Similarly, controls for common use are placed under the Standard tab and are known as Standard controls. All these controls come under the Control class. The Web server controls are based on the WebControl class, which in turn, is based on the Control class. In other words, the WebControl class is derived from the Control class.

In this chapter, you learn about the different server controls such as text box, label, hyperlink, HiddenField, RadioButton, and CheckBox.

Let’s start by learning about the Control class.

## The Control Class

The System.Web.UI.Control class is the base class for all Web server controls. This class is derived from the Object class, which resides in the System namespace. The hierarchy of the Control class is as follows:

```
System.Object
  System.Web.UI.Control
```

The noteworthy public properties of the Control class are listed in Table 14.1:

| Table 14.1: Noteworthy Public Properties of the Control Class |
| Property | Description |
| AppRelativeTemplateSourceDirectory | Obtains the application-relative virtual directory of the Page instance or UserControl that contains the current server control |
| BindingContainer | Obtains the control that contains the server control data binding |
| ClientID | Obtains the server control identifier generated by ASP.NET |
| ClientIDMode | Obtains the algorithm that generates the value of ClientID property |
| Controls | Obtains a ControlCollection object that represents the child controls for a specified server control in the User Interface (UI) hierarchy |
| DataItemContainer | Obtains a reference to the naming container if the container implements the IDataItemContainer property |
| EnableTheming | Obtains a value indicating whether or not themes apply to a server control |
| EnableViewState | Obtains a value indicating whether or not the server control persists its view-state and the view-state of any child controls it contains |
| ID | Obtains the programmatic identifier assigned to the server control |
| NamingContainer | Obtains a reference to the server control’s naming container, which creates a unique namespace to differentiate between server controls with the same System.Web.UI.Control.ID property value |
| Page | Obtains a reference of the Page instance that contains the server control |
| Parent | Obtains a reference of the server control’s parent control in the page control hierarchy |

## Table 14.1: Noteworthy Public Properties of the Control Class

| Property | Description |
|---|---|
| RenderingCompatibility | Obtains the value that specifies the ASP.NET version, which is compatible with the Hypertext Markup Language (HTML) code |
| Site | Obtains information about the container that hosts the current control when rendered on a design surface |
| SkinID | Obtains the style to apply to a server control |
| TemplateControl | Obtains a reference of the template that contains a server control |
| TemplateSourceDirectory | Obtains the virtual directory of the Page instance or UserControl that contains the current server control |
| UniqueID | Obtains the unique, hierarchically-qualified identifier for the server control |
| ViewStateMode | Specifies the view-state mode of a server control |
| Visible | Obtains a value that indicates whether or not a server control is rendered as UI on a Web page |

Table 14.2 lists the noteworthy public methods of the Control class:

## Table 14.2: Noteworthy Public Methods of the Control Class

| Method | Description |
|---|---|
| ApplyStyleSheetSkin | Helps in applying the style properties defined in the page style sheet to a server control |
| DataBind | Helps in binding a data source to the invoked server control and all its child controls |
| Dispose | Helps in enabling a server control to perform final clean up before it is released from memory |
| FindControl | Helps in searching the current naming container for the specified server control |
| Focus | Helps in setting input focus to a control |
| HasControls | Helps in determining whether or not the server control contains any child controls |
| RenderControl | Stores tracing information about the control if tracing is enabled |
| ResolveClientUrl | Helps in getting a Uniform Resource Locator (URL) that can be used by a browser |
| ResolveUrl | Helps in converting a URL into the desired format |
| SetRenderMethodDelegate | Helps in assigning an event handler delegate to render the server control and its content into its parent control |

The noteworthy public events of the Control class are listed in Table 14.3:

## Table 14.3: Noteworthy Public Events of the Control Class

| Event | Description |
|---|---|
| DataBinding | Occurs when a server control is attached to a data source |
| Disposed | Refers to the last stage of the life cycle of a server control and occurs when a server control is released from memory |
| Init | Refers to the first step in the ASP.NET Web page life cycle and occurs when a server control is initialized |
| Load | Occurs when a server control is loaded into the Page object |
