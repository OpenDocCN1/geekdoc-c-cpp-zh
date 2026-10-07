# Binding XML

The code starts with a local:Manager element that uses attributes to the object's FirstName, LastName, Extension, and Title properties.

The Manager class has a Reports property that holds an array of Employee objects (XAML doesn't support the List<Employee> data type, so I converted the code-behind definition to arrays for this example.) The XAML code uses the local:Manager.Reports property to an array of Employee objects.

The OrgChart program uses its Windows.Resources to create an array name containing two local:Region objects. It's easy to use this array as a data source for the program's TreeView controls in the following code:

```
<TreeView Name="trvByManager Background="Transparent"
Grid.Row="1" Column="0" ItemsSource={StaticResource regions}">
</TreeView>
```

![](bbox=[0.103, 0.287, 0.163, 0.003363])

![](bbox=[0.823, 0.35, 0.94, 0.365])

The rest of the code's long but not anything straightforward. The program's HierarchicalDataTemplates are exactly the same as those used by the OrgChartTreeView program. You can download it from the project's web to see the remaining details.

> NOT QUITE THE SAME
Although the OrgChartTreeView and OrgChartXml look like they produce the same result, the actual data is slightly different. The OrgChartTreeView program reuses the same objects several times. For example, the employee Alice is in two Manager' Reports controls, is TeamLead for project ACROBAT, and is a TeamMember for that project. The OrgChartTreeView program creates one Employee object to represent Alice and then adds it in all of its locations.
In the OrgChartXml program, I was unable to use the same Employee in multiple places in this manner. This obvious approach would be to create an Employee resource representing Alice and use it in the appropriate places. Unfortunately, if you try this, XAML claims you are trying to add a StaticResourceExtension object to an array that should contain Employees. To avoid this problem, the program uses multiple Employee objects that contain the values for Alice.
If you out how to share objects in this way, let me know at RodStephens@vb-helper.com.

# BINDING XML

The previous two sections explain how to build objects from classes defined in the code-behind and bind them to controls as TreeView. A third approach builds the objects as XML data stored completely in the XAML code.