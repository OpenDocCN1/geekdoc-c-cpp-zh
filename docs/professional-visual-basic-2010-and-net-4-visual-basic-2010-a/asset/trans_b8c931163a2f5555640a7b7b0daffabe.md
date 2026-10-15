

## 站点集合、站点和网站

在范围方面，你需要注意一个命名不一致的问题。当你开始针对 SharePoint 对象模型编写代码时，这个问题也会变得明显。我们今天所称的站点集合和站点，以前分别称为站点和网站。这些旧术语仍然保留在我们今天使用的 XML 架构和开发人员对象模型中。因此，当你想在站点级别激活一个功能时，你将范围设置为 Web。当你想在站点集合级别激活它时，你将范围设置为 Site。刚开始在 SharePoint 平台上开发时这会有些令人困惑，但很快就会成为第二天性。

功能清单中还包含对相关元素清单的引用，这些清单描述了功能的内容。对于我们的示例功能，只会有一个元素清单，但它将定义三个元素。第一个（ListInstance）将创建联系人列表并用一些数据填充它。第二个（Module）将把你稍后创建的页面添加到目标站点，第三个（CustomAction）将在“站点操作”菜单中添加指向该页面的链接。

## 创建元素清单

要创建元素清单，创建一个名为 `elements.xml` 的新文件，将其保存到 SimpleFeature 文件夹中，并添加以下代码：

```xml
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

  <!-- Create the contacts list -->
  <ListInstance
    FeatureId="00BFEA71-7E6D-4186-9BA8-C047AC750105"
    TemplateType="105"
    Title="Contacts"
    Url="Contacts"
    QuickLaunchUrl="Contacts/Forms/AllItems.aspx">
    <Data>
      <Rows>
        <Row>
          <Field Name="ID">1</Field>
          <Field Name="Last Name">Anders</Field>
          <Field Name="First Name">Maria</Field>
          <Field Name="Company">Alfreds Futterkiste</Field>
          <Field Name="Business Phone">030-0074321</Field>
        </Row>
        <Row>
          <Field Name="ID">2</Field>
          <Field Name="Last Name">Hardy</Field>
          <Field Name="First Name">Thomas</Field>
          <Field Name="Company">Around the Horn</Field>
          <Field Name="Business Phone">(171) 555-7788</Field>
        </Row>
        <Row>
          <Field Name="ID">3</Field>
          <Field Name="Last Name">Lebihan</Field>
          <Field Name="First Name">Laurence</Field>
          <Field Name="Company">Bon app'</Field>
          <Field Name="Business Phone">91.24.45.40</Field>
        </Row>
        <Row>
          <Field Name="ID">4</Field>
          <Field Name="Last Name">Ashworth</Field>
          <Field Name="First Name">Victoria</Field>
          <Field Name="Company">B's Beverages</Field>
          <Field Name="Business Phone">(171) 555-1212</Field>
        </Row>
        <Row>
          <Field Name="ID">5</Field>
          <Field Name="Last Name">Mendel</Field>
          <Field Name="First Name">Roland</Field>
          <Field Name="Company">Ernst Handel</Field>
          <Field Name="Business Phone">7675-3425</Field>
        </Row>
      </Rows>
    </Data>
  </ListInstance>

  <!-- Provision the page to display the contacts -->
  <Module Url="MySitePages" >
    <File Url="Contacts.aspx" Type="Ghostable" />
  </Module>

  <!-- Add the menu option that links to Contacts.aspx -->
  <CustomAction
    Id="SiteActionsToolbar"
    GroupId="SiteActions"
    Location="Microsoft.SharePoint.StandardMenu"
    Sequence="100"
    Title="Contacts"
    Description="A page showing some sample data">
    <UrlAction Url="~site/MySitePages/Contacts.aspx"/>
  </CustomAction>

</Elements>
```

来自 elements.xml 的代码片段

你可以添加许多类型的元素，远不止本章所能涵盖的。这里使用的三种（ListInstance、Module 和 CustomAction）是最常见的。可以在 SharePoint Foundation SDK 的这一部分找到更多信息：http://msdn.microsoft.com/en-us/library/ms414322(office.14).aspx

元素定义的一个重要方面是使用通常称为魔术数字和字符串的东西。这些是具有特定含义的硬编码值。例如，字符串“FF0000”在某些上下文中用于表示颜色红色。在 CAML 中使用魔术字符串和数字是很常见的。

前面的文件演示了两个示例。首先，ListInstance 元素中 FeatureId 和 TemplateType 的组合指示你希望创建的列表类型。其次，CustomAction 元素中 GroupId 和 Location 属性的组合指示菜单选项或链接将在 SharePoint 站点中的何处放置。

要创建的最后一个文件是用于显示联系人列表数据的页面。这是一个标准的 ASP.NET 内容页面，它将填充站点默认母版页中的两个内容占位符。它将使用 SharePoint 特定的 ASP.NET DataSource 和 GridView 控件的版本来检索和显示来自联系人列表的数据。

SPDataSource 专门设计用于处理来自 SharePoint 列表的数据，而 SPGridView 设计用于尊重 SharePoint 站点中使用的 CSS 样式。一起使用这些控件提供了一种简单、无代码的方法来展示来自 SharePoint 站点的数据。

创建一个名为 Contacts.aspx 的文件，添加以下代码，并将其保存到 SimpleFeature 文件夹：

```
<%@ Assembly Name="Microsoft.SharePoint, Version=14.0.0.0, ..." %>

<%@ Page MasterPageFile="~masterurl/default.master" meta:progid="SharePoint.WebPartPage.Document" %>

<%@ Register TagPrefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=14.0.0.0, ..." %>
<asp:Content runat="server" ContentPlaceHolderID="PlaceHolderPageTitle">
    Contacts
</asp:Content>
<asp:Content runat="server" ContentPlaceHolderID="PlaceHolderMain">
    <h3>Contacts</h3>
    <SharePoint:SPDataSource runat="server"
        ID="ContactsDataSource" DataSourceMode="List"
        UseInternalName="false">
        <SelectParameters>
            <asp:Parameter Name="ListName" DefaultValue="Contacts" />
        </SelectParameters>
    </SharePoint:SPDataSource>
    <SharePoint:SPGridView runat="server"
        ID="ContactsGridView" DataSourceID="ContactsDataSource"
        AutoGenerateColumns="false" RowStyle-BackColor="#DDDDDD"
        AlternatingRowStyle-BackColor="#EEEEEE">
        <Columns>
            <asp:BoundField HeaderText="Company"
                HeaderStyle-HorizontalAlign="Left" DataField="Company" />
            <asp:BoundField HeaderText="First Name"
                HeaderStyle-HorizontalAlign="Left" DataField="First Name" />
            <asp:BoundField HeaderText="Last Name"
                HeaderStyle-HorizontalAlign="Left" DataField="Last Name" />
            <asp:BoundField HeaderText="Phone"
                HeaderStyle-HorizontalAlign="Left" DataField="Business Phone" />
        </Columns>
    </SharePoint:SPGridView>
</asp:Content>
```

来自 Contacts.aspx 的代码片段

## 手动部署和安装功能

现在你已经准备好了所有文件，需要部署该功能。我们将首先查看一种手动技术，后面你将学习如何正确打包功能以进行生产部署。手动部署是一个两步过程：

1. 将功能文件复制到 SharePoint 系统文件夹。
2. 安装功能。

SharePoint 系统文件夹位于系统根目录下，位于 C:\Program Files\Common Files\Microsoft Shared\web server extensions\14\.（你可能会听到它被称为“14 Hive”，尽管 Microsoft 和 SharePoint 社区正在远离使用该术语。）在系统文件夹中存储的是跨整个场通用的文件，其中包括定义功能的那些文件。在本章的其余部分，[14] 的简写形式将用于表示系统根目录的路径。

功能存储在 [14]\TEMPLATES\FEATURES 中。每个功能都有自己的子文件夹，其中包含功能和元素清单以及其他支持文件。部署示例功能的第一个步骤是将 SimpleFeature 文件夹复制到此处。使用 Windows 资源管理器（或其他技术）执行此操作。

要安装功能，请打开 SharePoint 2010 管理 Shell 并输入以下命令，该命令是从 [14]\TEMPLATES\FEATURES 到包含功能清单的文件夹的相对路径：

```
Install-SPFeature -path SimpleFeature
```

## 激活功能

现在你可以激活示例功能了。导航到你之前创建的团队站点（http://localhost/sites/demo）并从“站点操作”菜单中选择“网站设置”>“管理网站功能”。

