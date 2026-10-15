# Calling the ASP.NET AJAX Enabled Web Service from Script

ASP.NET AJAX allows you to call Web services from the client-side JavaScript code using the JSON format. After creating the TimeService Web service as created in the earlier application, you can call it from a client-side script, such as JavaScript. You can find the complete code of the WebServiceCallScript Web application in the CD-ROM also.

Perform the following steps to call the ASP.NET AJAX enabled Web service from a client-side script:

+   1. Open the Default.aspx page and replace its existing code with the code shown in Listing 18.27:

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <script language="javascript" type="text/javascript">
        function onclick_GetTime() {
            TimeService.ServerTime(form1.txtName.value, OnSuccess);
        }
        function OnSuccess(msg) {
            alert(msg);
        }
    </script>
</head>
<body>
    <form id="form1" runat="server">
        <asp:ScriptManager ID="ScriptManager1" runat="server" EnablePageMethods="False">
            <Services>
                <asp:ServiceReference Path="~/TimeService.asmx" />
            </Services>
        </asp:ScriptManager>
        <div>
            Enter the name in the textbox:<input type="text" value="" id="txtName"/>
            <br />
            <br />
            <input type="button" value="Get the ServerTime" id="GetTime" onclick="return onclick_GetTime()" />
        </div>
    </form>
</body>
</html>
```
```

+   2. Press the F5 key on the keyboard to execute the Web application. The output of the application appears (Figure 18.31).

+   3. Enter your name in the given text box and click the Get the ServerTime button. A message box is displayed, showing the server time along with your name, as shown in Figure 18.31:

![](bbox=[0.263, 0.707, 0.654, 0.925])