# FIGURE 7-4

![](bbox=[0.093, 0.088, 0.702, 0.398])

Right-click on the test project. Select Add ▸ New Test. In the Add New Test dialog (see Figure 7-6), select Basic Unit Test and call the new file AverageTests.vb. Click OK to add the new test to your project. The initial code for the unit test provides the core structure needed by all tests:

```
Imports System.Text

<TestClass()> Public Class AverageTests
    <TestMethod()> Public Sub TestMethod1()
    End Sub
End Class
```

As you can see, the test class is simply a normal Visual Basic class, with the addition of a couple of attributes.

The TestClass attribute identifies this class to the testing functionality of Visual Studio; it has no other purpose beyond marking this as a class containing one or more tests.

The TestMethod attribute identifies one of those tests within the class. Like the TestClass attribute, this is primarily a marker attribute. Each of the tests will use this attribute to identify itself. This allows you to have other helper methods within the class that are not tests. Notice also that each of the tests is a Sub, not a Function.

You're ready to begin to create some test methods. As with many other discussions regarding TDD, there are a number of opinions about the scope of each test. Some developers choose to test a number of separate cases within a single method, while others prefer to keep the scope of each test relatively simple. This book falls

# FIGURE 7-5

![](bbox=[0.715, 0.435, 0.88, 0.648])

# FIGURE 7-6

![](bbox=[0.517, 0.682, 0.88, 0.927])