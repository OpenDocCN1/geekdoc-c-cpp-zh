> NOTE
> Because the EntityUIHintAttribute is applied to entity classes, it has to be accessible from the project where your EDMX (entity model) is defined. As you can tell by looking at the namespace declaration, this attribute is defined in the Unleashed.DataAnnotations project of the sample solution accompanying this book. It is referenced by the DataModel project, which contains the entity model itself.

# Extending Page Templates to Support EntityUIHintAttribute

To support the entity UI hints, you need to extend the built-in page templates that come with Dynamic Data project templates to initialize the UIHint property of the DynamicEntity control programmatically. Similar to other dynamic controls, this task has to be performed in the Init event handler before the control loads the template. You can modify markup of the three built-in page templates—Details, Insert, and Edit, plus the Delete page template created in Chapter 6, to define the Init event handler:

```
<asp:DynamicEntity runat="server" OnInit="DynamicEntity_Init" />
```

Make sure you leave the Mode attribute as is (the Edit and Insert page templates set it to Edit and Insert, respectively). The Init event handler itself is shown next. As you can see, it tries to find the EntityUIHintAttribute in the MetaTable object describing the entity class. If the attribute is found, the code sets the UIHint property of the DynamicEntity control:

```
protected void DynamicEntity_Init(object sender, EventArgs e)
{
    var entityUIHintAttribute = this.table.Attributes
        .OfType<EntityUIHintAttribute>().FirstOrDefault();
    if (entityUIHintAttribute != null)
        ((DynamicEntity)sender).UIHint = entityUIHintAttribute.EntityUIHint;
}
```

# UnleashedEntity Control

You can reimplement the DynamicEntity initialization logic in all four of the dynamic page templates. With a small number of page templates, this will not be a big effort. However, it is always a good idea to avoid code duplication. One of the ways to do it is to create an extended version of the DynamicEntity control, such as the UnleashedEntity in the sample solution. Listing 11.12 shows its source code.