This chapter will continue to build on this example for the Act and Assert parts of the test, too. The test method’s name, `AddingTransactionChangesBalance()`, succinctly describes the intent of the test—to ensure that whenever a transaction is added to the account, the balance of the account is changed to include this new transaction.

```
```csharp
[TestClass]
public class AccountTest
{
    [TestMethod]
    public void AddingTransactionChangesBalance()
    {
        // Arrange
        var account = new Account();
    }
}
```
```

The Arrange step taken here is simple enough. The only precondition to this test is a new instance of the Account class. You create this directly in your test by calling the new operator. From here, you can move on to the next step in the AAA pattern.

# Performing the testable act

Now that you have the system under test ready to be acted on, you can execute the method that you are testing. Each test’s Act phase should consist of just one interaction with the system under test—one method call or property getter or setter, for instance. This ensures that the tests are simple to both read and write and have clearly delineated execution paths.

Listing 5-2 shows the addition of the Act part of the test. In keeping with the test method’s name, the test calls the `account.AddTransaction()` method.

```
```csharp
[TestClass]
public class AccountTest
{
    [TestMethod]
    public void AddingTransactionChangesBalance()
    {
        // Arrange
        var account = new Account();

        // Act
        account.AddTransaction(200m);
    }
}
```
```