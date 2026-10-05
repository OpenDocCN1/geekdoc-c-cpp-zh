# Exercise 10-2 Enhance the Future Value application

This exercise will guide you through the process of adding a combo box and a list box to the Future Value application.

Open the Future Value application and add two controls

+   1. Open the application that's in the C:\C# 2010\Chapter 10\FutureValue directory.
2. Delete the Number of Years text box and replace it with a Number of Years combo box. Then, delete the Future Value text box and replace it with a Future Values list box.

Add the code that works with the controls

+   3. Generate the event handler for the Load event of the form. Then, add code that loads the 1 through 20 in the Number of Years combo box, and add code that selects 3 as the default number of years.
4. Delete the code in the IsValidData method that refers to the Number of Years text box since it isn't needed anymore.
5. Modify the event handler for the Click event of the Calculate button so that it adds the value for each year to the Future Values list box. For example, if you calculate the future value for three years, the Future Value form should return a result like this:

![](bbox=[0.196, 0.526, 0.584, 0.723])

To get this to work correctly, you'll need to use the Clear method of the Items collection for the list box to clear the list each time the Calculate button is clicked. In addition, you can use the modulus operator (%) to add the future value after every twelve months of the calculation. For example:
if (month % 12 == 0) // add the future value to the list box

Test this application to make sure it works correctly.