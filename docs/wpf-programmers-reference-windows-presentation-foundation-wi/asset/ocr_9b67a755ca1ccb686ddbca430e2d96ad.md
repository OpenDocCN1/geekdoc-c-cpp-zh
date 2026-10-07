```
</TabItem.Header>
<Grid>
<-- Controls omitted. -->
</Grid>
</TabItem>
</TabControl>
```

RotatedTabs

Figure C-1 shows the result.

![](bbox=[0.066, 0.261, 0.378, 0.451])

FIGURE C-1

# TOOLBAR AND TOOLBARTRAY

The Toolbar displays a series of Buttons, ComboBoxes, and other tools that the user can access easily.
The ToolBarTray displays an area, normally at the top of the window below the menus, that contains one or more ToolBars. The user can drag the ToolBars around within the ToolBarTray. The key properties of ToolbarTray are given in Table C-13.

TABLE C-13:

| PROPERTY | PURPOSE |
|---|---|
| Background | The color used to fill the interior of the control |
| FlowDirection | Determines whether the ToolBars are arranged right-to-left or left-to-right. |
| IsLocked | If True, then the user cannot move ToolBars within the ToolBarTray. |
| Orientation | Determines whether the ToolbarTray arranges the ToolBars horizontally or vertically |

A Toolbar can arrange its ToolBars in various bands. The Toolbar's Band and BandIndex properties determine where a ToolBar initially appears within a ToolBarTray. These properties can be any numeric value. The Toolbar automatically creates bands as needed and arranges the ToolBars within them. The key properties of Toolbar are given in Table C-14.