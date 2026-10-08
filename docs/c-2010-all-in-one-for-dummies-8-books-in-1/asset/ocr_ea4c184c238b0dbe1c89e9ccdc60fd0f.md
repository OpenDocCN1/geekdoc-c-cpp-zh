# 350 Hiding Behind an Interface

![](bbox=[0.14, 0.1, 0.226, 0.175])

Programmers (I think I can guess which ones) can defeat my little ploy with a simple cast:

RobzillamyKillazilla = (Robzilla)myzilla;

Doing so is quite a bad idea, the interface has a purpose. Bill Wagner says, "Programmers who go to do much work create bugs what they deserve."

In real life, programmers sometimes use this hand-out-interface technique to interact with the complex DataSet class used in ADO.NET. DataSet can return a set of database tables with records — such as a table of Customers and a table of Orders. (Modern relational databases, as Oracle and SQL Server, contain tables linked by various relationships. each table contains lots of records, where each record might be, for example, the name, and serial number of a Customer.)

Unfortunately, if you hand a client a DataSet reference (even through a read-only property's get clause), he can easily mislead the situation that you reaching into the DataSet and modifying elements that you don't want modified. One way to prevent such mischief is to return a DataView object, which is read-only. Alternatively, you can create a C# interface to expose a safe subset of the operations available on the DataSet. Then you subclass DataSet and the subclass (call it MyDataSet) implement the interface. Finally, give clients a way to obtain an interface reference to a live MyDataSet object and let them have it in relative safety — through the interface.

![](bbox=[0.14, 0.59, 0.226, 0.675])

You usually shouldn't return a reference to a collection, either, because it itself alters the collection that you hand out can still point to the original collection inside your class. Remember that your List<T>... provides an AsReadOnly() method. This method returns a collection that can't be altered:

```
private List<string> readWriteNames = ... // A modifiable data member
ReadOnlyCollection<string> readonlyNames = readWriteNames.AsReadOnly();
return readonlyNames; // Safer to return this than readWriteNames.
```

Although it doesn't qualify as using an interface, the purpose is the same.

![](bbox=[0.14, 0.795, 0.226, 0.88])

The HidingBehindAnInterface example on this book's Web site shows the Robzilla code in this section.