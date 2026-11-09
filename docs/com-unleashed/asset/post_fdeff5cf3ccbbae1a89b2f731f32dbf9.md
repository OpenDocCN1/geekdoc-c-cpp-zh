
### LISTING 17.2 The Visual Basic Client Application That Uses the Simple Transaction Component

```
Private Sub Command1_Click()
    Label2.Caption = "Executing Transaction"

    Dim obj As Object
    Set obj = CreateObject("SimpleTrans.First.1")

    Res = obj.DoIt()

    Label2.Caption = "Result of DoIt():" & obj.TransactionResult

    Set obj = Nothing

End Sub
```

## 17 COM+ AS A TRANSACTION COORDINATOR

The component has a class named CFirst with a method named DoIt() that does the work. The first thing that happens in the DoIt() method is GetObjectContext() is called. The object context must be obtained in order to either commit (with SetComplete()) or abort (with SetAbort()) the transaction.

Some error checking comes next to make sure the IObjectContext pointer was retrieved without an error. We wouldn't want to perform operations on a NULL or invalid IObjectContext pointer.

For this example, the decision to commit or abort is based on the system time. If the system time returns a minute that's an even number, the transaction succeeds. If the minute is an odd number, the transaction aborts.

In order to commit the transaction, a simple call to SetComplete() is made. To abort, a call to SetAbort() is made. The IObjectContext is freed with a call to Release(), and the method then returns to the caller.

Notice that a CString class member named m_strTransactionResult is set during the method so that the calling program can easily get a text string describing the outcome of the method call.

The Visual Basic program (Listing 17.2) is easy to understand. It simply instantiates the component, calls the DoIt() method, and then sets a label in the form with the result string.

It's very important to note here that in order for this to work, the component must be in the COM+ catalog as part of an application. Its attributes must also be set correctly. I talk about setting COM+ component attributes later in the chapter.

### Transaction Protocols

Of course, transactions have been around a long time and have cropped up somewhat independently on various platforms. This complicates matters somewhat. The COM+ programming environment provides support for several different transaction protocols, discussed in the next sections.

### OLE Transactions

Microsoft bases almost all its services and architectures on COM these days. Thus COM is the basis for the OLE transaction standard. OLE transactions are native to MS DTC, SQL Server, and just about any other transactional Microsoft product.

### XA Transactions

The X/Open UNIX standards body promotes its XA transaction standard. XA transactions are used extensively in many distributed environments, especially UNIX. Because this is the preferred transaction mechanism used by some of the largest database companies in the world (Oracle, Informix, Sybase, and others), it would be a tragedy to leave out XA transaction support in any product seeking to become the enterprise-enabling, transactional component runtime of the millennium. Thus DTC supplies support for XA transactions.

As you might have guessed, there is, regrettably, a little more to it than that. Because Microsoft is more inclined to integrate and fully test the services of SQL Server than, say, Oracle 8, XA transaction configuration can take some work. Be sure to examine the COM+ Help system supplied with your version to ensure that you have the correct driver revisions before attempting to use XA transactions in a COM+ system. The TestOracleXAConfig.exe command line utility enables you to check for correct Oracle database transaction support. Check your database vendor’s Web site and the Microsoft Web site for the latest support.

### CICS and IMS Transactions

Okay, now you’re moving into alien territory. Not only do mainframes support their own unique transaction protocols, but they often also operate in a completely different network infrastructure. They were here first, so you can’t blame them for that. Mainframes are the center of the transaction processing world because of their legendary reliability. So it really would be nice to allow a slick Web-based client that calls a component running in a COM+ middle-tier server to interact with the big iron. Fortunately, DTC supports LU 6.2 Sync Level 2, and with the help of SNA Server and COMTI, transactions can be distributed into the mainframe environment. Chapter 19, “The COM Transaction Integrator,” discusses the nature of CICS and IMS transaction integration with COM+.

### The COM+ Transaction Programming Model

One of the greatest things about the COM+ transaction programming model is that most things are automatic, and those that aren’t are pretty darn easy to code. Once again, COM+ comes through with a very complex set of services in an easy-to-use package; however, certain rules remain invariant no matter how easy the programming task becomes. In fact, it’s very easy to build a really bad COM+ component. In light of this fact, take a hard look at design issues as you work your way through the programming features and the design-specific section at the end of the chapter.

The basic design premise to consider when structuring your components is that transactions are expensive. Avoid them if you can. If you can’t avoid transactions, keep your transactions as fine-grained as possible. Reserving expensive resources for extended periods of time only exacerbates the transactional overhead. This means that you should complete all transactions as quickly as you can.

Here’s a sketch of a typical COM+ transaction sequence:

1. A client calls a transactional COM+ object method.
2. COM+ receives the call and allocates a DTC transaction to attach to the object’s context. It then forwards the call to the object, creating and activating the object if necessary.
3. The object method performs a behavior, invoking the services of other objects and resource managers, which are automatically enlisted in the transaction.
4. Upon completion the object assesses the results of the various functions and either commits or aborts the transaction. (Resource managers subsequently make permanent or roll back the transactional changes.)
5. The object returns status to the client, and COM+ deactivates the object.

This execution sequence, which is illustrated in Figure 17.1, demonstrates one of the most powerful features of component-based transactions. Each of the objects involved in the transaction performs its task in a well-encapsulated way. The calling component does not need details regarding the implementation of the objects it calls. Should the called object make transactional updates to a resource manager, those updates are automatically enlisted in the existing transaction. This automatic transaction propagation ensures that fragments of the overall operation fail or succeed with the whole, regardless of the base object’s knowledge of the subordinate object’s specific behavior.

![](img/112c2326f49d26b8d59aa054e14c5747_477_0.png)

### Creating Transactions

Creating transactions in COM+ is most often a declarative process. You can generate transactions procedurally, but this is not generally necessary. Transactions are automatically created by COM+ in much the same way that transactions automatically propagate from object to object and from object to resource manager. Usually the only manual part of the process is the final step in which the object chooses to commit or abort the operation.

This sometimes happens behind the scenes depending on the Resource Dispenser (RD) in question. Some RDs expose this functionality in their own API. (ODBC simply added support behind the scenes of such calls as `::SQLConnect()`, `::SQLDriverConnect()`, and so on.) Other RDs require that you explicitly enlist in a transaction.

### Automatic Transactions

Automatic transactions are created or propagated by COM+ any time a method of a transactional object is invoked. The one exception to this rule occurs when a transactional object retains a transaction for more than one method call. In this case, successive calls use the existing transaction. Objects can be configured to use transactions through the Component Management Console. Simply right-click the class in question and choose properties. The Transactions tab of the Class Properties dialog box supplies the five transaction settings listed here (see Figure 17.2):

- Disabled
- Not Supported
- Supported
- Required
- Requires New
