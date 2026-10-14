```
"Package weight must be positive and non-zero");
    Contract.Requires<ArgumentOutOfRangeException>(packageDimensionsInInches.X > 0f &&
    packageDimensionsInInches.Y > 0f, "Package dimensions must be positive and non-zero");

    Contract.Ensures(Contract.Result<decimal>() > 0m);

    return decimal.One;
}

[ContractInvariantMethod]
private void ClassInvariant()
{
    Contract.Invariant(flatRate > 0m, "Flat rate must be positive and non-zero");
}
}
```

For interface contracts, you of course need an interface to work with. In this example, the CalculateShippingCost method has been extracted into its own IShippingStrategy interface. It is this interface, rather than a single implementation, that is going to have the contracts applied. This is an important departure from the previous examples because it means that all implementations of this interface will acquire the applied contracts. This is how you can enhance a simple interface that provides few instructions for implementation and use, to give it more powerful requirements and assurances.

When writing an interface contract, you also need a class that is going to implement the methods of the interface but only fill them with uses of the Contract.Requires and Contract.Ensures methods. The abstract ShippingStrategyContract provides this functionality and looks like the prior examples, but what the prior examples lacked was the real functionality of the method. Even in production code, this is the limit of the code contained in a contract class. There is also a ContractInvariantMethod to house any calls to Contract.Invariant, just as if this class were the real implementation.

To link the interface to the contract class implementation, you unfortunately need a two-way reference via an attribute. This is somewhat unfortunate because it adds noise to the interface, which it would be nice to avoid. Nevertheless, by marking the interface with the ContractClass attribute and the contract class with the ContractClassFor attribute, you can write your preconditions, postconditions, and data invariant protection code once and have it apply to all subsequent implementations of the interface. Both the ContractClass and ContractClassFor attributes accept a Type argument. The ContractClass is applied to the interface and has the contract class type passed in, whereas the ContractClassFor is applied to the contract class and has the interface type passed in.

This concludes the introduction to code contracts and the foray into the Liskov substitution principle’s rules relating to contracts. One final important point needs to be emphasized. Whether they are implemented manually or by using code contracts, if a precondition, postcondition, or invariant fails, clients should not catch the exception. Catching an exception is an action that indicates that the client can recover from this situation, which is seldom likely or perhaps even possible when a contract is broken. The ideal is that all contract violations will happen during functional testing and