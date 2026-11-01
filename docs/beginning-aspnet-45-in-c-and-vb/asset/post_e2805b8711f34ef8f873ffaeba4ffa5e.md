
5. Back in the page, the ListView should still appear as a plain rectangle, shown in Figure 14-14, because you haven't provided any template information yet.

![](img/eadab2ccd79b253c01a3fdff2321202d_573_0.png)

FIGURE 14-14

6. On the Smart Tasks panel of the ListView, choose Configure ListView. (If you don't see this link, click Refresh Schema first and reopen the Smart Tasks panel.) A dialog box appears that enables you to choose the layout of the control, a style, and whether or not you want to enable operations such as inserting and updating. Choose Bulleted List as the layout, and check the Enable Inserting and Enable Deleting items so your dialog box ends up as shown in Figure 14-15.

![](img/eadab2ccd79b253c01a3fdff2321202d_573_1.png)

FIGURE 14-15

```
<br />
<asp:Button ID="DeleteButton" runat="server" CommandName="Delete" Text="Delete" />
</li>
```

11. Repeat the previous step for the InsertItemTemplate that is also part of the ListView control's markup.

Compare your code with the following code and make any changes if necessary. Check if your ListView has a DataKeyNames property set to Id and add it if it isn't there. Sometimes VS doesn't add this property, although the code requires it to be there. Also check that the templates contain the correct controls. The order of the templates or the white space can be different in your code.

```
<asp:ListView ID="ListView1" runat="server" DataKeyNames="Id"
    DataSourceID="EntityDataSource1" InsertItemPosition="LastItem">
    <InsertItemTemplate>
        <li style="">
            Description:
            <asp:TextBox ID="DescriptionTextBox" runat="server"
                Text='<%# Bind("Description") %>' /> </br />
            ToolTip:
            <asp:TextBox ID="ToolTipTextBox" runat="server"
                Text='<%# Bind("ToolTip") %>' /> </br />
            ImageUrl:
            <asp:TextBox ID="ImageUrlTextBox" runat="server"
                Text='<%# Bind("ImageUrl") %>' /> </br />
            <asp:Button ID="InsertButton" runat="server"
                CommandName="Insert" Text="Insert" />
            <asp:Button ID="CancelButton" runat="server"
                CommandName="Cancel" Text="Clear" />
        </li>
    </InsertItemTemplate>
    <ItemTemplate>
        <li style="">
            Description:
            <asp:Label ID="DescriptionLabel" runat="server"
                Text='<%# Eval("Description") %>' /> </br />
            ToolTip:
            <asp:Label ID="ToolTipLabel" runat="server"
                Text='<%# Eval("ToolTip") %>' /> </br />
            ImageUrl:
            <asp:Label ID="ImageUrlLabel" runat="server"
                Text='<%# Eval("ImageUrl") %>' /> </br />
            <asp:Button ID="DeleteButton" runat="server"
                CommandName="Delete" Text="Delete" />
        </li>
    </ItemTemplate>
    <LayoutTemplate>
        <ul class="ItemContainer">
            <li ID="itemPlaceholder" runat="server" />
        </ul>
    </LayoutTemplate>
</asp:ListView>
```

12. Switch back to Design View, select the EntityDataSource control, and open its Properties Grid. Switch to the Events tab and double-click the Inserting event. At the top of the page add an

Imports or a using statement for the PlanetWroxModel namespace, as you did in the other pages in this chapter. Then in the event handler that VS added for you, write the following code:

### VB.NET

```
Protected Sub EntityDataSource1_Inserting(sender As Object,
    e As EntityDataSourceChangingEventArgs) Handles EntityDataSource1.Inserting
    Dim photoAlbumId As Integer = Convert.ToInt32(Request.QueryString.Get("PhotoAlbumId"))
    Dim myPicture As Picture = CType(e.Entity, Picture)
    myPicture.PhotoAlbumId = photoAlbumId
End Sub
```

### C#

```
protected void EntityDataSource1_Inserting(object sender,
    EntityDataSourceChangingEventArgs e)
{
    int photoAlbumId = Convert.ToInt32(Request.QueryString.Get("PhotoAlbumId"));
    Picture myPicture = (Picture)e.Entity;
    myPicture.PhotoAlbumId = photoAlbumId;
}
```

13. Add the following CSS code to Monochrome.css in the Monochrome theme's folder and save the file:

```
.ItemContainer
{
    width: 600px;
    list-style-type: none;
    clear: both;
}

.ItemContainer li
{
    height: 300px;
    width: 200px;
    float: left;
}

.ItemContainer li img
{
    width: 180px;
    margin: 10px 20px 10px 0;
}
```

14. Add the same code to DarkGrey.css in the DarkGrey theme's folder, but this time set the width of the ItemContainer class to 400px like this:

```
.ItemContainer
{
    width: 400px;
    list-style-type: none;
    clear: both;
}
```

15. Save all your changes, close all open files, and then request `NewPhotoAlbum.aspx` in your browser. Make sure you don't accidentally open `ManagePhotoAlbum.aspx`, because it requires a query string that is sent by `NewPhotoAlbum.aspx`. Enter a new name for the photo album and click Insert. You're taken to `ManagePhotoAlbum.aspx` where you can enter new pictures. For now, all you can do is enter the description of the picture, the tooltip, and a fake URL of the image (just enter some text); you see later how to modify this and let a user upload real pictures to the website. Once you click the Insert button, a new item appears in the list, next to the insert controls. Add a few more items and you'll notice that the insert controls move to a row below the others, as shown in Figure 14-16, which shows the page in Firefox.

![](img/eadab2ccd79b253c01a3fdff2321202d_577_0.png)

FIGURE 14-16

16. Click the Delete button for an item and see how the item is removed from the list automatically.

17. If you're currently viewing the site in the Monochrome theme, use the drop-down list to switch to DarkGrey. Notice that this theme shows only two images per row instead of the three displayed by the Monochrome theme shown in Figure 14-16.

## How It Works

You started this exercise by attaching an `EntityDataSource` control to the `ListView` control. The `EntityDataSource` is configured to work with the `Pictures` entity set. As you saw earlier, each picture

## 蚂蚁集团智能运营平台的实践

导读：本文整理自蚂蚁集团高级技术专家、蚂蚁智能运营负责人剑璘，在 ArchSummit 全球架构师峰会（深圳站）上所做的以智能运营平台实践为主题的分享。

> > 在运维领域，突发的故障很难完全避免，关键是如何快速发现、快速响应、快速恢复，把损失降到最低。

今天我的分享集中在三个方面：首先回顾一下过去几年蚂蚁运维体系的演进过程；其次介绍我们当前对智能运维的理解，以及怎样把算法平台和运维场景结合得更好；最后是未来演进方向上的一些思考。

### 蚂蚁运维体系的演进

蚂蚁的运维体系发展经历了几个重要阶段。从最早的人肉运维，到工具化、平台化，再到现在的智能化运维，每一步都是伴随着业务体量的增长和技术栈的复杂化而演进的。

在早期阶段，运维主要依赖人工经验和脚本处理，效率较低且容易出错。随着业务规模扩大，我们逐步构建了标准化的运维工具链，将常见操作固化到平台中，提升了整体的运维效率。

### 智能运维的实践

目前我们正在推进的智能运维体系，核心是将算法能力与运维场景深度结合。通过时序预测、异常检测、根因分析等算法能力，帮助运维人员更快地发现问题、定位问题、解决问题。

- 5. Inside the ItemTemplate template of the ListView, locate the Eval statement for the Description Label and change it from Eval("Description") to Item.Description. You should end up with this code:
- 6. Repeat step 5 for the ToolTip Label. Again, the ImageUrl gets special treatment later in this chapter, so there's no point in changing it now.
- 7. Save your changes and request NewPhotoAlbum.aspx in the browser. Insert a new album and then add a few pictures by entering a description and tooltip and uploading an image file. Notice how the code still behaves as before.

```
<asp:Label ID="DescriptionLabel" runat="server"
    Text='<%# Item.Description%>' />
```

## How It Works

You didn't have to change a lot to make the ListView strongly typed and get access to IntelliSense and compile-time checking of your code. All you had to do was add an ItemType property to the ListView and replace the calls to Bind and Eval with their BindItem and Item counterparts. With these changes in place, the control behaves exactly as before. At run time, the control looks at the value of the assigned properties and displays them in the browser. When you submit data back to the server, the reverse takes place: The values you entered in the controls are assigned to the properties of an instance of the Picture object, which is then saved in the database by the Entity Framework. It's recommended to use the strongly typed binding capabilities whenever you can, because they'll help you spot errors much sooner and make it easier to type your code.

Right now, users need to type in a URL for an image manually. Obviously, this isn't very user friendly. It would be much easier for them if they could pick an image from their local computer and upload it to the server. You see how to accomplish this in the next exercise.

## TRY IT OUT Customizing Templates of the ListView Control

The default templates for the ListView control that VS generates based on the information from the EntityDataSource are enough only in the most trivial situations. Usually, you need much more control. For example, in the ItemTemplate you may want to display an actual Image control instead of the plain ImageUrl property as text. Likewise, in the InsertItemTemplate you may want to display a file upload control instead of a simple text box. In this exercise, you see how to change the standard templates so you can incorporate both features. Additionally, you see how to handle the Inserting event of the EntityDataSource control to save the uploaded file to disk, and update the database with the URL of the image.

For this example to work, the account used by the web server (the account you use to log on to your machine if you are using IIS Express) needs read and write permissions to the GigPics folder that you create in this exercise. The account should already have these permissions on your machine, but if you run into problems with this exercise, refer to the section "Understanding Security in IIS" in Chapter 19.

- 1. Create a new folder in the root of the website called GigPics. This folder will contain concert pictures uploaded by users.
