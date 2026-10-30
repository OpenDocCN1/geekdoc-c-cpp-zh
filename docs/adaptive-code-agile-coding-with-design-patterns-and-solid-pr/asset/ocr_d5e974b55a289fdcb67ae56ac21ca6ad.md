# LISTING 5-27 This test is a little shorter and a little easier to read.

```
[TestMethod]
public void AccountExceptionsAreWrappedInThrowServiceException()
{
    // Arrange
    mockAccount.Setup(a => a.AddTransaction(100m)).Throws<DomainException>();
    mockRepository.Setup(r => r.GetByName("Trading Account")).Returns(mockAccount.Object);

    // Act
    try
    {
        sut.AddTransactionToAccount("Trading Account", 100m);
    }
    catch(ServiceException serviceException)
    {
        // Assert
        Assert.IsInstanceOfType(serviceException.InnerException, typeof(DomainException));
    }
}
```

Three lines might not be a huge amount of code to remove, but the cumulative effect on all of the unit tests is more readable code. You know that, by convention, any variable with the prefix mock will be a mocked object, whereas the variable sut is your system under test.

# Unit-testing patterns

Tests, just like production code, can become unwieldy and unreadable. And, just like production code, tests are read many more times than they are written—by all sorts of people. Someone once said that you should write code as if the next person to read it is a psychopath who knows where you live. Of course, this is hyperbolic and pithy, but there is a nugget of truth in there. Be considerate of the poor souls who must read your code in the future: help them to do their job, do not hinder them.

# Writing maintainable tests

Given that test readability is at least as important as production code readability, how do you diagnose readability problems with existing tests, and what options are available to you for improving the readability of tests?

First, there are tactical changes that can be made to tests that improve the line-by-line readability of the tests. Second, there are strategic—or structural—changes that can influence the readability in a larger way.