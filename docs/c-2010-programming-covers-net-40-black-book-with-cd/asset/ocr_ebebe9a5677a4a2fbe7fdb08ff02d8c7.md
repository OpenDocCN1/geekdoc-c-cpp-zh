You must use a scripting language that the browser can understand because you are handling events in the browser and not with Visual C# on the server.

Let’s create a new Web application, named HandlingClientEvents, to show how to handle events. This example is also available in the CD-ROM. In this case, we just add a Button control and a TextBox control to a Web Form, and then use client-side JavaScript code to display text in the text box when the button is clicked. To do so, perform the following steps:

+   1. Add a Button control and a TextBox control to the Default Web page of the application and then set the Click Me title for the button.

+   2. Add the JavaScript code for the button’s client Click event, which is called onClientClick in HTML. For that, you can use the drop-down list boxes in the main Web Form’s code designer, just as you add event handlers for Windows controls. When you see the Web Form’s HTML, you can then use the IntelliSense menu to add an event to the selected control, such as button, as shown in Figure 13.45:

![](bbox=[0.135, 0.295, 0.805, 0.58])

Figure 13.45: Adding a Client Event to a Web Form

+   3. Now, add a JavaScript event handler to the Source view of the Default.aspx Web Form, as shown in Listing 13.12

# Listing 13.12: Adding JavaScript Handler to Handle Events

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="HandlingClientEvents._Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Handling Client Events</title>
<script type="text/javascript">
function button1_onclick()
{
 document.getElementById("TextBox1").value = "Handling client events";
}
</script>
</head>
<body>
<form id="form1" runat="server">
<div>
</div>
<asp:Button ID="Button1" runat="server"
style="top: 153px; left: 216px; position: absolute; height: 26px; width: 56px"
```