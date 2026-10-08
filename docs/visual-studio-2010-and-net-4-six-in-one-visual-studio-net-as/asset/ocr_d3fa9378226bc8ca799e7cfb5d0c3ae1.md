application with the interface definitions without writing any concrete code. Listing 18-1 shows an example of using an interface in a fictitious banking system.

# LISTING 18-1: Interface Definitions for a Banking System

```
public interface IAccountingService
{
    IAccountDetails GetAccountDetails(ICustomer customer);
    ITransaction TransferMoney(ICustomer sender,
                                 ICustomer receiver,
                                 TransferDetails details);
}

public interface IAccountDetails
{
    // Account detail properties
}

public interface ICustomer
{
    // Customer properties
}

public interface ITransferDetails
{
    // Transfer details
}

public interface ITransaction
{
    // Transaction data
}
```

As you see, with interfaces, you can describe functionality without sticking to the implementation details of concrete classes. Both input arguments and results are handled with interfaces. This design makes it possible to have different IAccountService implementations for different banking systems, but with the same functionality.

# Repository Design Pattern

Most applications have a need to store and retrieve data from some kind of store, which is usually a relational database management system (RDBMS) as SQL Server, Oracle, or DB2.

The Repository Design Pattern acts as a mediator between the relational store and your applications logic. By using well-designed repository classes, it's the developers choose where and how to store the data. Repository Design Pattern adds another level of decoupling to your system by encapsulating the data store-specific implementation details into its own classes.

Listing 18-2 shows a book repository interface with functions defined for finding, retrieving, and storing book data.