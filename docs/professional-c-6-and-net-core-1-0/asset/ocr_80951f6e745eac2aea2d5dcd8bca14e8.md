method names. By default, Tests or Test is added as postfix, but you can decide to change this. From this dialog, you can also install additional test frameworks.

![](bbox=[0.105, 0.125, 0.895, 0.435])

# Figure 19.1

A unit test class is marked with the TestClass attribute, and a test method is marked with the TestMethod attribute. The implementation creates an instance of DeepThought and invokes the method that is to be tested:
TheAnswerToTheUltimateQuestionOfLifeTheUniverseAndEverything.
The return value is compared with the value 42 using Assert.AreEqual. In case Assert.AreEqual fails, the test fails (code file UnitTestingSamplesTest/DeepThoughtTests.cs):

```
[TestClass]
public class TestProgram
{
    [TestMethod]
    public void
TestTheAnswerToTheUltimateQuestionOfLifeTheUniverseAndEverything
    {
        // arrange
        int expected = 42;
        var dt = new DeepThought();

        // act
        int actual =
 dt.TheAnswerToTheUltimateQuestionOfLifeTheUniverseAndEverything(

        // assert
        Assert.AreEqual(expected, actual);
    }
}
```