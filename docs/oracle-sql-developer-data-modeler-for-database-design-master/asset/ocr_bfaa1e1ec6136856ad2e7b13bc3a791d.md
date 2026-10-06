# 98 Oracle SQL Data Modeler for Database Design Mastery

> NOTE
If you want to see the structured column expanded in a diagram, just right-click the relational diagram and choose View Details | Expand Complex Types.

The transformation rules just explained are shown in Table 5-1 in a more complex form.

| Heading Element in Logical Model | Heading Element in Relational Model |
| --- | --- |
| Entity | Turns into a table. |
| Attribute | Turns into a column. |
| Relationship | Turns into a foreign key constraint. |
| Unique identifier | Turns into a primary key. |
| One-to-many | Columns for the foreign key will be added to the child table; if the relationship is identifying, these new foreign key columns will be added also to the primary key. |
| One-to-one relationship | Columns for the foreign key will be added to the table on the mandatory side of the relationship; if the relationship is identifying, these new foreign key columns will be added to the primary key. |
| Many-to-many relationship | A new table will be created (with the name of the relationship). Columns based on the primary key attributes on each table in the relationship will be added. A primary key for the new table is created based on those columns. Also, new one-to-many relationships are created for both tables involved. |
| Relationship with attributes, one-to-many | Data Modeler adds the attribute as a column to the child table and creates a dependent constraint constraint. |
| Relationship with attributes, many-to-many | A new table will be created (with the name of the relationship). Columns based on primary key attributes on each table in the relationship will be added. A primary key for the new table is created based on those columns. Also, new one-to-many relationships are created for both tables involved. A column for the relationship attribute is created for the new table. |
| Multivalued attribute | There are two choices:
Create a user-defined data type (collection) and use that for the data type for the attribute.
Split the attribute into separate attributes/entities before engineering to the relational model. |

**TABLE 5-1.** Transformation Rules for Engineering to a Relational Model (continued)