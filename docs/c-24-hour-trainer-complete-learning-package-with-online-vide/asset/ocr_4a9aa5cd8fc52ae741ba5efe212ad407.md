# 25

# Fine-Tuning Classes

In Lesson 24 you learned how to build constructors and destructors, special methods that execute when an object is created or destroyed. In this lesson you learn about other special methods you can give a class. You learn how to overload and override class methods.

# OVERLOADING METHODS

Lesson 24 mentioned that you can give a class any number of constructors as long as they have different parameter lists. For example, it's common to give a class a parameterless constructor that takes no parameters and one or more other constructors that take parameters.

Making multiple methods with the same name but different parameter lists is called overloading. C# uses the parameter list to decide which version to use when you invoke the method.

For example, suppose you're building a course assignment application and you have built Student, Course, and Instructor classes. You could give the Student class two versions of the Enroll method, one that takes as a parameter the name of a class the student is taking and a second that takes a Course object as a parameter.

You could give the Instructor class similar versions of the Teach method to make the instructor teach a class by name or Course object.

Finally, you could give the Course class different Report methods that:

+   - Display a report in a dialog if there are no parameters.
+   - Append a report to the end of a file if the method receives a FileStream as a parameter.
+   - Save the report into a new file if the method receives a string (the filename) as a parameter.