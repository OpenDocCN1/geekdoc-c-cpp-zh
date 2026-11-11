```
cout<<"Name "<<Name;
}
};
// The Student class simply derives itself from the Person base class
class Student:public Person {
};
int main () {
// Since the derived class has access to the properties and functions
of the base class , these can be accessed via the Student object
Student stud1 ;
stud1.ID=1;
stud1.Name="John";
stud1.Display();
return 0;
}
```

With this program, the output is as follows:

ID 1

Name John

We can also redefine the Display function in the Student class. But if you look at the above example, you will notice that the Display function in the Person class has the display text as ID and Name. But suppose we wanted to have the display name as Student ID and Student name in the student class, we can redefine the Display function. Let’s look at an example of this.

Example 4: The following program shows how to use an inherited class with redefined functions.