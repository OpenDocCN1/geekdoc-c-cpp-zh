program gets to a position where it just can't continue (perhaps a file cannot be opened or an input value makes no sense) it can give up and "throw" an exception:

```
throw new Exception("Oh Dear");
```

The Exception object contains a Message property that is a string which can be used to describe what has gone wrong. In the above example the message would be set to "Oh Dear".

If the exception is not "caught" the program will end at that point. You can make a program respond to exceptions by enclosing code that might throw an exception in a try - catch construction. When the exception is thrown the program transfers execution to the code in the catch clause:

```
try
{
    // code that might throw an exception
}
catch (Exception e)
{
    // code that is obeyed if an exception is thrown
    // e is a reference to the exception that was thrown
}
finally
{
    // code in here is always obeyed, whether the exception
    // was thrown or not
}
```

A try – catch construction can also contain a finally clause, which contains code that is executed whether or not the exception is thrown.

# Functional Design Specification

Large software developments follow a particular path, from the initial meeting right up to when the product is handed over. The precise path followed depends on the nature of the job and the techniques in use at the developer, however, all developments must start with a description of what the system is to do. This is the most crucial item in the whole project, and is often called the Functional Design Specification, or FDS.

# Globally Unique Identifier (GUID)

This is something which is created with the intention of it being unique in the world. It gives an identifier by which something can be referred to. GUID creation involves the use of random values and the date and time, amongst other things. GUIDs are used for things like account references and tags which must be unique. Many operating systems and programmer libraries provide methods which will create GUIDs.

# Hierarchy

A hierarchy is created when a parent class is extended by a child to produce a new class with all the abilities of the parent plus new and modified behaviours specific to the requirements of the child. Extending the child produces a further level of hierarchy. The classes at the top of the hierarchy should be more general and possibly abstract (for example BankAccount) and the classes at the lower levels will be more specific (for example Ch11dBankAccount).

# Immutable

An immutable object cannot be changed. If an attempt is made to change the content of an immutable object a new object is created with the changed content and the "old" one