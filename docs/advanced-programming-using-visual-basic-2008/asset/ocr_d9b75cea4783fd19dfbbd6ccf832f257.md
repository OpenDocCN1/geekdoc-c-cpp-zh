Throughout your programming, you have used a series of collections. List boxes have a collection of items. Tables have a collection of rows and of columns and datasets have collections of tables. In this chapter, you will examine various types of collections such as stacks, queues, dictionaries, hash tables, sorted lists, and array lists. A collection may consist of a group of individual data items or a collection of objects (remember that a data item is an object).

You will find that programmers and programming documentation often use the words collection, list, and data structure interchangeably. For most of the references in this chapter, you can substitute one term for another.

With generics, you create a strongly typed object, such as a procedure or a class, but the type is not defined until the object is instantiated or the procedure called. You will code a generic procedure and create a generic collection class.

# Referencing Collection Items

You have referenced some of the built-in collections of VB all along. You can refer to the individual elements of most collections by either a key (a string value) or an index (the numeric position). For example, to reference an individual table in the Tables collection of a DataSet object:

```
' The Stores table.
PubsDataSet.Tables("Stores")
```

or

```
' Also refers to the Stores table, assuming that it is the first table.
PubsDataSet.Tables(0)
```

or

```
' Also refers to the Stores table by using the bang notation.
PubsDataSet.Tables!Stores
```

# System.Collections Namespace

A collection is a group of objects. The System.Collections namespace provides classes for several different types of collections. When you need to create a collection, you should be aware of the different types available and the strengths and weaknesses of each type. You may need to inherit from a list class or simply select the type of collection that is best for a specific situation. An understanding of the types of collections can make the task easier and the program more efficient.