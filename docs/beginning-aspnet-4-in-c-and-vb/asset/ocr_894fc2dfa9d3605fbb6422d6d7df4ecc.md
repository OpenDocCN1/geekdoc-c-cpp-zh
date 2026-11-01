# Nested Scopes with Ambient Transactions

With the `TransactionScope` class you can also nest scopes. The nested scope can be directly inside the scope or within a method that is invoked from a scope. A nested scope can use the same transaction as the outer scope, suppress the transaction, or create a new transaction that is independent from the outer scope. The requirement for the scope is defined with a `TransactionScopeOption` enumeration that is passed to the constructor of the `TransactionScope` class.

The values available with the `TransactionScopeOption` enumeration and their functionality are described in the following table:

| TRANSACTION SCOPE OPTION MEMBER | DESCRIPTION |
|---|---|
| `Required` | Required defines that the scope requires a transaction. If the outer scope already contains an ambient transaction, the inner scope uses the existing transaction. If an ambient transaction does not exist, a new transaction is created.

If both scopes share the same transaction, every scope influences the outcome of the transaction. Only if all scopes set the success bit can the transaction commit. If one scope does not invoke the `Complete()` method before the root scope is disposed of, the transaction is aborted. |
| `RequiresNew` | RequiresNew always creates a new transaction. If the outer scope already defines a transaction, the transaction from the inner scope is completely independent. Both transactions can commit or abort independently. |
| `Suppress` | With Suppress, the scope does not contain an ambient transaction, whether or not the outer scope contains a transaction. |

The next sample defines two scopes, in which the inner scope is configured to require a new transaction with the option `TransactionScopeOption.RequiresNew`:

```
```csharp
using (var scope = new TransactionScope())
{
    Transaction.Current.TransactionCompleted +=
        OnTransactionCompleted;

    Utilities.DisplayTransactionInformation("Ambient TX created",
        Transaction.Current.TransactionInformation);

    using (var scope2 =
        new TransactionScope(TransactionScopeOption.RequiresNew))
    {
        Transaction.Current.TransactionCompleted +=
            OnTransactionCompleted;

        Utilities.DisplayTransactionInformation(
            "Inner Transaction Scope",
            Transaction.Current.TransactionInformation);

        scope2.Complete();
    }
    scope.Complete();
}
```
```

code snippet TransactionSamples/Program.cs

Running the application, you can see that both scopes have different transaction identifiers, although the same thread is used. Having one thread with different ambient transactions because of different scopes, the transaction identifier differs in the last number following the GUID.