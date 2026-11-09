some resource manager dissents, it aborts. What if I want to abort the transaction myself because of a problem my code discovers? Well, I’m glad you asked. (It’s lonely sitting in a dark room, typing all day. You start talking to yourself.) Every COM+ call carries with it some basic information or context. This might be information such as who called you plus all the security stuff discussed in Chapter 18, “COM+ Security.” MTS ups the ante with even more context, including things such as transaction information. In fact, the MTS context supplies support for just about everything that a sane developer could need within a component method call. Using the MTS context interface, we can vote to commit or abort the current transaction.

This is not the MTS section of the book, so I’ll limit the discussion here to the things you would need to simply queue messages in an MTS transaction. The first things you need are declarations for the various MTS interfaces and structures of interest. These are available through mtx.h. Next, you need a way to get the context information for the call. MTS maintains a Context object describing the specifics for each outstanding MTS call. The Context object supports the IObjectContext interface and can be retrieved through the MTS GetObjectContext() call. Because MTS tries to simplify the COM model for COM+ objects, the protocol for ending a transaction is a little different from what you’ve seen before. Objects have access to five routines relating to the state of their transaction, as shown in Table 25.5.

**Table 25.5 — Transaction State Access Routines**

| Routine | Description |
|---|---|
| `IsInTransaction()` | Identifies the existence of a transaction in the current context. |
| `DisableCommit()` | Causes subsequent attempts to commit to abort. |
| `EnableCommit()` | Re-enables a transaction after a call to `DisableCommit()`. |
| `SetAbort()` | Aborts the transaction. |
| `SetComplete()` | Attempts to commit the transaction (implicitly enables commitment). |

Listing 25.10 shows the complete code for the PlaceOrder() method of the MTS OrderEntry component. You’ll note that we don’t begin the transaction within the code; instead, we rely on an implicit transaction. Such transactions can be configured by the MTS administrator, or (as you’ll see in the MTS section) configured through attributes in the components type library. In cases in which you find yourself executing with MTS without a transaction (sacrilege!), you can always roll your own with the ITransactionContextEx::CreateInstance() method call. You can create a ITransactionContextEx object with CreateInstance(), and because it requires a