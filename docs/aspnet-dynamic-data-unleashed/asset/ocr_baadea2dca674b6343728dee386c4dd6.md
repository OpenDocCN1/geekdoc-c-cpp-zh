If the Mode property is set to Insert, Dynamic Data will also try Insert mode templates in the order shown in Table 4.1.

Notice that in Insert mode, the lookup algorithm breaks the pattern used in Read-only and Edit modes. Instead of trying different template names for Insert mode first, such as `Contact_Insert.ascx`, `Customers_Insert.ascx`, and `Default_Insert.ascx` and then repeating the process with Edit mode, it tries Insert and Edit modes for each template name. This is unfortunate because it makes the lookup algorithm much more confusing and difficult to understand. On the other hand, this twist allows you to reuse Edit mode templates in Insert mode. If it were not in place, the `Default_Insert.ascx` field template would always be used in Insert mode unless you defined `Contact_Insert.ascx` or `Customers_Insert.ascx`.

**TABLE 4.1** Example of Entity Template Lookup

| Mode="Insert" | Mode="Edit" | Mode="ReadOnly" |
|---|---|---|
| `Contact_Insert.ascx` | `Contact_Edit.ascx` | `Contact.ascx` |
| `Contact_Edit.ascx` | `Customers_Edit.ascx` | `Customers.ascx` |
| `Customers_Insert.ascx` | `Default_Edit.ascx` | `Default.ascx` |
| `Customers_Edit.ascx` | `Contact.ascx` |  |
| `Default_Insert.ascx` | `Customers.ascx` |  |
| `Default_Edit.ascx` | `Default.ascx` |  |
| `Contact.ascx` |  |  |
| `Customers.ascx` |  |  |
| `Default.ascx` |  |  |

# Built-in Entity Templates

Out of the box, Dynamic Data projects offer three dynamic entity templates, one for each mode:

+   - `Default.ascx`
+   - `Default_Edit.ascx`
+   - `Default_Insert.ascx`

All three dynamic entity templates generate a table with two columns, where the left column contains Label controls and the right column contains DynamicControl instances. One table row is generated for each scaffolded column in the entity MetaTable. Aside from the Mode property of the DynamicControl, which they set to ReadOnly, Edit, and Insert, respectively, these three entity templates are nearly identical and designed to present a consistent view of the entity in all three different modes.