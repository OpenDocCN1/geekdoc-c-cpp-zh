
When you run your test again it will pass, just as before, as proven by Figure 5-6.

![](img/f852e0a12c174e64d91a8e1a05146eab_192_0.png)

FIGURE 5-6 After being mocked with stubs, the test passes again.

Before you rejoice, you need to acknowledge that you have cheated. You have edited a unit test and not transitioned it from red to green. The test was already successful and, perhaps despite the change, it is still successful. In order to fail this test and then verify that it only passes as a result of a correctly implemented SUT, you should remove the code inside the AddTransactionToAccount method. When you do so, the test will fail, reinstating the code causes the test to succeed. This is an important part of the unit test editing process that avoids false positives—that is, it prevents you from writing a test that succeeds despite not being implemented correctly.

## Testing all control flows

Your first attempt at completing a working AccountService by using a TDD approach has been successful. There are potential problems that will require further tests to ensure that this method is much more robust. So far, you have tested only the Happy Path: the execution path through the code that yields no errors and causes no problems. There are a few gaps that need to be addressed:

- What if the account repository is a null reference?
- What if the repository cannot find the account?
- What if the account method throws an exception?

With each extra test that you write, you either uncover a defect that exists in your implementation (if the test fails) or you add extra confidence that your implementation is robust (if the test succeeds).

Under what circumstances might the account repository be a null reference? This will occur only if the AccountService is constructed with a null passed in as its constructor parameter. Because a valid account repository is a required dependency for the account service, you could say that this is a precondition of the constructor. Thus, we can write the test in Listing 5-18.

This test is slightly different from the previous ones; the assertion is not in the usual place. MSTest requires you to apply the ExpectedExceptionAttribute to the test method with a parameter describing the type of exception that you require.

### LISTING 5-18 No Arrange and no Assert, yet this is a valid test pattern for exceptions.

```
[TestMethod]
[ExpectedException(typeof(ArgumentNullException))]
public void CannotCreateAccountServiceWithNullAccountRepository()
{
    // Arrange

    // Act
    new AccountService(null);

    // Assert
}
```

What this test is specifying is that you expect an ArgumentNullException to be thrown if you construct an AccountService with a null reference for the IAccountRepository instance. This is precisely the precondition that you need, to ensure that in any method of the account service, you always have a valid instance of the repository and do not need to handle the case where it is null. This test fails for the right reasons, as shown here.

Test method ServiceTests.AccountServiceTests.CannotCreateAccountServiceWithNullAccountRepository did not throw an exception. An exception was expected by attribute Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute defined on the test method.

To make this test pass, you need to implement the precondition. The manual approach is shown in Listing 5-19.

### LISTING 5-19 Passing a null account repository into the constructor will cause an exception.

```
public AccountService(IAccountRepository repository)
{
    if (repository == null)
    {
        throw new ArgumentNullException("repository", "A valid account repository must be supplied.");
    }

    this.repository = repository;
}
```

The added lines are in bold. This is an example of failing fast. Without this precondition, an exception would eventually be thrown, but it would be a NullReferenceException and it would occur whenever you first try to access the null repository.

With your constructor test passing, you can move on to the next test case: when the repository cannot find the account. Assume that your repository does not implement the Null Object pattern, which, as described in Chapter 4, "Interfaces and design patterns," would mean that it never returned a null object or threw an exception if the repository could not find the account requested. Instead,

your repository should return a null reference for the account. Listing 5-20 shows the unit test that enforces the expected behavior for this case.

### LISTING 5-20 No expected exception attribute and no assertion!

```
[TestMethod]
public void DoNotThrowWhenAccountIsNotFound()
{
    // Arrange
    var mockRepository = new Mock<IAccountRepository>();
    var sut = new AccountService(mockRepository.Object);

    // Act
    sut.AddTransactionToAccount("Trading Account", 100m);

    // Assert
}
```

The Assert phase of this test is blank, and there is no ExpectedException attribute, either. This is because your expectations are that there should not be an exception thrown during the Act phase of the test. If an exception is thrown at that point, the test fails. If an exception is not thrown—and there are no other assertions that could potentially fail—the test will pass, by default.

In the Arrange phase of the test, you mock the repository and pass it to the SUT (avoiding the precondition by providing a valid instance of the repository) but set up no expectations. This means that the call to IAccountRepository.GetByName() will return null. The next thing that you do with this return value is attempt to call Account.AddTransaction(). Because the instance is null, this causes a NullReferenceException and this test fails. To transition this test to green, you need to prevent this exception from being thrown in your method, as Listing 5-21 shows.

### LISTING 5-21 The if statement protects this method from a NullReferenceException.

```
public void AddTransactionToAccount(string uniqueAccountName, decimal transactionAmount)
{
    var account = repository.GetByName(uniqueAccountName);
    if (account != null)
    {
        account.AddTransaction(transactionAmount);
    }
}
```

By adding a simple if statement that ensures that the account is not null before attempting to use it, you prevent the exception from being thrown, and the test passes.

Now, let's implement the final required test case. This test involves the behavior expected of the account service when the call to the account's AddTransaction method throws an exception. To avoid leaking dependencies between layers, it is good practice to wrap an exception thrown at a lower layer in a new exception for this layer. Figure 5-7 exemplifies this principle.

## 1. 引言

本文档旨在介绍一种基于深度学习的图像识别方法，该方法在多个标准数据集上取得了优异的性能。我们详细阐述了模型的架构设计、训练策略以及实验结果，并对其潜在的应用场景进行了探讨。

## 2. 相关工作

近年来，卷积神经网络（CNN）在计算机视觉领域取得了突破性进展。从早期的 AlexNet 到后来的 VGG、ResNet 等，网络结构不断加深，性能持续提升。此外，注意力机制的引入进一步增强了模型对关键特征的提取能力。

## 3. 方法

我们提出的模型采用了一种新颖的多尺度特征融合策略。具体而言，模型由三个主要模块组成：特征提取骨干网络、多尺度特征融合模块和分类头。

- 特征提取骨干网络：采用 ResNet-50 作为基础架构。
- 多尺度特征融合模块：通过空洞卷积和特征金字塔网络实现。
- 分类头：使用全局平均池化和全连接层。

## 4. 实验

我们在 CIFAR-10 和 ImageNet 数据集上进行了大量实验。下表展示了模型在不同数据集上的准确率对比。

| 数据集 | 准确率 |
|--------|--------|
| CIFAR-10 | 95.2% |
| ImageNet | 78.5% |

## 5. 结论

本文提出了一种有效的图像识别方法，实验结果表明其性能优于现有基线模型。未来工作将探索该方法在更多实际场景中的应用。

The expected exception attribute is used to assert that the SUT throws a ServiceException, whereas the account mock is told to throw a DomainException. Therefore, it is up to the SUT to convert one to the other. The method does not do this, so this test correctly fails, with this message:

Test method ServiceTests.AccountServiceTests.AccountExceptionsAreWrappedInThrowServiceException threw exception Domain.DomainException, but exception Services.ServiceException was expected. Exception message: Domain.DomainException: Exception of type 'Domain.DomainException' was thrown.

The expected exception attribute has determined that the exception thrown is not of the correct type compared to that which was specified. The code in Listing 5-23 shows the changes required to the AddTransactionToAccount method.

### LISTING 5-23 The try/catch block is introduced to map one exception with another.

```
public void AddTransactionToAccount(string uniqueAccountName, decimal transactionAmount)
{
    var account = repository.GetByName(uniqueAccountName);
    if (account != null)
    {
        try
        {
            account.AddTransaction(transactionAmount);
        }
        catch(DomainException)
        {
            throw new ServiceException();
        }
    }
}
```

Although the introduction of the try/catch block transitions your test from red to green, there is an expectation missing, which means that this is still incomplete.

## Writing tests for defect fixes

Imagine that you receive a defect report relating to the current example code. The report states:

> I received a ServiceException when adding a transaction to my account.

You proceed to reproduce the problem and discover the exception that is thrown—this is the proximate cause. But, because the DomainException has been replaced with the ServiceException, it is very difficult to understand the ultimate cause of the error. The original expectation that the new exception should wrap the existing one has not been fulfilled because an assertion is missing from the unit tests.

When a defect arises in this manner, the first thing to do is to write a failing unit test that captures two things: the exact reproduction steps required to force the defect to occur, and the expected behavior that is not currently enforced. Listing 5-24 shows both of these elements in a unit test that fails.
