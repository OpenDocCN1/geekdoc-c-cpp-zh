# ## Exercise 16-2 Create and use a class library

In this exercise, you’ll create a class library that contains the Validator class. Then, you’ll use that class library with the CustomerMaintenance application.

+   1. Create a new Class Library project named ValidationLib. Then, delete the empty Class1.cs file, and add the Validator.cs file from the CustomerMaintenance project that you worked on in the previous exercise.
+   
+   2. Change the namespace in the Validator class to Murach.Validation. Then, use the Build→Build Solution command to build the class library, and close the solution.
+   
+   3. Open the application that you used in the previous exercise, delete the Validator.cs file, and add a reference to the ValidationLib assembly you created in step 2. Then, open the Add Customer form and add a using directive for the Murach.Validation namespace.
+   
+   4. Run the project and test it to make sure the validation works correctly.

# ## Exercise 16-3 Create and run unit tests

In this exercise, you’ll create a unit test project that tests one of the methods of the Validator class in the class library you worked on in exercise 16-2.

+   1. Open the application in the C:\Chapter 16\ValidationLib directory.
+   
+   2. Create a new MSTest Test Project called ValidationLibTest. Add a reference to the test project to the ValidationLib project so you can test the methods in that project.
+   
+   3. Rename the default class file in the MSTest project to ValidatorTest.
+   
+   4. Rename the default test method to IsWithinRange_Valid(). Then, add code to this method that uses the AreEqual() method of the Assert class to test that the IsWithinRange() method works properly when a valid value is passed to it. As you do that, be sure to use the AAA pattern as described in figure 16-11.
+   
+   5. Add a test method to the ValidatorTest class to test what happens if the value that’s passed to the IsWithinRange() method is smaller than the minimum value. Do that, use the IsTrue() method of the Assert class to test that the method returns the expected error message.
+   
+   6. Add another test method to test what happens if the value that’s passed to the IsWithinRange() method is larger than the maximum value. The easiest way to do that is to copy the method you added in step 5, and then change the method name and the value that’s passed to the IsWithinRange() method.
+   
+   7. Compile the project and correct any errors that are detected.
+   
+   8. Display the Test Explorer window. Then, point to the first four buttons in the toolbar to see what they do, and display the menu for the second button to see what it includes. In addition, point to the next four buttons to see what information they display.