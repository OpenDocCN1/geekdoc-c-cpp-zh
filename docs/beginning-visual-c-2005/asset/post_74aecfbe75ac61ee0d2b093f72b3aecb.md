
## Record Locking

Record locking prevents other users from accessing the locked record while a table row is being updated. The extent to which a record is locked during an update is determined by the locking mode set in the recordset object. There are two locking modes defined in CRecordset, referred to as optimistic mode and pessimistic mode.

| CRecordset::optimistic | In optimistic locking mode, the record is only locked while the Update() member function is executing. This minimizes the time that the record in inaccessible to other users of the database. If an editing operation may take a long time, pessimistic locking is often not a practical solution because other users may need to access the database. The standard solution is to use optimistic locking and to introduce some sort of conflict resolution mechanism. |
| CRecordset::pessimistic | In pessimistic locking mode, the record is locked as soon as you call Edit(), and it remains locked and therefore inaccessible to other users until the completion of the call to Update() or until the update operation is aborted. This can obviously severely affect performance when updates are being prepared interactively; however, this mode is essential in many instances to ensure the integrity of the data is maintained. |

The default mode for a recordset object is optimistic, so you have to set it only if you want pessimistic mode. To set this mode, you call the SetLockingMode() member of the recordset object with CRecordset::pessimistic as the argument. Of course, you can also reset it by calling the function with CRecordset::optimistic as the argument.

## Transactions

The idea of a transaction in the database context is to enable operations to be safely undone when necessary. A transaction packages a well-defined series of one or more modifications to a database in to a single operation so that at any point prior to the completion of the transaction everything can be reversed (or rolled back) if an error occurs. Clearly, if an update were to fail when it was partially completed, due to a hardware problem, for instance, it could have a disastrous effect on the integrity of the database. A transaction is not just an update to a single table. It can involve very complex operations on a database involving a series of modifications to multiple tables and may take an appreciable time to complete. In these situations, support for transactions is virtually a necessity if the integrity of the database is to be assured.

With transaction based operations, the database system manages the processing of the transaction and records recovery information so that anything that the transaction does to the data can be undone in the event of a problem part way through. By making your database operations based on transactions, you can protect the database against errors that might occur during processing. Typically, transaction processing locks records as necessary along the way and also ensures that any other database users accessing data that has been modified by the transaction will see the changes immediately.

Transactions are supported by most large commercial database systems on mainframe computers, but this is not always the case with database systems that run on a PC. In spite of this, the CDatabase class in MFC does support transactions, and as it happens, so does the Microsoft ODBC support for Access databases, so you can try out transaction processing with the Sample Data database if you want.

## CDatabase Transaction Operations

Transactions are managed through members of your CDatabase class object that provides the connection to the database. To determine whether transactions are supported for any given connection, you call the CanTransact() member of the CDatabase object. This returns TRUE if transactions are supported. Incidentally, there is also a CanUpdate() member of CDatabase that returns FALSE if the data source is read-only.

There are three member functions of CDatabase involved in transaction processing:

| BeginTrans() | Starts a transaction on the database. All subsequent recordset operations are part of the transaction, until either CommitTrans() or Rollback() is called. The function returns TRUE if the transaction start was successful. |
| CommitTrans() | Commits the transaction so all recordset operations that are part of the transaction are expedited. The function returns FALSE if an error occurs, in which case the state of the data source is undefined. |
| Rollback() | Rolls back all the recordset operations executed since BeginTrans() was called, and restores the data source to the condition at the time when BeginTrans() was called. |

The sequence of events in a transaction is very simple:

- Call BeginTrans() to start the transaction.
- Call Edit(), Update(), AddNew(), for your recordset as necessary.
- Call CommitTrans() to complete the transaction.

Outside of a transaction, Edit() or AddNew() operations on a recordset are executed when you call Update(). Within a transaction they are not executed until you call CommitTrans() for the CDatabase object. If you need to abort the transaction at any time after calling BeginTrans(), just call Rollback().

Complications can arise with the effect of CommitTrans() and Rollback() (the position in the recordset you are operating on can be lost for instance, so you may need to take some action in your program to recover the record pointer after completing or aborting a transaction. There are two members of CDatabase to help with this. After a CommitTrans() call you need to call the GetCursorCommitBehavior() member of CDatabase, and after calling Rollback() you need to call GetCursorRollbackBehavior(). Both of these functions return one of three values of type int that indicate what you should do:

![](img/2359b0c604600c58fba3539c738a356e_1026_0.png)

Figure 20-2

![](img/2359b0c604600c58fba3539c738a356e_1026_1.png)

Figure 20-3

## Customizing the Application

The Order Details table contains five columns — Order ID, Product ID, Unit Price, Quantity, and Discount. If you display Class View and look at the members of COrderDetailsSet, you will see the data members corresponding to these. You need a static text control and an edit control for each of these on the dialog corresponding to the recordset. I arranged them as shown in Figure 20-4, but you can arrange them how you like.

![](img/2359b0c604600c58fba3539c738a356e_1027_0.png)

Assign IDs to the edit controls to match the field name as you did in the previous chapter — the last one is IDC_DISCOUNT, for example. The default style set for an edit control allows keyboard input, but on the assumption you want to limit which recordset fields can be altered, you should set the first three edit controls as read-only, using the styles tab in the Properties window. The value displayed in a read-only control can be set in the program, but a value cannot be entered in the control from the keyboard. You can set all these to read-only in a single step by selecting each of the three controls with the Ctrl key held down and then right-clicking to display the popup menu and selecting Properties. Whatever you then set in the Properties window is applied to all three. With the dialog arrangement shown, you will only be able to enter data for Quantity and Discount.

The only other thing you need to do is to associate the edit controls with a corresponding data member of the recordset, and as you saw in the previous chapter, you just add a DDX_ function call to the DoDataExchange() function in the recordset view class, COrderDetailsView, for each data field in the recordset. Here's how that code looks:

```
```cpp
void COrderDetailsView::DoDataExchange(CDataExchange* PDX)
{
	CRecordView::DoDataExchange(pDX);
	DDX_FieldText(pDX, IDC_ORDERID, m_pSet->m_OrderID, m_pSet);
	DDX_FieldText(pDX, IDC_PRODUCTID, m_pSet->m_ProductID, m_pSet);
	DDX_FieldText(pDX, IDC_UNITPRICE, m_pSet->m_UnitPrice, m_pSet);
	DDX_FieldText(pDX, IDC_QUANTITY, m_pSet->m_Quantity, m_pSet);
	DDX_FieldText(pDX, IDC_DISCOUNT, m_pSet->m_Discount, m_pSet);
}
```
```
