# ON THE WEB

The starting database for this walkthrough, Chapter23.accdb, can be downloaded from this book's website.

If you haven't done so, you'll want to explore Chapter 22. There, you'll get the foundation needed to better understand the terms and features you'll see in this chapter.

# Introducing Data Macros

A data macro is logic you attach to a table to enforce business rules at the table level. In some ways, a data macro is similar to a validation rule, except that a validation rule is rather unintelligent. Validation rules can't modify data or determine whether corrective action is needed. Data macros are specifically provided to allow you to manage data-oriented activity at the table level.

Data macros are intended to make it easier to ensure consistent data handling throughout your application. Because data macros are applied at the table level, the exact same action happens each time the table's data is updated. Although the subset of actions available to data macros is considerably smaller than standard macros, when carefully crafted and implemented, data macros are a powerful addition to Access applications.

# NOTE

Data macros are especially handy in split database applications (applications where the tables live in a separate Access file from the forms and reports). Because the macros are attached to the tables, they continue to work even if someone links to the tables in some other way than the designed front-end application.

# Understanding Table Events

There are five different macro-programmable table events: BeforeChange, BeforeDelete, AfterInsert, AfterUpdate, and AfterDelete.

To see these events in the Ribbon, open the Chapter23.accdb database and open tblProducts in Datasheet view. On the Ribbon, you'll see a Table tab. Select that tab and you'll see the events shown in Figure 23.1: BeforeChange, BeforeDelete, AfterInsert, AfterUpdate, and AfterDelete.

These events are designated as "before" and "after" events. The "before" events occur before changes are made to the table's data, while the "after" events indicate that successful changes have been made.