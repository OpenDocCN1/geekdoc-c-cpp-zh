# A TreeView control

![](bbox=[0.12, 0.095, 0.325, 0.34])

# The aspx code for the TreeView control shown above

```
<asp:TreeView ID="TreeView1" runat="server"
    DataSourceID="SiteMapDataSource1"
    ShowLines="True">
</asp:TreeView>
```

# Attributes of the TreeView control

| Attribute | Description |
|---|---|
| ID | The ID of the control. |
| Runat | Must specify "server". |
| DataSourceID | The ID of the SiteMapDataSource control the tree should be bound to. |
| ExpandDepth | The number of levels to be automatically expanded when the tree is initially displayed. The default is FullyExpand. |
| MaxDepthDataBind | Limits the maximum depth of the tree. The default is -1, which places no limit. |
| NodeIndent | The number of pixels to indent each level. The default is 20. |
| NodeWrap | Set to True to word-wrap the text of each node. The default is False. |
| ShowExpandCollapse | Set to False if you want to hide the Expand/Collapse buttons. The default is True. |
| ShowLines | Set to True to include lines that show the hierarchical structure. The default is False. |

# Description

+   - The TreeView control is used to display the site map in a hierarchical tree.
+   - To display an application’s navigation structure, the TreeView control must be bound to a SiteMapDataSource control as described in the next figure.