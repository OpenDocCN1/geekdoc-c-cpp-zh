# How to validate data

Whenever a user enters data, that data usually needs to be checked to make sure that it's valid. This is known as data validation. When an entry is invalid, the application needs to display an error message and give the user another chance to enter valid data. This needs to be repeated until all the entries on the form are valid.

# How to validate a single entry

When a user enters text into a text box, you may want to perform several types of data validation. In particular, it's common to perform the three types of data validation shown in figure 7-8.

First, if the application requires that the user enters a value into a text box, you can check the Text property of the text box to make sure the user entered one or more characters. Second, if the application requires that the user enters a number in the text box, you can use the appropriate Method of the Convert class within a try-catch statement to check that the Text property of the text box can be converted to the appropriate numeric data type. Third, if the application requires that the user enters a number within a specified range, you can use if-else statements to check that the number falls within that range. It is known as range checking.

Although this figure only shows how to check data that the user has entered into a text box, the same principles apply to other types of controls. In control 10, you'll learn more about validating entries made in other types of controls. In addition, although this figure only shows how to check the range of a number, you can also check strings and dates to make sure that they fall within certain ranges. You'll learn more about working with data and strings in chapter 9.

Often, the code that performs the data validation prevents exceptions from being thrown. For example, if the user doesn't enter a value in the Monthly Investment text box, the code in this figure displays a dialog box and moves the focus to the Monthly Investment text box. If you didn't include this code, an exception would occur when the application tried to convert the empty string to a numeric data type.

Since code that validates data without using exception handling runs faster than code that uses exception handling, you should avoid using exception to validate data whenever possible. Of course, this isn't always practical or possible. For example, it's difficult to parse a string to check whether it contains a valid numeric format without using the To method. That's why the second example uses a try-catch statement to check whether converting a string to a decimal throws an exception. In chapter 9, though, you'll learn how to write code that performs the same function without catching an exception.