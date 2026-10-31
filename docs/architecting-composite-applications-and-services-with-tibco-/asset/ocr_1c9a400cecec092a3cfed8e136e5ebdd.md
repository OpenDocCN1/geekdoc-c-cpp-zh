![](bbox=[0.18, 0.13, 0.85, 0.45])

Figure A-7: Generalization

# Structure

Structure is an important element of architecture, so you need to know how to indicate structure. In UML, structure can be indicated a number of ways. We have already seen two. One is the inclusion of attributes in a class: Each attribute is a structural element of the class. The other is an association with a role name at the opposite end, particularly when the association is an aggregation or a composition.

# Composite Structure Diagrams

UML has another graphic notation for indicating structure called a Composite Structure Diagram. Each diagram represents the structure of a particular concept. For example, Figure A-8 is a composite structure diagram of the SalesOrder class shown in Figure A-6. The frame around the diagram identifies the concept whose structure is being shown.

Within the frame, the individual elements are known as parts. Each part has a name that is used to identify the part, with the overall concept being the whole. Part names must be unique. The part can indicate the type of object that is allowed to play the part and the allowed multiplicity of those objects. In the example, A SalesOrder has a part called orderedItems of type SalesOrderLineItem, and there may be zero or more instances of SalesOrderLineItem.