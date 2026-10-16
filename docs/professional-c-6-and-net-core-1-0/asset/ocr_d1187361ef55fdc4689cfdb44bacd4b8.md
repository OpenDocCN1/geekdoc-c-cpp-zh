# LoadStreamLoadOptions.

All these shim members are of a delegate type. This delegate allows specifying a custom method. This custom method is invoked in place of the method call that’s inside the method that is under test. The unit test method TestChampionsByCountry replaces the XElement.Load method with one parameter in the Formula1.ChampionsByCountry method with the call to XElement.Parse, accessing the sample data.

ShimXElement.LoadString specifies the new implementation.

Using shims, it’s necessary to create a context, which you can do using ShimsContext.Create. The context is active until the Dispose method is invoked by the end of the using block (code file UnitTestingSamplesTests/Formula1Tests.cs):

```
[TestMethod]
public void TestChampionsByCountry()
{
    using (ShimsContext.Create())
    {
        ShimXElement.LoadString = s =>
            XElement.Parse(Formula1SampleData());
        Formula1 f1 = new Formula1();
        XElement actual = f1.ChampionsByCountry("Finland");
        Assert.AreEqual(Formula1VerificationData().ToString(),
            actual.ToString());
    }
}
```

Although it is best to have a flexible implementation of the code that should be tested, the Fakes Framework offers a useful way to change an implementation such that it is not dependent on outside resources for testing purposes.

# IntelliTest

A new testing feature available with Visual Studio 2015 Enterprise is IntelliTest, which automatically creates unit tests by making a white-box analysis of the code. IntelliTest analyzes the code to find all iterations by passing as few parameters as possible. When you select a method in the code editor, from the context menu you can select Run IntelliTest to create tests, as shown in Figure 19.6. For the GetStringDemo method, IntelliTest creates 10 test methods that pass different strings for the input parameters. You can check these methods to see whether they fit the purpose, and you can also check for errors if you missed validating input parameters in the method.