# LISTING 6.5 Continued

```
<img runat="server" src="~/DynamicData/Content/Images/plus.gif"/>
Insert new item
<asp:DynamicHyperLink>
</div>
</ContentTemplate>
</asp:UpdatePanel>
</asp:Content>
```

The GridView control is configured to allow paging and sorting. It includes a single TemplateField to define a column that displays action links—Edit, Delete, and Details. The actual data columns are generated dynamically by a DefaultAutoFieldGenerator. During page initialization, the DynamicDataManager control sets the ColumnsGenerator property of the GridView with a new instance of the DefaultAutoFieldGenerator class. So, instead of being specified explicitly in page markup, as shown in the example below, the DynamicField instances are created dynamically, based on the metadata information describing properties of the current entity type.

```
<Columns>
<asp:DynamicField DataField="ProductName" />
<asp:DynamicField DataField="UnitsInStock" />
</Columns>
```

Paging functionality is implemented by the GridViewPager control. This is not a built-in ASP.NET control; it is a user control included in the Dynamic Data project templates of Visual Studio and created in the DynamicData\Content folder of your web application when you first create the project.

The QueryableFilterRepeater control, which was discussed in Chapter 5, is used to generate a set of DynamicFilter controls, one for each property that can be filtered using filter templates available in the DynamicData\Filters folder of the web application. Notice that this markup does not specify the DataField property of the DynamicFilter control. This is done automatically when the QueryableFilterRepeater instantiates its ItemTemplate for each filterable property in the entity type. The ID property of the DynamicFilter control has to be "DynamicFilter," which is what the QueryableFilterRepeater looks for by default.

The QueryableFilterRepeater control is associated with the QueryExtender by the DynamicFilterExpression in the page markup. In its turn, the QueryExtender control is associated with the EntityDataSource, which allows the individual filter templates to modify the LINQ query it generates at run time based on the values selected by the user.

Listing 6.6 shows the code-behind file of the List page template, again, cleaned-up to improve readability and highlight important points.