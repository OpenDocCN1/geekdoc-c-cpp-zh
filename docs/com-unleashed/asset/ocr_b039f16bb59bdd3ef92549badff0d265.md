# LISTING 17.2 The Visual Basic Client Application That Uses the Simple Transaction Component

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

17 COM+ AS A TRANSACTION COORDINATOR

The component has a class named CFirst with a method named DoIt() that does the work. The first thing that happens in the DoIt() method is GetObjectContext() is called. The object context must be obtained in order to either commit (with SetComplete()) or abort (with SetAbort()) the transaction.

Some error checking comes next to make sure the IObjectContext pointer was retrieved without an error. We wouldn't want to perform operations on a NULL or invalid IObjectContext pointer.

For this example, the decision to commit or abort is based on the system time. If the system time returns a minute that's an even number, the transaction succeeds. If the minute is an odd number, the transaction aborts.

In order to commit the transaction, a simple call to SetComplete() is made. To abort, a call to SetAbort() is made. The IObjectContext is freed with a call to Release(), and the method then returns to the caller.

Notice that a CString class member named m_strTransactionResult is set during the method so that the calling program can easily get a text string describing the outcome of the method call.

The Visual Basic program (Listing 17.2) is easy to understand. It simple instantiates the component, calls the DoIt() method, and then sets a label in the form with the result string.

It's very important to note here that in order for this to work, the component must be in the COM+ catalog as part of an application. Its attributes must also be set correctly. I talk about setting COM+ component attributes later in the chapter.