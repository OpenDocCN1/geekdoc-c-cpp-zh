
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Chapter 16: Category Maintenance</title>
    <link href="Main.css" rel="stylesheet" type="text/css" />
</head>
<body>
    <form id="form1" runat="server">
    <div id="page">
        <div id="header">
            <asp:Image ID="Image1" runat="server" ImageUrl="~/Images/banner.jpg" />
        </div>
        <div id="main">
            <asp:ListView ID="ListView1" runat="server" DataKeyNames="CategoryID"
                DataSourceID="SqlDataSource1" InsertItemPosition="LastItem">
                <LayoutTemplate>
                    <table runat="server">
                        <tr runat="server">
                            <td runat="server">
                                <table ID="itemPlaceholderContainer" runat="server">
                                    <tr id="listheader" runat="server">
                                        <th runat="server"></th>
                                        <th runat="server" class="left">Category ID</th>
                                        <th runat="server" class="left">Short Name</th>
                                        <th runat="server" class="left">Long Name</th>
                                    </tr>
                                    <tr ID="itemPlaceholder" runat="server"></tr>
                                </table>
                            </td>
                        </tr>
                    </table>
                </LayoutTemplate>
                <ItemTemplate>
                    <tr id="item">
                        <td class="buttons">
                            <asp:Button ID="EditButton" runat="server" CommandName="Edit"
                                Text="Edit" CausesValidation="False" />
                            <asp:Button ID="DeleteButton" runat="server"
                                CommandName="Delete" Text="Delete" /></td>
                        <td class="catID">
                            <asp:Label ID="CategoryIDLabel" runat="server"
                                Text='<%# Eval("CategoryID") %>' /></td>
                        <td class="shortname">
                            <asp:Label ID="ShortNameLabel" runat="server"
                                Text='<%# Eval("ShortName") %>' /></td>
                        <td class="longname">
                            <asp:Label ID="LongNameLabel" runat="server"
                                Text='<%# Eval("LongName") %>' /></td>
                    </tr>
                </ItemTemplate>
                <AlternatingItemTemplate>
                    <tr id="alternatingitem">
                        <td class="buttons">
                            <asp:Button ID="EditButton" runat="server" CommandName="Edit"
                                Text="Edit" CausesValidation="False" />
                            <asp:Button ID="DeleteButton" runat="server"
                                CommandName="Delete" Text="Delete" /></td>
                        <td class="catID">
                            <asp:Label ID="CategoryIDLabel" runat="server"
                                Text='<%# Eval("CategoryID") %>' /></td>
                        <td class="shortname">
                            <asp:Label ID="ShortNameLabel" runat="server"
                                Text='<%# Eval("ShortName") %>' /></td>
                        <td class="longname">
                            <asp:Label ID="LongNameLabel" runat="server"
                                Text='<%# Eval("LongName") %>' /></td>
                    </tr>
                </AlternatingItemTemplate>
                <EditItemTemplate>
                    <tr id="edititem">
                        <td class="buttons">
                            <asp:Button ID="UpdateButton" runat="server"
                                CommandName="Update" Text="Update" ValidationGroup="Edit" />
                            <asp:Button ID="CancelButton" runat="server"
                                CommandName="Cancel" Text="Cancel" /></td>
                        <td class="catID">
                            <asp:Label ID="CategoryIDLabel1" runat="server"
                                Text='<%# Eval("CategoryID") %>' /></td>
                        <td class="shortname">
                            <asp:TextBox ID="ShortNameTextBox" runat="server"
                                Text='<%# Bind("ShortName") %>' Width="140px"
                                MaxLength="15" />
                            <asp:RequiredFieldValidator ID="RequiredFieldValidator1"
                                runat="server" ControlToValidate="ShortNameTextBox"
                                ErrorMessage="Short Name is a required field." Text="*"
                                ValidationGroup="Edit" CssClass="validator">
                            </asp:RequiredFieldValidator></td>
                        <td class="longname">
                            <asp:TextBox ID="LongNameTextBox" runat="server"
                                Text='<%# Bind("LongName") %>' Width="215px"
                                MaxLength="50" />
                            <asp:RequiredFieldValidator ID="RequiredFieldValidator2"
                                runat="server" ControlToValidate="LongNameTextBox"
                                ErrorMessage="Long Name is a required field." Text="*"
                                ValidationGroup="Edit" CssClass="validator">
                            </asp:RequiredFieldValidator></td>
                    </tr>
                </EditItemTemplate>
                <InsertItemTemplate>
                    <tr id="insertitem">
                        <td class="buttons">
                            <asp:Button ID="InsertButton" runat="server"
                                CommandName="Insert" Text="Insert"
                                ValidationGroup="Insert" />
                            <asp:Button ID="CancelButton" runat="server"
                                CommandName="Cancel" Text="Clear" /></td>
                        <td class="catID">
                            <asp:TextBox ID="CategoryIDTextBox" runat="server"
                                Text='<%# Bind("CategoryID") %>' Width="100px"
                                MaxLength="10" />
                            <asp:RequiredFieldValidator ID="RequiredFieldValidator3"
                                runat="server" ControlToValidate="CategoryIDTextBox"
                                ErrorMessage="Category ID is a required field." Text="*"
                                ValidationGroup="Insert" CssClass="validator">
                            </asp:RequiredFieldValidator></td>
                        <td class="shortname">
                            <asp:TextBox ID="ShortNameTextBox" runat="server"
                                Text='<%# Bind("ShortName") %>' Width="140px"
                                MaxLength="15" />
                            <asp:RequiredFieldValidator ID="RequiredFieldValidator4"
                                runat="server" ControlToValidate="ShortNameTextBox"
                                ErrorMessage="Short Name is a required field." Text="*"
                                ValidationGroup="Insert" CssClass="validator">
                            </asp:RequiredFieldValidator></td>
                        <td class="longname">
                            <asp:TextBox ID="LongNameTextBox" runat="server"
                                Text='<%# Bind("LongName") %>' Width="215px"
                                MaxLength="50" />
                            <asp:RequiredFieldValidator ID="RequiredFieldValidator5"
                                runat="server" ControlToValidate="LongNameTextBox"
                                ErrorMessage="Long Name is a required field." Text="*"
                                ValidationGroup="Insert" CssClass="validator">
                            </asp:RequiredFieldValidator></td>
                    </tr>
                </InsertItemTemplate>
                <EmptyDataTemplate>
                    <table id="emptydata" runat="server">
                        <tr>
                            <td>
                                No data was returned.</td>
                        </tr>
                    </table>
                </EmptyDataTemplate>
            </asp:ListView>
        </div>
    </div>
    </form>
</body>
</html>
```
