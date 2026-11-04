TreeView: The TreeView is a hierarchical ItemsControl much like Windows Explorer. The nodes (or branches) can be expanded or contracted, giving a nice user interface into any multilevel data. (See Figure 2-20.)

The sample shown in Listing 2-16 (taken from MSDN) uses hard-coded data, but with a simple hierarchical template tree views can be bound just like any other control.

# Listing 2-16: The TreeView XAML

```
<TreeView Name="myTreeViewEvent">
  <TreeViewItem Header="Employee1" IsSelected="True">
    <TreeViewItem Header="Jesper Aaberg"/>
    <TreeViewItem Header="Employee Number">
      <TreeViewItem Header="12345"/>
    </TreeViewItem>
    <TreeViewItem Header="Work Days">
      <TreeViewItem Header="Monday"/>
      <TreeViewItem Header="Tuesday"/>
      <TreeViewItem Header="Thursday"/>
    </TreeViewItem>
  </TreeViewItem>
  <TreeViewItem Header="Employee2">
    <TreeViewItem Header="Dominik Paiha"/>
    <TreeViewItem Header="Employee Number">
      <TreeViewItem Header="98765"/>
    </TreeViewItem>
    <TreeViewItem Header="Work Days">
      <TreeViewItem Header="Tuesday"/>
      <TreeViewItem Header="Wednesday"/>
      <TreeViewItem Header="Friday"/>
    </TreeViewItem>
  </TreeViewItem>
</TreeView>
```

Figure 2-20:
The TreeView.

![](bbox=[0.27, 0.75, 0.45, 0.9])