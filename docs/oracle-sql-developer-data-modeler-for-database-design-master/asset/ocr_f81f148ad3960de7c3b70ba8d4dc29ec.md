# 72 Oracle SQL Developer Data Modeler for Database Design Mastery

type is a verb. A relationship set is a subset of a relationship type, and it includes only those relationships that belong to the target of modeling. In spoken language, relationship types and relationship sets are often called relationships. In this book, we call a relationship type and a relationship set a relationship because in the context of Data Modeler's what they are called. You can create a relationship in Data Modeler on the logical model canvas by using one of the relationship icons in the toolbar (the green arrows).

A complex relationship usually demands more investigation. An ER model is only two-dimensional, and having a complex relationship does not fit into that without raising questions. Figure 4-9 shows an example of a complex relationship. A Customer is ordering a Product that has been supplied by a Supplier. Can any of the Suppliers supply any of the Products? Can a Customer order any Products from a product list, or are there limitations (the age of a Customer, for instance?) The ER model does not answer these questions unless the solution has been decided upon based more questions.

A relationship has participation constraints: It can be mandatory (total) or optional (partial). In Data Modeler, you will define the participation constraints in the Preferences dialog on the Logical tab. If you want the source side of the relationship to be optional, select the Source Optional property; otherwise, disable it. The Target Optional property defines the same thing for the target side of the relationship.

A relationship has cardinality constraints (mapping cardinality, cardinality ratio) to describe the number of entity instances this entity has in a relationship. For

![](bbox=[0.165, 0.615, 0.833, 0.855])

FIGURE 4-9. Example of a complex relationship