# **TABLE 10-5** *(continued)*

| PROPERTY | DESCRIPTION |
|---|---|
| `Log` | Enables you to specify the output location of the command that was used in the query |
| `Mapping` | Provides the metamodel on which the mapping is based. That is, this defines how the tables will be translated to VB classes. |
| `ObjectTrackingEnabled` | Specifies whether or not to track changes to the objects within the database for transactional purposes. If you are dealing with a read-only database, then you should set this property to false. |
| `Transaction` | Enables you to specify the local transaction used with the database |

# ## The Table(TEntity) Object

The `Table(TEntity)` object is a representation of the tables that you are working with from the database. For instance, you saw the use of the Product class, which is a `Table(Of Product)` instance. As you will see throughout this chapter, several methods are available from the `Table(TEntity)` object. Some of these methods are defined in Table 10-6.

# **TABLE 10-6:** Partial List of Table(TEntity) Object Methods

| METHOD | DESCRIPTION |
|---|---|
| `Attach` | Enables you to attach an entity to the DataContext instance |
| `AttachAll` | Enables you to attach a collection of entities to the DataContext instance |
| `DeleteAllOnSubmit(TSubEntity)` | Enables you to put all the pending actions into a state of readiness for deletion. Everything here is enacted when the SubmitChanges method is called off of the DataContext object. |
| `DeleteOnSubmit` | Enables you to put a pending action into a state of readiness for deletion. Everything here is enacted when the SubmitChanges method is called off of the DataContext object. |
| `GetModifiedMembers` | Provides an array of modified objects. You will be able to access their current and changed values. |
| `GetNewBindingList` | Provides a new list for binding to the data store |
| `GetOriginalEntityState` | Provides an instance of the object as it appeared in its original state |
| `InsertAllOnSubmit(TSubEntity)` | Enables you to put all the pending actions into a state of readiness for insertion. Everything here is enacted when the SubmitChanges method is called off of the DataContext object. |
| `InsertOnSubmit` | Enables you to put a pending action into a state of readiness for insertion. Everything here is enacted when the SubmitChanges method is called off of the DataContext object. |

# ## QUERYING THE DATABASE

As you have seen so far in this chapter, there are a number of ways in which you can query the database from the code of your application. In some of the simplest forms, your queries looked like the following:

```
Dim query As Table(Of title) = dc.titles
```

This command retrieved the entire Titles table to your `Query` object instance.