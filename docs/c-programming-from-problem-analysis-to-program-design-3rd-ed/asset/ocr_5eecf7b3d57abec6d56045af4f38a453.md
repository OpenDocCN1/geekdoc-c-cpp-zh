# Example 4-14

```
Student aStudentObject = new Student(1234, "Maria Smith", 97, 75, 87,
    "CS");
average = aStudentObject.CalculateAverage();
```

You may want to look back to Example 4-3. The six argument constructor shown in that example is called here to instantiate the class. The new operator creates the object, aStudentObject. Once a Student object is instantiated, as illustrated in Example 4-14, CalculateAverage( ) can now be invoked. A dot separates the object and the instance method name.

Since CalculateAverage( ) has a return type of double, there must be a place for a value to be returned. It is returned through an assignment statement. Another option would be to return it directly to an output statement. However the only way it can be called or invoked is with an object of the Student class. Example 4-15 shows instantiating another Student object using the constructor that takes one argument (review Example 4-3). Example 4-15 also illustrates using its properties to assign values to the scores and then invoking the instance method with that object. This time the value from the CalculateAverage( ) method is returned to a WriteLine( ) method.

# Example 4-15

```
Student anotherStudentObject = new Student(2345 );
anotherStudentObject.Score1 = 95;
anotherStudentObject.Score2 = 62;
anotherStudentObject.Score3 = 87;
Console.WriteLine("Student ID: " +
    anotherStudentObject.StudentNumber +
    "\nAverage: {0:f1}",
    anotherStudentObject.CalculateAverage());
```

Notice no arguments are needed as parameters to the CalculateAverage( ) method. This is because CalculateAverage( ) is a member of the Student class and has full access to all of the Student class data members. The properties Score1, Score2, Score3 have a public access mode. They were used to assign values to the private instance data members score1, score2, and score3.

![](bbox=[0.15, 0.88, 0.22, 0.95])

Recall to clear a console window and reposition the cursor to the top of the display, invoke Console.Clear().

# Testing Your New Class

A different class is needed for testing and using your class. If you added your class as a second class to the application, as was recommended earlier, you already have that other class. This other class is the class that has Main( ) in it. Here, in Main( ), you can construct objects of