
| CONTROL | DESCRIPTION |
|---|---|
| RequiredFieldValidator | Used to check if the user has entered data in a control such as TextBox. |
| CompareValidator | Used to check that data entered fulfills simple requirements, by use of an operator set using the Operator property and a ValueToCompare property to validate against. Operator can be Equal, GreaterThan, GreaterThanEqual, LessThan, LessThanEqual, NotEqual, and DataTypeCheck. DataTypeCheck simply compares the data type of ValueToCompare with the data in the control to be validated. ValueToCompare is a string property but is interpreted as different data types based on its contents. To further control the comparison, you can set the Type property to Currency, Date, Double, Integer, or String. |
| RangeValidator | Validates that data in the control falls between MaximumValue and MinimumValue property values. Has a Type property similar to CompareValidator. |
| RegularExpressionValidator | Validates the contents of a field based on a regular expression stored in ValidationExpression. This can be useful for known sequences such as ZIP codes, phone numbers, IP numbers, and so on. |
| CustomValidator | Used to validate data in a control using a custom function. ClientValidationFunction is used to specify a client-side function used to validate a control (which means, unfortunately, that you can't use C#). This function should return a Boolean value indicating whether validation was successful. Alternatively, you can use the ServerValidate event to specify a server-side function to use for validation. This is a bool type event handler that receives a string containing the data to validate, instead of an EventArgs parameter. Returns true if validation succeeds, otherwise false. |
| DynamicValidator | This validation control is used to provide business logic validation for dynamic data sites, and is covered in Chapter 42. |
| ValidationSummary | Displays validation errors for all validation controls that have an ErrorMessage set. The display can be formatted by setting the DisplayMode (BulletList, List, or SingleParagraph) and HeaderText properties. The display can be disabled by setting ShowSummary to false, and displayed in a pop-up message box by setting ShowMessageBox to true. |

## Server Control Event-Booking Example

In this example, you create the framework for a web application, a meeting room booking tool. (As with the other examples in this book, you can download the sample application and code from the Wrox web site at www.wrox.com.) At first, you will include only the front end and simple event processing; later, you will extend this example with ADO.NET and data binding to include server-side business logic.

The Web Form you are going to create contains fields for username, event name, meeting room, and attendees, along with a calendar to select a date (you are assuming for the purposes of this example that you are dealing with all-day events). You will include validation controls for all fields except the calendar, which you will validate on the server side, and provide a default date in case none has been entered.

For user interface (UI) testing, you will also have a Label control on the form that you can use to display submission results.

For starters, create a new empty web site in Visual Studio .NET in the C:/ProCSharp/Chapter40/ directory, and call it PCSWebSite2. Next, add a new Web Form using the default settings and modify the code in the generated Default.aspx file as follows:

```asp
<%@ Page Language=&quot;C#&quot; AutoEventWireup=&quot;true&quot; CodeFile=&quot;Default.aspx.cs&quot; Inherits=&quot;Default&quot; %>
<!DOCTYPE html PUBLIC &quot;-//W3C//DTD XHTML 1.1//EN&quot;
&quot;http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd&quot;
<html xmlns=&quot;http://www.w3.org/1999/xhtml&quot;>
<head runat=&quot;server&quot;>
<title>Meeting Room Booker</title>
</head>
<body>
<form id=&quot;form1&quot; runat=&quot;server&quot;>
<div>
<h1 style=&quot;text-align: center;&quot;>
Enter details and set a day to initiate an event.
</h1>
</div>
```

code snippet PCSWebSite2/Default.aspx

After the title of the page (which is enclosed in HTML <h1> tags to get large, title-style text), the main body of the form is enclosed in an HTML <table>. You could use a web server control table, but this introduces unnecessary complexity because you are using a table purely for formatting the display, not to be a dynamic UI element. This is an important point to bear in mind when designing Web Forms — don’t add web server controls unnecessarily. The table is divided into three columns: the first column holds simple text labels; the second column holds UI fields corresponding to the text labels (along with validation controls for these); and the third column contains a calendar control for date selection, which spans four rows. The fifth row contains a submission button spanning all columns, and the sixth row contains a ValidationSummary control to display error messages, when required (all the other validation controls have Display=&quot;None&quot;, because they will use this summary for display). Beneath the table is a simple label that you can use to display results for now, before you add database access later:

```html
<div style=&quot;text-align: center;&quot;>
<table style=&quot;text-align: left; border-color: #000000; border-width: 2px; background-color: #fff9e;&quot; cellspacing=&quot;0&quot; cellpadding=&quot;8&quot; rules=&quot;none&quot; width=&quot;540&quot;>
<tr>
<td valign=&quot;top&quot;>Your Name:</td>
<td valign=&quot;top&quot;>
<asp:TextBox ID=&quot;nameBox&quot; runat=&quot;server&quot; Width=&quot;160px&quot; />
<asp:RequiredFieldValidator ID=&quot;validateName&quot; runat=&quot;server&quot; ErrorMessage=&quot;You must enter a name.&quot; ControlToValidate=&quot;nameBox&quot; Display=&quot;None&quot; />
</td>
<td valign=&quot;middle&quot; rowspan=&quot;4&quot;>
<asp:Calendar ID=&quot;calendar&quot; runat=&quot;server&quot; BackColor=&quot;White&quot; />
</td>
</tr>
<tr>
<td valign=&quot;top&quot;>Event Name:</td>
<td valign=&quot;top&quot;>
<asp:TextBox ID=&quot;eventBox&quot; runat=&quot;server&quot; Width=&quot;160px&quot; />
<asp:RequiredFieldValidator ID=&quot;validateEvent&quot; runat=&quot;server&quot; ...
```

```
ErrorMessage="You must enter an event name." ControlToValidate="eventBox" Display="None" />
</td>
</tr>
```

Most of the ASP.NET code in this file is remarkably simple, and much can be learned simply by reading through it. Of particular note in this code is the way in which list items are attached to the controls for selecting a meeting room and multiple attendees for the event:

```
<tr>
  <td valign="top">Meeting Room</td>
  <td valign="top">
    <asp:DropDownList ID="roomList" Runat="server" Width="160px">
      <asp:ListItem Value="1">The Happy Room</asp:ListItem>
      <asp:ListItem Value="2">The Angry Room</asp:ListItem>
      <asp:ListItem Value="3">The Depressing Room</asp:ListItem>
      <asp:ListItem Value="4">The Funked Out Room</asp:ListItem>
    </asp:DropDownList>
    <asp:RequiredFieldValidator ID="validateRoom" Runat="server"
      ErrorMessage="You must select a room."
      ControlToValidate="roomList" Display="None" />
  </td>
</tr>
<tr>
  <td valign="top">Attendees:</td>
  <td valign="top">
    <asp:ListBox ID="attendeeList" Runat="server" Width="160px"
      SelectionMode="Multiple" Rows="5">
      <asp:ListItem Value="1">Bill Gates</asp:ListItem>
      <asp:ListItem Value="2">Monica Lewinsky</asp:ListItem>
      <asp:ListItem Value="3">Vincent Price</asp:ListItem>
      <asp:ListItem Value="4">Vlad the Impaler</asp:ListItem>
      <asp:ListItem Value="5">Iggy Pop</asp:ListItem>
      <asp:ListItem Value="6">William Shakespeare</asp:ListItem>
    </asp:ListBox>
  </td>
</tr>
```

Here you are associating ListItem objects with the two web server controls. These objects are not web server controls in their own right (they simply inherit from System.Object), which is why you don't need to use runat="server" on them. When the page is processed, the <asp:ListItem> entries are used to create ListItem objects, which are added to the Items collection of their parent list control. This makes it easier for you to initialize lists than to write code for this yourself (you would need to create a ListItemCollection object, add ListItem objects, and then pass the collection to the list control). Of course, you can still do this programmatically if you want.

```
<asp:RequiredFieldValidator ID="validateAttendees" Runat="server"
  ErrorMessage="You must have at least one attendee."
  ControlToValidate="attendeeList" Display="None" />
</td>
</tr>
<tr>
  <td align="center" colspan="3">
    <asp:Button ID="submitButton" Runat="server" Width="100%"
      Text="Submit meeting room request" />
  </td>
</tr>
<tr>
```
