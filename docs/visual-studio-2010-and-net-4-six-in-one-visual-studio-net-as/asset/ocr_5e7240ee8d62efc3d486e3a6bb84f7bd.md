| FILE | DESCRIPTION |
|---|--|
| ManyToMany_Edit.ascx | Enables users to edit fields that have a many-to-many relationship in a pure join table and the application's data model is based on ADO NET Entity Framework. LINQ to SQL doesn't support many-to-many relationships. |
| Text.ascx | Uses a Literal to display string and many numeric data types. |
| Text_Edit.ascx | Uses a TextBox control (with its TextMode set to SingleLine) to enable edit single-line text. It also renders a RegularExpressionValidator control when the data model defines a RegularExpression attribute. The MaxLength property of the TextBox control is enforced according to the maximum length defined in the data model. |
| Url.ascx | Uses a HyperLink to display URLs. |

By default, Dynamic Data uses the edit-mode field templates for the insert mode when doesn't find a user control defined with the _Insert.ascx suffix.

# # Working with Entity Templates

Entity templates are user controls that allow you to customize the layout for a table. They are user controls derived from the EntityTemplateUserControl class (System.Web.DynamicData.EntityTemplateUserControl). The default entity templates display the fields in a two-column table — one column for the field name, and the other for the field values.

Dynamic Data provides three entity templates, in the DynamicData/EntityTemplates folder. They are included in the page templates that define the different operations, as shown in Table 17-7.

| FILE | INCLUDED IN THE TEMPLATE |
|---|--|
| Default.ascx | Details.ascx |
| Default_Edit.ascx | Update.ascx |
| Default_Insert.ascx | Insert.ascx |

**TABLE 17-7:** Entity Templates

The combined-page mode ListDetails.ascx page template will also use the three entity templates. The entity templates use the previously explained field templates to display the fields. The page templates display the corresponding entity template using the DynamicEntity control and replacing it with the appropriate entity template at run-time.