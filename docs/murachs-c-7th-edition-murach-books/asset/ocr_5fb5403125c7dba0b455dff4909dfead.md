# Commonly used static methods of the Assert class

| Method | Description |
|---|---|
| `AreEqual(expected, actual)` | Tests whether the actual object is equal to the expected object and throws an exception if the two objects are not equal. |
| `AreNotEqual(expected, actual)` | Tests whether the actual object is equal to the expected object and throws an exception if the two objects are not equal. |
| `IsFalse(booleanExpression)` | Tests whether the Boolean expression is false and throws an exception if it is true. |
| `IsTrue(booleanExpression)` | Tests whether the Boolean expression is true and throws an exception if it is false. |

# A using directive that simplifies access to the class being tested

```
using Murach.Validation;
```

# Unit tests for the Validator class

```
[TestClass]
public class ValidatorTest
{
    [TestMethod]
    public void IsDecimal_ValidValue()
    {
        string expected = "";                 // arrange
        var result = Validator.IsDecimal("3.14", "Name"); // act
        Assert.AreEqual(expected, result);     // assert
    }

    [TestMethod]
    public void IsDecimal_InvalidValue()
    {
        string name = "Test field";            // arrange
        var result = Validator.IsDecimal("three", name); // act
        Assert.IsTrue(result.Contains(name));  // assert
    }
    .
    .
}
```

# Description

+   - To simplify access to the project you’re testing, you can include a using directive for that project as shown above.
+   - You must include a TestClass attribute before each test class declaration to indicate that the class contains unit tests. You must also include the TestMethod attribute before each method in a test class to indicate that it’s a test method.
+   - Each unit test class should include as many methods as necessary to test all possible aspects of the methods in the class being tested.
+   - A common way to code a test method is to use the Arrange, Act, Assert (AAA) pattern. First, you create the objects and initialize the variables to be passed to the method being tested (Arrange). Then, you call the method with the arranged arguments (Act). Finally, you use methods of the Assert class to test that the result is as expected (Assert).

Figure 16-11    How to code unit tests