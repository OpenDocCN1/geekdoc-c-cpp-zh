the IMSMQTransactionDispenser interfaces. Transactions are ended by calling the `commit()` or `abort()` methods of the `ITransaction` interface.

# ## Transaction

The `ITransaction` COM+ interface is used to end transactions and to retrieve transaction information regarding a given transaction. From the MSMQ API perspective, the `ITransaction` interface supports three methods:

+   - `Commit()`
+   - `Abort()`
+   - `GetTransactionInfo()`

MSMQ ActiveX components represent this interface through the MSMQTransaction class, which treats the last method as a property. Note that ITransaction is a COM+ interface and, therefore, inherits IUnknown and must be released when no longer needed. Be careful with Smart Pointers because they will take care of this for you.

The `commit()` method ends the transaction requesting that all queues make permanent and apply any changes taking place in the transaction. The commit can fail, however. It is very important to examine the HRESULT returned by the commit operation. A failed commit is equivalent to an abort, and all queue operations in the transaction will be rolled back. The `abort()` method performs a transaction abort outright, rolling back all changes. Both commit and abort methods have three parameters, which can be used to configure advanced features such as asynchronous completion. These parameters are set to 0 to provide default behavior in most cases.

# ## Creating Transactional Queues

Transaction messages can only be sent to transaction queues. By the same token, non-transaction messages can only be sent to nontransaction queues. Transaction queues are created just like normal queues with the addition of a true value in the transaction flag field. A queue’s transactional attribute cannot be modified, so it must be set correctly at the time the queue is created. The sample Create routine for a transactional queue, shown in Listing 25.6, comes from our EnterOrder component.

# **LISTING 25.6**  Creating a Transactional Queue

```
STDMETHODIMP COrder::CreateShippingQueue()
{
    try
    {
        //Set up queue information using a smart pointer
```