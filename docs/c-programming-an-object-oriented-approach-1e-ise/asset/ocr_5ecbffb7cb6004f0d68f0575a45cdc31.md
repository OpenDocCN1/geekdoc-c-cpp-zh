![](bbox=[0.274, 0.089, 0.806, 0.16])

**Figure 18.1**  Linear collection of objects

# 18.1.1 Objects Relationship

Operations on a collection, as an object of objects, depend on the relationship between the objects in the collection. We normally encounter two general relationships in a collection: linear and nonlinear.

# Linear Collection

A collection may impose a linear relationship between objects in a collection, which means that each object is somehow connected to the previous and next object. Figure 18.1 shows the basic concept of a linear collection.

# Nonlinear Collection

In a nonlinear collection, each object can be connected to a group of objects. We do not have a collection of objects that come one after another. The objects can be related to each other in a tabular relationship, in which an object is connected to two objects in the same row and to two objects in the same column. We can also have a collection in which the objects are related to each other the way branches of a tree are connected. We can have a root and branches, each with a number of objects, in an upside-down tree. Figure 18.2 shows these two types of relationships in a nonlinear collection.

# 18.1.2 Interface versus Implementation

As we discussed in the case of individual objects, we need to think about two aspects of an object in object-oriented programming: interface and implementation. This statement is also true for a collection, which is an object of objects.

# Interface

We learned that the interface of an individual object simply gives the list of operations that we can use without revealing how the object is created and its contents. This is true for both fundamental and user-defined objects. Since a collection is normally implemented as a template entity, we can define the type of the objects in the collection, but how the collection

![](bbox=[0.265, 0.757, 0.815, 0.906])

**Figure 18.2**  Nonlinear collection of objects