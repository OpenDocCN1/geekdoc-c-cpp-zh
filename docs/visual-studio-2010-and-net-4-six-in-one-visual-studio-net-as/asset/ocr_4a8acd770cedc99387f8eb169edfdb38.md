```
{
    public string CustomerName { get; set; }
    public int ProductId { get; set; }
    public int Quantity { get; set; }
}
```

Unfortunately, these two classes have issues. When you see their definitions and want to use them, you must ask the architect (or even the developer) some questions about these classes to use them successfully. Here are a few questions you may ask:

+   - What happens if a null is passed to the QueueOrder method? You may assume, it raises an ArgumentNullException, but you cannot be sure.
- What if the ColumnName property of Order is null, or an empty string? Is the order valid in this case?
- What if the Quantity property of Order is negative? Does it mean that actually a product is returned to the warehouse? Can this be zero?

These questions would not be necessary if there were a way to describe the behavior of the QueueOrder method in any unambiguous way as the signature of the contract. Actually, the answers to these questions would be part of the contract defining the WarehouseService behavior.

This is a new-er .NET Framework approach, programming with code contracts, comes into the picture. The idea behind code contracts is that classes and methods should explicitly state what they require, what they guarantee and what happen if those requirements are met. This practice was first introduced by Bertrand Meyer with the Eiffel programming language, and Microsoft Research also has a project called Spec#, which carries a formal language for API contracts (influenced by Eiffel, JML, and Asml languages). These contracts are not only human-readable but can also be picked up by tooling that can perform run-time checking or verification, or perhaps include them in generated documentation.

# Understanding the Code Contracts System

There are two parts to involved in using code contracts in the .NET Framework 4.0. The first part is the code contract library. Contracts are encoded using static method calls defined in the Contract class of the System.Diagnostics.Contracts namespace. Contracts are declarative, and these static calls in your methods can be thought of as part of the method signature. For example, the QueueOrder method treated earlier could be extended with a few declarative contracts:

```
public void QueueOrder(Order order)
{
    Contract.Requires(order != null);
    Contract.Requires(order.Quantity > 0);
    // ...
}
```