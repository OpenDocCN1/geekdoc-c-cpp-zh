DAO objects are arranged in a hierarchical fashion. Certain objects are subordinate to other objects, and they can't exist without an instance of their parent object. The top-level DAO object is DBEngine, and all other DAO objects are descendants of DBEngine (see Figure 28.2).

Each of the most frequently used DAO objects is described later in this section.

Generally speaking, the DAO hierarchy closely follows the arrangement of Access database objects. For example, an Access table (which is a TableDef object) contains fields (each of which is a Field object). A field has a set of properties you use to specify the details of its data type, the default value, validation rules, and so on.

# FIGURE 28.2

The DAO object model.

![](bbox=[0.18, 0.52, 0.92, 0.82])

NOTE
For clarity's sake, the set of properties associated with each DAO object is left out of Figure 28.2. But you can safely assume that every object in Figure 28.2 includes a number of properties.