19. When you design your own classes that might cause exceptions, and other classes will use your classes as clients, you should usually create your methods to

+   a. neither throw nor handle exceptions
b. throw exceptions but not handle them
c. handle exceptions but not throw them
d. both throw and handle exceptions

20. When you create an Exception subclass of your own, you should extend the class.

+   a. SystemException
b. PersonalException
c. OverloadedException
d. Exception

# Exercises

# Programming Exercises

+   1. Write a program named SubscriptExceptionTest in which you declare an array of 10 doubles and store values in the array. Write a try block that prompts the user for a subscript value and displays the value stored in the corresponding array position. Create a catch block that catches any IndexOutOfRangeException and displays an appropriate error message.

+   2. ArgumentException is an existing class that derives from Exception; use it when one or more of a method's arguments do not fall within an expected range. Create an application named SwimmingWaterTemperature containing a variable that can hold a temperature expressed in degrees Fahrenheit. Within the class, create a method that accepts a parameter for a water temperature and returns true or false, indicating whether the temperature is between 70 and 85 degrees and comfortable for swimming. If the temperature is not between 32 and 212 (the freezing and boiling points of water), it is invalid, and the method should throw an ArgumentException. In the Main() method, continuously prompt the user for data temperature, pass it to the method, and then display a message indicating whether the temperature is comfortable, not comfortable, or invalid.