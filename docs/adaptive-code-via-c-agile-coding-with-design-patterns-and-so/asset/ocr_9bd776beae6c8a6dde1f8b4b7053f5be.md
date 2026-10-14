Moq defines *loose* mocks, which means that all of their return values are default. The default for any reference type is null and this applies to the Account class. The alternative to the loose mock is the *strict* mock, which will throw an exception whenever it is faced with a method call or property access that you have not already specified. Neither of these options is what you need, so you have to set up some expected behavior manually.

The Setup method of a Mock instance is very clever. It accepts a lambda expression that provides an instance of the underlying mocked type as a context parameter. By calling a method on the type, you are effectively specifying that you want something to happen when the method is called, with the exact arguments provided. What you choose to specify depends on your test situation. Moq lets you set the following expectations on a method call:

+   - Call some other lambda expression.
+   - Return a specific value.
+   - Throw a specified type of exception.
+   - Verify that this method was called.

For this test, you want the second option: return a specified value. The fluent interface of the Mock.Setup method call allows you to chain the call to the Returns method. This improves readability and reduces what is already becoming a rather large Arrange phase of the test. The Returns method is given the Account instance that you have already created, and with this you have completed setting your expectations of this mock. In brief, you have given the mock the following instruction:

> When the GetByName method is called for this IAccountRepository instance, and the account name provided is “Trading Account”, return this instance of the Account class.

When you run your test again it will pass, just as before, as proven by Figure 4-6.

![](bbox=[0.01, 0.54, 0.985, 0.77])

# FIGURE 4-6 After being mocked with stubs, the test passes again.

Before you rejoice, you need to acknowledge that you have cheated. You have edited a unit test and not transitioned it from red to green. The test was already successful and, perhaps despite the change, it is still successful. In order to fail this test and then verify that it only passes as a result of a correctly implemented SUT, you should remove the code inside the AddTransactionToAccount method. When you do so, the test will pass, and reinstating the code causes the test to succeed. This is an important part of the unit test editing process that avoids false positives—that is, it prevents you from writing a test that succeeds despite not being implemented correctly.