constructor calls the properties. This ensures that whatever validation you add to the property also applies to the constructor. For the Salary property, it tests for a negative value passed in. If this happens, then a new exception is thrown.

Add a third test method to the test `PersonTests` class. This test will confirm that the validation added to the `Salary` property does actually throw an exception:

```
```vb
<TestMethod()> Public Sub SalaryCannotBeNegative()
    Try
        Dim emp As New Person.Employee("Foo deBar", -10, DateTime.Today)
        'if we get to this line, there is a problem
        'as the line should have triggered the exception
        Assert.Fail("Employee salary cannot be negative")
    Catch aex As ArgumentOutOfRangeException
        'this is caused by passing in a negative value
        'as it is expected, we'll ignore it
        'which will return a success for the test
    Catch ex As Exception
        'deal with other exceptions here
        Assert.Fail(ex.Message)
    End Try
End Sub
```
```

> *Code snippet from Person*

This test is a little counterintuitive at first. Remember that you are attempting to cause an exception, so it is a little like coding a double negative. The method first attempts to create a new `Employee`, passing in the same `Name` and `hireDate` as before, but now with a negative `Salary`. If the class has been coded correctly, this should throw an `ArgumentOutOfRangeException`. Therefore, if the code doesn’t throw an exception, it will continue on past the constructor, meaning that there is a problem in the code. The code then fails the test. If instead the correct exception was thrown, the code silently ignores it, meaning that the test will pass. This method of constructing a test enables you to ensure that your classes have been defined defensively. You should now be able to run the three tests and see them pass.

Using the Generate from Usage functionality in Visual Studio can be a great time saver when you create your tests, and the classes they test. It enables you to write the tests first, and then be able to execute the tests almost immediately, while giving you the core of the desired class.

# OTHER VISUAL STUDIO EDITIONS

This chapter focuses on the testing functionality included in the Professional Edition of Visual Studio. Table 7-5 describes the Premium and Ultimate Editions, which include a great deal of additional functionality when testing.

**TABLE 7-5:** Functionality of the Premium and Ultimate Editions of Visual Studio

| EDITION | FUNCTIONALITY | DESCRIPTION |
|---|---|---|
| Premium | Code coverage | This feature will analyze your code and tests and allows you to determine how much of the functionality of your classes is actually tested. Ideally, you would like this value to be as high as possible, as it means that you are testing most of the functionality of your application. |
|  | Test impact analysis | This feature analyzes your code and tests and determines which tests are needed after a code change. This can be a great time saver if you have a large number of tests, as it means you will only need to execute a subset of them after updating your code. |