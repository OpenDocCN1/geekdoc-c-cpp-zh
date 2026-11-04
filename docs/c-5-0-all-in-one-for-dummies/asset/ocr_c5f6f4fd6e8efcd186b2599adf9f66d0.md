# Unit testing

Unit testing is an important piece of software development. There are many great resources on getting started with unit testing and test-driven development, including Kent Beck's classic tome, Test-Driven Development: By Example (Addison-Wesley).

The popular convention for setting up test projects is to create one for each Line of Business project and name the projects <ProjectToTestName>Tests. The project in the sample code for this chapter is named Chapter4Commands; therefore, the Test Project is named Chapter4CommandsTests.

Each test should exercise a distinct Unit of Code (in C#, this translates to a method), have a meaningful name that describes the test scenario, and be composed of three parts:

+   * *Arrange:* Sets up any objects or data required for the test
+   * *Act:* Executes the Unit of Code
+   * *Assert:* Validates the results

The unit tests in this chapter are by no means extensive, but they illustrate the capabilities gained by adhering to the principle of Separation of Concerns.

# First unit test

The first unit test verifies that the Text property of the instantiated command gets populated in the constructor. The complete unit test is shown in Listing 4-10. The Arrange, Act, and Assert comments are not usually included in the unit tests. They are included in Listing 4-10 to demonstrate the structure of a unit test.

To execute the test, run Gallio Icarus — the GUI test runner that ships with Gallio. Click Add Files, navigate to your compiled test project, and then click Start to run the tests.

# Listing 4-10: Unit Testing the Constructor Setting the Text Property

```
[Test]
public void Should_Set_Text_Property_In_The_Constructor()
{
    //Arrange
    CustomSaveCommand command;
    //Act
    string expectedValue = "Save";
    command = new CustomSaveCommand(expectedValue);
    //Assert
    Assert.AreEqual(expectedValue, command.Text);
}
```