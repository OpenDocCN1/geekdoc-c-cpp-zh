```
"BankOfMe", "Me")
MessageBox.Show(String.Format("(0:C) transfered from {1} to {2}",
CDec(Me.TransferField.Text), "BankOfWrox", "BankOfMe"),
"Transfer Succeeded",
MessageBoxButtons.OK,
MessageBoxIcon.Information)
Catch ex As Exception
MessageBox.Show(ex.Message, "Transfer failed",
MessageBoxButtons.OK,
MessageBoxIcon.Error)
End Try
End Sub
```

Code snippet from TestTransactions

# The Transaction Attribute

Now it’s time to tell Component Services how the component should enter a transaction. There are two ways of doing this: via the Component Services Console or via an attribute in code. To do it via the Component Services Console, open the Explorer tree to locate the Transactions component (as shown in Figure D-14).

Right-click on the Transactions.DLL and select Properties. You can view the available options for the transactions for this class by going to the Transactions tab. Select one of the available options; you’ll learn what these all mean in a moment. It’s a little tiresome to require the system manager to do this every time, especially if you already know that your component is always going to have the same transaction characteristics. An alternative mechanism is available: You can explicitly set up an attribute in the code for your component.

Attributes are items of declarative information that can be attached to the elements of code, such as classes, methods, data members, and properties. Any code that accesses classes that include attributes can query the values assigned at runtime. One such attribute is called TransactionAttribute, which, unsurprisingly, is used for specifying the transaction characteristics of a component class. The value of this attribute is taken from an enumeration called TransactionOption. Both TransactionAttribute and TransactionOption are found within the System.EnterpriseServices namespace. The enumeration can take the following values:

![](bbox=[0.59, 0.27, 0.88, 0.51])

FIGURE D-14

| VALUE | DESCRIPTION |
| Disabled | Ignores any transaction in the current context. This is the default. |
| NotSupported | Creates the component in a context with no governing transaction. |
| Required | Shares a transaction if one exists. Creates a new transaction if necessary. |
| RequiresNew | Creates the component with a new transaction, regardless of the state of the current context. |
| Supported | Shares a transaction if one exists. If it doesn’t, then it creates the component. |

The available values are exactly the same as the ones shown in the Transaction tab. This case is a standalone transaction, so either RequiresNew or Required are equally valid. However, you would most commonly select RequiresNew to create a component that will participate in an existing transaction or create a new transaction if needed.