to each test. You can also do the same with the SUT, because that only requires the mock repository as a constructor parameter and its construction doesn’t depend on anything specific to each unit test. [Listing 4-26](#) shows the changes required to the test class to support the setup method.

# **LISTING 4-26** The mock objects and the SUT can be constructed in a setup method.

[Click here to view code image](#)

```
```csharp
[TestClass]
public class AccountServiceTests
{

    [TestInitialize]
    public void Setup()
    {
        mockAccount = new Mock<Account>();
        mockRepository = new Mock<IAccountRepository>();
        sut = new AccountService(mockRepository.Object);
    }

    private Mock<Account> mockAccount;
    private Mock<IAccountRepository> mockRepository;
    private AccountService sut;
}
```
```

With these objects constructed as part of a test initialization method, which is called individually for each test method, you can simplify some of the unit test code by removing this object construction. [Listing 4-27](#) shows the changes made to the most recent unit test, AccountExceptionsAreWrappedInThrowServiceException.

# **LISTING 4-27** This test is a little shorter and a little easier to read.

[Click here to view code image](#)

```
```csharp
[TestMethod]
public void AccountExceptionsAreWrappedInThrowServiceException()
{
    // Arrange
    mockAccount.Setup(a => a.AddTransaction(100m)).Throws<DomainException>();
    mockRepository.Setup(r => r.GetByName("Trading
Account")).Returns(mockAccount.Object);

    // Act
    try
    {
```
```