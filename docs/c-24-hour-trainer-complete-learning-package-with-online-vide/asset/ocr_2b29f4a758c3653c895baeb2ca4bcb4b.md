5. It's always better to prevent the user from making a mistake than it is to display an error message. Copy the program you wrote for Exercise 4 and make the following changes:

+   - Remove the previous error messages.
+   - Enable the Add button only if both TextBoxes have non-blank text and the list doesn't already contain a person with those first and last names.
+   - Enable the Remove button only if both TextBoxes have non-blank text and the list contains a person with those first and last names.

6. Make a program that defines the following classes and interfaces:

+   - An IWolf interface with PackName and Rank properties, and a WolfInfo method that returns a string. (In classes that implement IWolf, make this method return the person's name and pack name.)
+   - A Person class with FirstName and LastName properties and an overridden ToString method.
+   - An Employee class that inherits from Person, adds a new EmployeeId property, and makes ToString include EmployeeId.
+   - A Werewolf class derived from Person and IWolf.
+   - A WereEmployee class derived from Employee and IWolf.

Create instances of the Person, Employee, Werewolf, and WereEmployee classes. Place them all in a List<Person> and place those that you can in a List<IWolf>. Loop through the lists and display the objects' information in two ListBoxes.

7. Copy the program you built for Exercise 6 and modify it so WereEmployee inherits from Werewolf. What are the advantages and disadvantages to this approach? Which approach seems better? (Look at the comments in the WereEmployee class in the download to see my thoughts.)

> NOTE Please select the videos for Lesson 27 online at www.wrox.com/go/csharp24hourtrainer2videos.