# Object Oriented Programming using C#

# Object Roles and the Importance of Polymorphism

# Activity 4

Taking the same diagram and having invoked the code directly below decide which of the following lines (a) or (b) would be valid inside the method Help(Student s)...

```
Student s = new Student();
Lecturer l = new Lecturer();
l.help(s);
```

![](bbox=[0.192, 0.253, 0.807, 0.44])

+   a) s.PrintTimetable();
b) s.ApplyForLoan();

# Feedback 4

+   a) This is valid - we can invoke this method on a Student object and also on a FtStudent object (as the method is inherited).
b) Not Valid! While we can invoke this method on a FtStudent object, and we are passing a FtStudent as a parameter to the Help() method, the Help() method cannot know that the object passed will be a FtStudent (it could be any object of type Student). Therefore there is no guarantee that the object passed will support this method. Hence this line of code would generate a compiler error.