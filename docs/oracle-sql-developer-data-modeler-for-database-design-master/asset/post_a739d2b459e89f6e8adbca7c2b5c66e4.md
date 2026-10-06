
## Chapter 4: Introducing Conceptual Database Design (Logical Model) 63

TIP
Try not to be too smart and make too complex a solution; remember that usually a simple solution is the best.

During the conceptual database design, you do not need to actively worry about normalizations, and so on, but remember the relational theory why it will help you. The important thing is to model the target as well as possible and yet enough so that other people can understand it too. It is important to find and model the concepts and how they are related to each other. Try to document everything you hear and learn. Be systematic in modeling. Decide where and how to document and figure out the right level of documentation. Make sure you have clear and easily understood for commenting and reviewing.

You should start modeling with the logical model you made during requirements analysis (Chapter 3). If you do not have anything from the requirements analysis, you must start from scratch and begin with the conceptual database design described in this chapter. At best, that means more work; it might even mean you don't have enough information to make the right modeling decisions.

A logical model consists of entities, relationships, views, inheritances, subviews, and displays. All logical model objects are displayed in the Browser pane under Logical Model. One logical model consists of one logical diagram and possibly one or more subviews and/or displays.

If you right-click Logical Model in the Browser pane, you will see the operations for a logical model.

- With Hide and Show, you can control whether the logical model diagram is open.
- You can create subviews and displays based on the logical model (more about those later in this chapter).
- You can set classification types (more about those in Chapter 8).
- You can apply naming standards and custom transformation scripts to create a glossary from the logical model (more about those in Chapter 3).
- You can search and create a report based on search results and update the data in Data Modeler with an Excel worksheet (more about that in Chapter 11).
- You can choose Engineer To Logical Model (more about that in Chapter 5) and of course view and edit the properties.

## Oracle SQL Developer Data Modeler for Database Design Mastery

- In every object in the Browser pane you also have the ability to select Versioning. You can find more about versioning and version control in Chapter 9.

And if you right-click the logical model diagram (or a subview diagram), you can do the following:

- You can undo operations.
- You can define the layout.
- You can define what details will be shown (View Details): All Details, Names Only, or Attributes. You can also specify that classification types (the name of the classification type on an element) or comments be shown.
- You can select the notation.
- You can display a page grid or a grid or make labels (source and target names) and relationship attributes visible in the diagram. You can specify that a legend should be shown. A legend shows the Summary properties in a diagram. All these can be selected under Show.

## An Entity and Its Attributes

An entity is anything that happens to be of the target of modeling, for example, say Heli. Every entity is of some entity type. An entity type is a set of entities (Person) having certain properties in common (Heli, Marko, Patrik, and Matias—like all entities of type Person—have a name). An entity is always a noun (Company, Employee, Customer). An entity is a subset of an entity type, and it includes only those that belong to the target of modeling. In language, entity and entity sets are often called entities. In this book, we will call both entity and an entity set entity because in the context of Data Modeler. When referring to a single entity (Heli) we use the term entity instance. You can create an entity in Data Modeler on the logical model by clicking the entity icon and inserting the properties for the entity, as shown in Chapter 3.

An entity can be strong or weak. A strong entity (for example, Customer) identifies itself without other entities or relationships; strong entities have independent existence. A weak entity (for example, Orderline) depends on other entities to identify it (Order, Customer) and has a mandatory, identifying relationship with them. The weakness of an entity is shown with a horizontal line at the end of the relationship line. You can define it in the Relation Properties dialog by selecting Identifying from the source side of the properties.

## Chapter 4: Introducing Conceptual Database Design (Logical Model) 65

An entity has properties (for example, Person has a name) as mentioned earlier. Those properties are called attributes. An attribute can be atomic, which means it contains only a single value from a certain domain and it cannot be divided into smaller components. For example, Zip Code is an atomic attribute. An attribute can also be a composite attribute, which means it is a combination of two or more attributes that can be atomic or composite. An example of a composite attribute would be Name = First + Lastname. An attribute can be multivalued or set-valued, which means the attribute will have multiple values, but the number of different values can be limited. For example, a Customer can have only three phone numbers: home, work, and mobile. Or an attribute can be a derived attribute. For example, Age can be derived from Date of Birth. For attributes you can find properties in the Attribute Properties dialog, shown in Figure 4-3. You can find it by clicking the

![](img/431f8ac8f273fa89a28377c500ed60d7_91_0.png)

FIGURE 4-3. Attribute Properties dialog, General tab

## Oracle SQL Developer Data Modeler for Database Design Mastery

Properties icon on the Attribute tab of Entity Properties dialog, double-clicking the attribute name, or selecting the attribute in the Browser pane, right-clicking it, and selecting Properties. In the Attribute Properties dialog, you can also define the name for the attribute source in Source Name field and then select the preferred source type from. The allowable values for Source type are empty (no source type), Manual, System, Derived, and Aggregate. If you want to define the formula for the derived or aggregated attribute, enter a description of the formula in Formula Description, as shown in Figure 4-3.

An attribute can be mandatory or optional. If an attribute has been defined as mandatory by selecting Mandatory when creating it, it will be shown on the canvas with an asterisk (*) in front of the attribute name. If an attribute is optional, there will be a small circle (o) in front of the attribute name in Barker notation and nothing in Bachman or Information Engineering notation.

If you right-click an entity on the canvas, you can see operations allowed on entity. You can, instance, do the following:

- Delete the entity totally (Delete Object) or only from the diagram (Delete View).
- Copy the entity.
- Show or hide elements.
- Select Neighbors and create a subview on the entity and its neighbors with CreateSubview From Selected.
- Sort the attributes of the entity.
- Create synonyms. Synonym actually means Create Visual Synonym; in other words, another presentation of an entity on the same diagram. It is not the synonym you might have in your database. It is meant to be used only to make diagrams easy to read. A synonym can have different visibility elements and a different format than the original.

In Data Modeler you can set object names to be unchanging in the properties. This is useful if you want to be nobody accidentally changes the names. For example, if you want to have tables in your design that belong to another schema (another system, and so on), you want them to be show that there is a logical relationship, but you want to prevent anybody from changing their names. A more common reason is that you already have this object in the database, and the name cannot be changed for any reason. You will find this functionality by choosing Tools | Objects Names Administration (Figure 4-4). In the Objects Names Administration dialog, select Fixed for all elements you want to have a fixed name. You can do this for the names of entities, attributes, relationships, identifiers, and views.
