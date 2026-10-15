
# SUMMARY

While Windows Workflow Foundation does not have the visual glitz of WPF or the broad reach of WCF, it is a highly useful addition to the .NET Framework. Most business applications have some need for workflows, and having a standard means of creating this workflow ensures that the workflow is fully featured and accurately reflects business needs. As WF is readily available with the .NET Framework, developers no longer need to recreate a core business rules engine with each application. WF is extensible, so developers can take advantage of it in their applications, without being limited to the designed features.

As with the other components of the .NET Framework, WF integrates well into other applications, including Windows Forms and ASP.NET applications. It provides the means to extract the frequently complex workflow from those applications and to graphically design it. This graphical representation can be used to communicate the process to business users, increasing the chance that the workflow is represented correctly. Finally, as business needs change, it is a simple process to update the workflow, without requiring changes to the core application.

## Enterprise Services

Chapter 28 explored the vast hinterland of legacy software known as COM. This appendix looks at “what COM did next” and how it fits into the world of .NET, in the form of .NET Enterprise Services.

To understand Enterprise Services, you must go back in time (all the way to the last century!) when a number of technologies began to emerge from Microsoft, including Microsoft Transaction Server (MTS), Microsoft Message Queuing (MSMQ), and Microsoft Clustering Services. The aim of these developments was to increase the scalability, performance, and reliability of applications.

Handling transactions involved a considerable extension to the NT/COM runtime. It also involved the introduction of several new standard COM interfaces, some to be used or implemented by transactional components and some to be used or implemented by the underlying resource managers, such as SQL Server. These additions, along with some other innovations relating to areas such as asynchronous COM, came to be known as COM+.

This appendix explores the .NET Enterprise Services. In particular, it looks at transaction processing and queued components using the classes of the System.EnterpriseServices namespace. The System.EnterpriseServices provides a number of classes that wrap the technologies that composed COM+. These include the classes that represent the ObjectContext, and the component interfaces that assist the system in transactions and queuing.

This is an enormous subject that could easily fill a whole book by itself, so this appendix only scratches the surface of it. However, by the end of the appendix, you will understand how all the pieces fit together. Let’s begin by looking at what transactions are, and how they fit into Visual Basic.

### TRANSACTIONS

A transaction is one or more linked units of processing placed together as a single unit of work, which either succeeds or fails. If the unit of work succeeds, then all the work is committed. If the unit fails, then every item of processing is rolled back and the process is returned to its original state.

The standard transaction example involves transferring money from account A to account B. The money must either end up in account B (and nowhere else), or—if something goes wrong—stay in account A (and go nowhere else). This avoids the very undesirable case in which you have taken money from account A but haven’t put it in account B.

### The ACID Test

Transaction theory starts with ACID, an acronym describing the following properties that all transactions should have:

- Atomicity—A transaction is atomic; that is, everything is treated as one unit. However many different components the transaction involves, and however many different method calls are made on those components, the system treats it as a single operation that either entirely succeeds or entirely fails. If it fails, then the system is left in the state it was in before the transaction was attempted.
- Consistency—All changes are done in a consistent manner. The system goes from one valid state to another.
- Isolation—Transactions that are going on at the same time are isolated from each other. If transaction A changes the system from state 1 to state 2, transaction B will see the system in either state 1 or 2, but not some half-baked state in between the two.
- Durability—If a transaction has been committed, the effect is permanent, even if the system fails.

Let’s illustrate this with a concrete example. Imagine that after spending a happy afternoon browsing in your favorite bookstore, you decide to shell out some of your hard-earned dollars for a copy of, yes, Professional Visual Basic 2010 (a wise choice). You take the copy to the checkout and exchange a bit of cash for the book. A transaction is going on here: You pay money and the store provides you with a book.

The important aspect of this transaction isn’t the exchange of money, but that only two reasonable outcomes are possible—either you get the book and the store gets its money or you don’t get the book and the store doesn’t get its money. If, for example, there is insufficient credit on your credit card, then you’ll leave the shop without the book. In that case, the transaction doesn’t happen. The only way for the transaction to complete is both for you to get the book and for the store to get its money. This is the principle of atomicity.

If the store provides you with a copy of some other book instead, then you would reasonably feel that you ended up with an outcome that was neither anticipated nor desirable. This would be a violation of the principle of consistency.

Now imagine that there is one copy of the book in the store, and another potential buyer of that book has gone up to the cashier next to you. As far as the person at the other checkout is concerned, your respective transactions are isolated from each other (even though you are competing for the same resource). Either your transaction succeeds or the other person’s does. What definitely doesn’t happen is that the bookstore decides to exert the wisdom of Solomon and give you half each.

Now suppose you take the book home and the bookstore calls you to ask if they can have the book back. Apparently, an important customer (well, far more important than you, anyway) needs a copy. You would find this a tad unreasonable, and a violation of the principle of durability.

At this point, it’s worth considering what implications all this is likely to have on the underlying components. How can you ensure that all of the changes in the system can be unwound if the transaction is aborted at some point? Perhaps you’re in the middle of updating dozens of database files and something goes wrong.

There are three aspects to rescuing this situation with transactions:

- Knowledge that something has gone wrong
- Knowledge to perform the recovery
- Coordination of the recovery process

The middle part of the process is handled by the resource managers themselves. The likes of SQL Server and Oracle are fully equipped to deal with transactions and rollback (even if the resource manager in question is restarted partway through a transaction), so you don’t need to worry about any of that. The last part of the process, coordination, is handled by the .NET runtime (or at least the Enterprise Services part of it). The first part, knowing that something is wrong, is shared between the components themselves and the .NET runtime.

This isn’t at all unusual: Sometimes a component can detect that something has gone wrong itself and signal that recovery is necessary, while on other occasions it may not be able to do so, because it has crashed.

Later, you will see how all this works as you build a transactional application.

### TRANSACTIONAL COMPONENTS

To understand what components are actually managed by Enterprise Services and what purpose they serve, you need to consider what a typical real-world n-tier application looks like. The bottom tier is the persistent data store, typically a database such as SQL Server or Oracle. However, there are other possible data stores, including the file system (on Windows NT and above). These are termed resource managers because they manage resources. The software here is concerned with maintaining the integrity of the application’s data and providing rapid and efficient access to it.

The top tier is the user interface. This is a completely different specialization, and the software here is concerned with presenting a smooth, easy-to-follow front end to the end user. This layer shouldn’t actually do any data manipulation at all, apart from whatever formatting is necessary to meet each user’s presentational needs. The interesting stuff is in the tiers in between—in particular, the business logic. In the .NET/COM+ transactional model, the software elements that implement this are components running under the control of the Enterprise Services runtime.

Typically, these components are called into being to perform some sort of transaction and then, to all intents and purposes, disappear again. For example, a component might be called into play to transfer information from one database to another in such a way that the information is either in one database or the other, but not both. This component might have a number of different methods, each of which does a different kind of transfer. However, each method call would carry out a complete transfer:

```
Public Sub TransferSomething()
    TakeSomethingFromA
    AddSomethingToB
End Sub
```

Crucially, this means that most transaction components have no concept of state; there are no properties that hold values between method calls. You can see the reason for this if you imagine what would happen if you had a number of instances of the preceding components all vying for the attention of the database. If instance one of the control started the transfer, remembering the state or current values of A and B just after instance two had done the same, you could end up with the state being different between the two instances. This would violate the isolation of the transaction. Persistence is left to the outside data stores in this model.

The business logic is the area of the system that requires all the transactional management. Anything that happens here needs to be monitored and controlled to ensure that all the ACID requirements are met. The neatest way to do this in a component-oriented framework is to develop the business logic as components that are required to implement a standard interface. The transaction management framework can then use this interface to monitor and control how the logic is implemented from a transactional point of view. The transaction interface is a means for the business logic elements to talk to the transaction framework and for the transaction framework to reply to the logic elements.

So what’s all this about not having state? Well, if you maintain state inside your components, then you immediately have a scaling problem. The middle tiers of your application are now seriously resource hungry. If you want an analogy from another area of software, consider why the Internet scales so well: because HTTP is a stateless protocol. Every HTTP request stands in isolation, so no resources are tied up in maintaining any form of session. It’s the same with transactional components.

This is not to say that you can never maintain state inside your transactional components. You can, but it’s not recommended, and the examples in this appendix don’t illustrate it.
