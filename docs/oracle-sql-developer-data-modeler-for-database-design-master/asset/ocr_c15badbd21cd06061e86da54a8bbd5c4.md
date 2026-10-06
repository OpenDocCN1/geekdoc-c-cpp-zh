# 7 Oracle SQL Developer Data Modeler for Database Design Mastery

with that value exist in the child table. The possible choices are No Action, Cascade, Set Null, Restrict.

+   - The value No Action performs no action on these rows, which means the rows must be deleted manually from the child table before they can be deleted from the parent table.

+   - The option Cascade deletes these rows from the child table automatically by Data Modeler deletes the rows from the parent table.

+   - The value Set sets null for all columns in those rows in the child table that can be set to null. If there are columns that cannot be set to null, they must be handled manually.

+   - The value Restrict prevents any updates or deletes on parent table columns referred to from child table.

Deleting a rule has no meaning in the logical model, but this is the right place to find the information needed to be document it. It is good that it can be documented in Data Modeler already in the logical model, and it will be forward engineered to the relational model.

A relationship can have attributes of its own. For example, a relationship between Customer and Order may have an attribute of Date of Purchase. Attributes for relationships can be defined in Relation Properties on the Attributes tab, as shown in Figure 4-11. In the diagram, the relationship attribute is shown in Figure 4-12. The relationship attributes are not shown in a diagram by default. If you cannot see them, right-click the canvas and choose Show | Relationship Attributes.

> NOTEnA common mistake is to model a foreign key as an attribute. Do not do that. If you do, you will end up with duplicate columns in your relational model after forward engineering.

If the relationship does not look the way you want, you can either select and move it or use the Data Modeler functions to move it. You can delete or hide the relationship. You can select Straight Lines, Add Elbow, or Change The Format. If you want to change the way the relationship line looks, select Change Format and change it. You can see all operations allowed for a relationship and a relationship line by right-clicking it in a diagram.