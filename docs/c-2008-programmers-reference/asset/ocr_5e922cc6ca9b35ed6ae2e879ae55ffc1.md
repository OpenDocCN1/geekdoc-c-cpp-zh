# Part II: Application Development Using C#

![](bbox=[0.35, 0.12, 0.65, 0.38])

Figure 18-14

Whenever a node in the TreeView control is selected, you should perform a check to see if it is a posting node and enable/disable the MenuItem controls appropriately (see Figure 18-15):

```
```csharp
//---fired after a node in the TreeView control is selected---
private void TreeView1_AfterSelect(object sender, TreeViewEventArgs e)
{
    //---if a feed node is selected---
    if (e.Node.ImageIndex != ICO_POST && e.Node.Parent != null)
    {
        mnuUnsubscribe.Enabled = true;
        mnuRefreshFeed.Enabled = true;
    }
    else
    {
        //---if a post node is selected---
        mnuUnsubscribe.Enabled = false;
        mnuRefreshFeed.Enabled = false;
    }
}
```
```

![](bbox=[0.2, 0.75, 0.8, 0.95])

Figure 18-15