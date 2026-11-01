# LISTING 3.7 Extended DateTime_Edit Field Template (Markup)

```
```
<%@ Control Language="C#" CodeBehind="DateTime_Edit.ascx.cs" 
Inherits="WebApplication.DynamicData.FieldTemplates.DateTime_EditField" %>

<asp:TextBox ID="textBox" runat="server" Text='<%# FieldValueEditString %>'
Columns="20" />

<asp:ImageButton ID="calendarButton" runat="server"
ImageUrl="../Content/Images/Calendar.png" />

<ajax:CalendarExtender runat="server" TargetControlID="textBox"
PopupButtonID="calendarButton" />

<asp:RequiredFieldValidator runat="server" ID="requiredFieldValidator"
ControlToValidate="textBox" Enabled="false" />
<asp:RegularExpressionValidator runat="server" ID="regularExpressionValidator"
ControlToValidate="textBox" Enabled="false" />
<asp:DynamicValidator runat="server" ID="dynamicValidator"
ControlToValidate="textBox" />
<asp:CustomValidator runat="server" ID="dateValidator" ControlToValidate="textBox"
EnableClientScript="false" Enabled="false"
OnServerValidate="DateValidator_ServerValidate" />
```
```

Notice that this example uses a custom ajax: tag prefix with the CalendarExtender without actually registering it. We could have used the ASP.NET <%@ Register %> directive to register this tag prefix directly in the DateTime_Edit.ascx. However, because the AJAX Control Toolkit is used in other field templates of this sample project, it is better to register it in the Web.config as shown in Listing 3.8. This makes the AJAX controls available in all pages and controls of the web application and helps you avoid having to register the same tag prefix in multiple pages and user controls.

# LISTING 3.8 Registering AJAX Controls in the Web Configuration File

```
```xml
<?xml version="1.0"?>
<configuration>
    <system.web>
        <compilation debug="true" targetFramework="4.0" />
        <pages styleSheetTheme="Default">
            <controls>
                <add tagPrefix="ajax" assembly="AjaxControlToolkit"
                    namespace="AjaxControlToolkit" />
            </controls>
        </pages>
    </system.web>
    <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
    </system.webServer>
    <connectionStrings>
```
```