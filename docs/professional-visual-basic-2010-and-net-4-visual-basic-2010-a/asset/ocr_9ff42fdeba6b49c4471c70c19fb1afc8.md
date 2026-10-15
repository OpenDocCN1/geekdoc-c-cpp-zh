You should now be able to run all the tests in both the RepositoryTests and TestDbTests to see that both of your implementations work and all tests pass.

As you can see, using the test implementation requires far less setup and code to implement than a test database. This means that it is easier to perform if you are simply experimenting with the functionality you might need to access your database. There is a slight chance that the behavior of the internal list may differ from the actual data access, but this can be controlled when defining the data types you return.

# Using the Generate from Usage Feature

Visual Studio 2010 adds a very exciting testing feature: the capability to create your classes from the tests. This enables you to do “pure” test-first development, without the actual effort of creating the structure of your classes after you have tested them.

Using this method, you leverage IntelliSense to create the basic structure of the tested code while writing your tests. Initially, these tests will fail, as the tested class does not have any functionality. You then edit your class to add the needed functionality, and watch as your tests go from red to green.

Create a new Class Library project called Person. You can delete the initially created Class1 from the project. Add a Test Project to the solution named Person.Tests. Rename the initially created class from UnitTest1 to EmployeeTests, and the initial test from TestMethod1 to DefaultEmployeeInitializes. This test will confirm that when you use the default constructor, the properties of the new object are set to default values. Of course, you haven’t created this new class, or the properties, yet.

![](bbox=[0.49, 0.35, 0.88, 0.44])

FIGURE 7-9

Add the line Dim emp As New Person.Employee to the method. You’ll notice that the class name gets a blue, wavy line under it to mark it as unknown to IntelliSense. Open the smart tag menu for the item. Don’t select the option to generate this type, as it will create the type within the Person.Tests project, rather than the Person project. Instead, select the “Generate new type” option (see Figure 7-9) to bring up the Generate New Type dialog.

![](bbox=[0.54, 0.47, 0.88, 0.67])

FIGURE 7-10

In the Generate New Type dialog (see Figure 7-10) select to add the new type to the Person project, and change the Access to Public. When you click OK, the Class Library should contain a new file named Employee.vb.

Continue editing the test to add a few assertions about properties of the Employee object. For example, if the object has been created with the default constructor, then the properties should have a value appropriate for each type:

```
<TestMethod()> Public Sub DefaultEmployeeInitializes()
    Dim emp As New Person.Employee
    'ensure default property values
    Assert.AreEqual(emp.Name, String.Empty)
    Assert.AreEqual(emp.Salary, Decimal.Zero)
    Assert.AreEqual(emp.HireDate, DateTime.MinValue)
End Sub
```

Blue, wavy lines should again appear under the three properties. You can open the smart tag menu and select to “Generate the property stub for ‘Name’ in Person.Employee.” This will add the method to the