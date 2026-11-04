# TRY IT

In the final Try It of this lesson, you get to experiment with classes, inheritance, and polymorphism. You build Person, Employee, and Manager classes. To test the classes, you build a simple program that creates instances of each class and passes them to a method that takes a Person as a parameter.

# Lesson Requirements

In this lesson, you:

+   - Create a Person class with properties FirstName, LastName, Street, City, State, Zip, Email, and Phone. Give the Person class a GetAddress method that returns the Person's name and address properties as a string in the format:
+     Alice Archer
+     100 Ash Ave
+     Bugsville CO 82010
+   - Derive an Employee class from Person. Add the properties EmployeeId and MailStop.
+   - Derive a Manager class from Employee. Add a DepartmentName property and a DirectReports property of type List<Employee>. Make a GetDirectReportsList method that returns the names of the Manager's Employees separated by newlines.
+   - Make the main program create two Employees named Alice and Bob, a Manager named Cindy who has Alice and Bob in her department, and a Person named Dan.
+   - Make a ShowAddress method that takes a Person as a parameter and displays the Person's address.
+   - On the main form, make buttons that call ShowAddress for each of the people, passing the method the appropriate object.
+   - Make a final button that displays Cindy's list of direct reports.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

# Hints

+   - This example doesn't do anything fancy with the class's properties so you can use auto-implemented properties.
+   - The ShowAddress method should take a Person parameter even though some of the objects it will be passed are Employees or Managers.