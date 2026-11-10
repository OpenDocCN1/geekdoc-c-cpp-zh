*Check tables* perform checks on the field input. In most cases, the value table and check table will be same; otherwise, the value table may propose a value as a possible entry and the check table may reject that entry. You can accept the system proposal or maintain any other table as a check table.

+   3. On the Change Foreign Key... screen (see Figure 10.28), you have the following options:

+   - Check Table: Enter the check table name and click Generate Proposal to list the fields of the check table that can be mapped to the foreign key table.
+   - Generic: If you have multiple fields in the foreign key table that match the key fields in the check table, you can select this checkbox to ignore the input validation for the field.
+   - Constant: You can assign a constant value for other fields so that the system will check if the field in the check table has the assigned constant value for the input validations.
+   - Screen Check: Select this checkbox if you want the system to perform input validations for the foreign key field against the check table. Optionally, you can also assign a custom error message.
+   - Semantic Attributes: Optionally, you can maintain semantic attributes while creating the foreign key relationship. These are primarily for documentation purposes.
+   - Foreign Key Field Type: Optionally, the type of foreign key fields can be defined to describe the meaning of the foreign key fields in the foreign key table. There are a few options:
+     - Non-Key Fields/Candidate: Indicates if the fields of the foreign key table are non-key fields that don't uniquely identify the row.
+     - Key Fields/Candidate: Indicates if the fields of the foreign key table are key fields that uniquely identify the row.
+     - Key Fields of a Text Table: If this option is selected, the foreign key table is handled as a text table of the check table. The primary key of the foreign key table must match the check table, plus a language key field with the type LANG should exist. One check table can have only one text table. The entries in the text table are used for input helps for screen fields and other such purposes.