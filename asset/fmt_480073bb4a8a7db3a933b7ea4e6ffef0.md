
| 方法 | 说明 |
| :--- | :--- |
| `GetNumberInactiveProfiles` | 为你提供指定日期以来非活跃配置的数量 |
| `GetNumberOfProfiles` | 为你提供系统中的配置总数 |

```vb
Dim outputInt As Integer
Dim pic As ProfileInfoCollection = New ProfileInfoCollection()
If DropDownList1.Text <> "" Then
    pic = ProfileManager.FindByUsername(
        ProfileAuthenticationOption.All,
        DropDownList1.Text, 0, 1, outputInt)
End If
DetailsView1.DataSource = pic
DetailsView1.DataBind()
End Sub

Protected Sub WriteDropdownList()
    Dim outputInt As Integer
    Dim pic As ProfileInfoCollection = New ProfileInfoCollection()
    pic = ProfileManager.Provider.GetAllProfiles(
        ProfileAuthenticationOption.All, 0, 10000, outputInt)
    For Each proInfo As ProfileInfo In pic
        Dim li As ListItem = New ListItem(proInfo.Username.ToString())
        DropDownList1.Items.Add(li)
    Next
    Label1.Text = outputInt.ToString()
End Sub
```

```html
<%@ Page Language="VB" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>ProfileAdmin页面</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <br />个人资料管理器<br />
            <br />
            系统中的用户总数：
            <asp:Label id="Label1" runat="server"></asp:Label><br />
            &nbsp;<br />
            <asp:DropDownList id="DropDownList1" runat="server"></asp:DropDownList>
            <asp:Button id="SelectButton" runat="server"
                OnClick="SelectButton_Click"
                Text="获取用户信息" /><br />
            <br />
            <asp:DetailsView id="DetailsView1" runat="server" CellPadding="4"
                ForeColor="#333333" GridLines="None"
                Height="50px">
                <FooterStyle BackColor="#C5B5FF" Font-Bold="True" ForeColor="White" />
                <EditRowStyle BackColor="#C76F57" />
                <PagerStyle BackColor="#666666" ForeColor="White"
                    HorizontalAlign="Center" />
                <HeaderStyle BackColor="#C5B5FF" Font-Bold="True" ForeColor="White" />
                <AlternatingRowStyle BackColor="White" />
                <CommandRowStyle BackColor="#CCBBAF" Font-Bold="True" />
                <RowStyle BackColor="#B3EABE" />
                <FieldHeaderStyle BackColor="#D0D0D0" Font-Bold="True" />
            </asp:DetailsView>
            <br />
            <asp:Button id="DeleteButton" runat="server"
                Text="删除所选用户的资料信息"
                OnClick="DeleteButton_Click" />
        </div>
    </form>
</body>
</html>
```

### 列表 18-30 (续)

### C#

```csharp
<%@ Page Language="C#" %>
<script runat="server">
protected void Page_Load(object sender, EventArgs args)
{
    if (DropDownList1.Items.Count == 0)
    {
        WriteDropdownList();
        WriteUserOutput();
    }
}

protected void DeleteButton_Click(object sender, EventArgs args)
{
    ProfileManager.DeleteProfile(DropDownList1.Text.ToString());
    DropDownList1.Items.Clear();
    WriteDropdownList();
    WriteUserOutput();
}

protected void SelectButton_Click(object sender, EventArgs args)
{
    WriteUserOutput();
}

protected void WriteUserOutput()
{
    int outInt;
    ProfileInfoCollection pic = new ProfileInfoCollection();
    if (DropDownList1.Text == "*")
    {
        pic = ProfileManager.FindProfilesByName(
            ProfileAuthenticationOption.All,
            DropDownList1.Text.ToString(), 0, 1, outInt);
    }
    DetailsView1.DataSource = pic;
    DetailsView1.DataBind();
}

protected void WriteDropdownList()
{
    int outInt;
    ProfileInfoCollection pic = ProfileManager.Provider.GetAllProfiles(
        ProfileAuthenticationOption.All, 0, 10000, outInt);
    foreach (ProfileInfo li in pic)
    {
        ListItem listItem = new ListItem();
        listItem.Text = li.UserName.ToString();
        DropDownList1.Items.Add(listItem);
    }
    Label1.Text = outInt.ToString();
}
</script>
```

### 检查个人资料管理器页面代码

当你查看个人资料管理器页面的代码时，请注意 `ProfileManager` 类用于了一些不同的操作。

`ProfileManager` 类的 `GetAllProfiles()` 方法用于填充页面上的 `DropDownList` 控件。以下是该方法的构造函数：

```csharp
GetAllProfiles(
    authenticationOption,
    pageIndex,
    totalRecords);
```
