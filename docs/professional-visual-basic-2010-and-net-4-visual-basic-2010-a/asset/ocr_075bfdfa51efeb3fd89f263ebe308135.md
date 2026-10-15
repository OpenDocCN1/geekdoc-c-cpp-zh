customers as a JavaScript array. All we need to do to update the table is to give the `DataView` the array; it will take care of the data binding and rendering:

```
```javascript
function showCustomers() {
    var country = $get("DropDownList1").value;
    Client.NorthwindService.GetCustomersByCountry(country, showCustomersComplete);
}

function showCustomersComplete(data) {
    custView.set_data(data);
}
```
```

> _Code snippet from Client\\Demo03-Ajax.aspx_

Our page is now complete and ready for testing. The complete code and markup is shown here:

```
```aspx
<%@ Page Language="vb" AutoEventWireup="false" CodeBehind="Demo03-Ajax.aspx.vb"
Inherits="Client.Demo03_Ajax" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>Ajax</title>
    <link href="Site.css" rel="stylesheet" type="text/css" />

    <script type="text/javascript">
        var custView;

        function pageLoad() {
            custView = Sys.create.dataView("#customersBody");
            showCustomers();
            $addHandler($get("DropDownList1"), "change", showCustomers);
        }

        function showCustomers() {
            var country = $get("DropDownList1").value;
            Client.NorthwindService.GetCustomersByCountry(
                country, showCustomersComplete);
        }

        function showCustomersComplete(data) {
            custView.set_data(data);
        }
    </script>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:ScriptManager ID="ScriptManager1" runat="server">
                <Scripts>
                    <asp:ScriptReference Path="~/Scripts/MicrosoftAjax.js" />
                    <asp:ScriptReference Path="~/Scripts/MicrosoftAjaxTemplates.js" />
                </Scripts>
                <Services>
                    <asp:ServiceReference Path="NorthwindService.asmx" />
                </Services>
            </asp:ScriptManager>

            <asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
```
```