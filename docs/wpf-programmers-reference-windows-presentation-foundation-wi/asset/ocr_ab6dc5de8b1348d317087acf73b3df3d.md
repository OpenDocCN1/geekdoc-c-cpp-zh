This template's ItemsSource attribute makes the TreeView use the Department's Projects-property to build child nodes.

# BINDING MASTER-DETAIL DATA

The OrgChartTreeView example shown in Figure 18-12 displays hierarchical data in a tree-like format, there are other ways to display this kind of data.

For example, the OrgChartMasterDetail example shown in Figure 18-13 lists a list of regions in their upper-left ListBox. When you click on one, the program displays a list of departments in that region. When you select a department, the program displays a list of managers in department. When you select a manager, the program displays a list of employees who report to that manager. The ListBoxes on the right display the same data, except they follow department projects of managers.

![](bbox=[0.095, 0.368, 0.535, 0.636])

Figure 18-13

The OrgChartMasterDetail program starts, it builds the same Region, Department, Manager, Project, and Employee objects used by the OrgChartTreeView program. It then follows the code to make two StackControls use the list of Regions as their DataContexts. The controls they inherit their DataContext values.

```
spByManager.DataContext = regions;
spProject.DataContext = regions;
```

The following code shows how the program defines its first Region ListBox:

```
<ListBox Name="ByManagerRegion" ItemsSource="{Binding}">
  <ListBox.ItemTemplate>
    <DataTemplate>
      <TextBlock Text="{Binding Path=RegionName}" Foreground="Red">
        <TextBlock.BitmapEffect>
          OuterGlowBitmapEffect/>
      </TextBlock>
    </DataTemplate>
  </ListBox.ItemTemplate>
</ListBox>
```