
In the Create Unit Tests dialog, select any other additional members you want to test and click OK (see Figure 2-70).

![](img/a977a875c7c627b45d939729705a252e_78_0.png)

Figure 2-70

You are prompted to name the test project. Use the default TestProject1 and click Create. You may also be prompted with the dialog shown in Figure 2-71. Click Yes.

![](img/a977a875c7c627b45d939729705a252e_78_1.png)

Figure 2-71

The TestProject1 is added to Solution Explorer (see Figure 2-72).

![](img/a977a875c7c627b45d939729705a252e_78_2.png)

Figure 2-72

## Part I: C# Fundamentals

The content of the PointTest.cs class is now displayed in Visual Studio 2008. This class contains the various methods that you can use to test the Point class. In particular, note the lengthTest() method:

```csharp
/// <summary>
/// A test for length
/// </summary>
[TestMethod()]
public void lengthTest()
{
    Point target = new Point(); // TODO: Initialize to an appropriate value
    Point pointOne = null; // TODO: Initialize to an appropriate value
    double expected = 0F; // TODO: Initialize to an appropriate value
    double actual;
    actual = target.length(pointOne);
    Assert.AreEqual(expected, actual);
    Assert.Inconclusive("Verify the correctness of this test method.");
}
```

The lengthTest() method has the [TestMethod] attribute prefixing it. Methods with that attribute are known as test methods.

Now modify the implementation of the lengthTest() method to basically create and initialize two Point objects and then call the length() method of the Point class to calculate the distance between the two points:

```csharp
/// <summary>
/// A test for length
/// </summary>
[TestMethod()]
public void lengthTest()
{
    int x = 3;
    int y = 4;
    
    Point target = new Point(x, y);
    Point pointOne = new Point(0,0);
    double expected = 5F;
    double actual;
    actual = target.length(pointOne);
    Assert.AreEqual(expected, actual, "UnitTesting.Point.length did not return the expected value.");
}
```

Once the result is returned from the length() method, you use the AreEqual() method from the Assert class to check the returned value against the expected value. If the expected value does not match the returned result, the error message set in the AreEqual() method is displayed.

### Running the Test

Before you run the unit test, take a look at the Test Tools toolbar (see Figure 2-73) automatically shown in Visual Studio 2008.

![](img/a977a875c7c627b45d939729705a252e_80_0.png)

Figure 2-73

To run the unit test, click the Run All Tests in Solution button in the toolbar. In this case, the lengthTest() method passed the test. The length between two points (3,4) and (0,0) is indeed 5 (see Figure 2-74).

![](img/a977a875c7c627b45d939729705a252e_80_1.png)

Figure 2-74

You can make modifications to the lengthTest() method to test other parameters. In the Test Results window, you have the option to view the previous test results (see Figure 2-75).

![](img/a977a875c7c627b45d939729705a252e_80_2.png)

Figure 2-75

### Testing with Floating Point Numbers

You need to take special note when your test involves comparing floating point numbers. Consider the following example:

```csharp
[TestMethod()]
public void lengthTest()
{
    int x = 4;
    int y = 5;

    Point target = new Point(x, y);
    Point pointOne = new Point(1,2);
    double expected = 4.24264F;
    double actual;
    actual = target.length(pointOne);
    Assert.AreEqual(expected, actual,
        "UnitTesting.Point.length did not return the expected value.");
}
```

When you run the test, the test will fail (see Figure 2-76).

![](img/a977a875c7c627b45d939729705a252e_81_0.png)

Why is this so? The reason is that floating point numbers (such as `Single` and `Double`) are not stored exactly as what they have been assigned. For example, in this case, the value of 4.24264 is stored internally as 4.2426400184631348, and the result returned by the `length()` method is actually 4.2426406871192848. The `AreEqual()` method actually fails if you compare them directly.

To address this issue, the `AreEqual()` method supports a third parameter — `delta` — that specifies the maximum difference allowed for the two numbers that you are comparing. In this case, the difference between the two numbers is 0.00000066865615. And so the following code will pass the test:

```csharp
Assert.AreEqual(expected, actual, 0.00000066865616,
    "UnitTesting.Point.length did not return the expected value.");
```

But this code will fail:

```csharp
Assert.AreEqual(expected, actual, 0.00000066865615,
    "UnitTesting.Point.length did not return the expected value.");

Assert.AreEqual(expected, actual, 0.00000066865614,
    "UnitTesting.Point.length did not return the expected value.");
```

Although the documentation says that the delta specifies the maximum difference allowed for the two numbers, in actual testing the difference should be less than the delta for the Assert.AreEqual() method to pass. This explains why that first statement fails.

### Adding Additional Test Methods

You can insert additional test methods by adding new subroutines to the PointTest.cs file and prefixing them with the [TestMethod] attribute. For example, the following test method uses the AreSame() method of the Assert class to check whether two objects are pointing to the same reference:

```csharp
[TestMethod()]
public void objectTest()
{
    Point point1 = new Point(4, 5);
    Point point2 = new Point() { x = 4, y = 5 };
    Point point3 = point2;

    //---Failed---
    Assert.AreSame(point1, point2, "point1 is not the same as point2");

    //---Passed---
    Assert.AreSame(point2, point3, "point2 is not the same as point3");
}
```

Figure 2-77 shows the test results.

![](img/a977a875c7c627b45d939729705a252e_82_0.png)

Figure 2-77

### Summary

This chapter provided a quick overview of the common features and tools available in Visual Studio 2008. Visual Studio 2008 is highly configurable, so you’ll want to take some time to familiarize yourself with the environment. If you’re totally new to C#, some Visual Studio features like code refactoring and unit testing may not seem all that important to you now, but once you’ve gotten some C# under your belt, you’ll want to take another look at those features.

When you’re ready, the next chapter gets you started in writing code in C#.

## C# Language Foundations

The best way to get started in a new programming language is to create a simple program and then examine the various parts that compose it. With this principle in mind, you’ll create a simple C# program — first using Visual Studio 2008 and then using a plain text editor.

In this chapter you build and run the HelloWorld application, using Visual Studio 2008 as well as using the command line. After that, you tackle the syntax of the C# language and all the important topics, such as:

- C# keywords
- Variables
- Constants
- Comments
- XML documentation
- Data types
- Flow control
- Loops
- Operators
- Preprocessor directives

### Using Visual Studio 2008

The easiest way to create your first C# program is to use Visual Studio 2008.

### Editions of Visual Studio 2008

You can use any of the following editions of Visual Studio 2008 to create a C# program:

- Visual C# 2008 Express Edition
- Visual Studio 2008 Standard Edition
- Visual Studio 2008 Professional Edition
- Visual Studio 2008 Team Suite Edition

All the code samples and screen shots shown in this book were tested using Visual Studio 2008 Professional Edition.

- 1. Launch Visual Studio 2008.
- 2. Create a new Console Application project by selecting File ⇒ New ⇒ Project.
- 3. Expand the Visual C# item on the left of the dialog, and select Windows. Then, select the Console Application template on the right (see Figure 3-1). Name the project HelloWorld.

![](img/a977a875c7c627b45d939729705a252e_85_0.png)

Figure 3-1
