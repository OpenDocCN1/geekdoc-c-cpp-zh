# Class and Object

![](bbox=[0.176, 0.093, 0.737, 0.125])

Fig. 4.6: Dependency.

| Multiplicity A | Multiplicity B |
| --- | --- |
| class A | class B |

Fig. 4.7: Representation of association in UML.

Figure 4.6 shows how to represent dependency between classes. UML uses a dashed line pointing to the depended upon to represent dependency between classes. In Figure 4.6, class A is the source and class B is the destination, meaning that class A uses class B, or class A depends on class B.

# b) Relationship – Association

Association is used to represent the relationship between objects from different classes. In UML, a line segment is used to represent association between two classes (or the same class). Generally there are multiplicities at both ends of the line segment. Multiplicity is the most important characteristic of association. Multiplicity in one end of a line segment means: each object on the other end of the line segment should interaction with a certain number of objects of the class on this end. Figure 4.7 shows how to represent association in UML.

In Figure 4.7, 'Multiplicity A' decides how many objects in A interact with each object in class B, and it is the same meaning for 'Multiplicity B.' The symbol forms of multiplicity and their meanings are list in Table 4.1.

# c) Inclusion Relation – Aggregation and Composition

Inclusion relation between classes or objects is described by two concepts in UML: aggregation and composition, which belong to a special kind of association. Aggregation in UML means that the relation between classes is that of whole and part, ‘include,’ ‘compose,’ and ‘divided into ... parts’ are all aggregations. A line segment having two end points is an example of aggregation. Aggregation can be further divided into shared aggregation and composition aggregation (abbreviated as composi-

Tab. 4.1: Symbol and Meaning of Multiplicity.

| Symbol | Meaning |
| --- | --- |
| * | Any amount of objects (includes 0) |
| 1 | One object exactly |
| n | N objects exactly |
| 0..1 | 0 or 1 object (means that association is optional) |
| n..m | N objects at least, m objects at most (n, m are integers) |
| 2, 4 | Discrete association (for example 2 or 4) |