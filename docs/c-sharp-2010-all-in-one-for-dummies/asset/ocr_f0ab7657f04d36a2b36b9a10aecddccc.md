```
if (rightStudent.Grade > leftStudent.Grade)
{
    return 1;
}
return 0;
}
```

Sorting an array of Students is reduced to this single call:

```
void MyMethod(Student[] students) // Where Student implements IComparable<T>
{
    Array.Sort(students); // Sort array of IComparable<Student>s
}
```

You provide the comparator (CompareTo()), and Array does all the work — sounds fair to me.

# Putting it all together

This is the moment you've been waiting for: the complete SortInterface program that uses the features described earlier in this chapter:

```
// SortInterface -- Demonstrates how the interface concept can be used
// to provide an enhanced degree of flexibility in factoring
// and implementing classes.
using System;
namespace SortInterface
{
    // IDisplayable -- An object that can convert itself into a displayable
    // string format (duplicates what you can do by overriding
    // ToString()), but helps me make a point)
    interface IDisplayable
    {
        // Display -- return a string representation of yourself.
        string Display();
    }
    class Program
    {
        public static void Main(string[] args)
        {
            // Sort students by grade...
            Console.WriteLine("Sorting the list of students");
            // Get an unsorted array of students
            Student[] students = Student.CreateStudentList();
            // Use the IComparable<T> interface to sort the array.
            Array.Sort(students);
            // Now use the IDisplayable interface to display the results
            DisplayArray(students);

            // Now sort an array of birds by name using the same routines even
            // though the classes Bird and Student have no common base class.
            Console.WriteLine("Sorting the list of birds");
            Bird[] birds = Bird.CreateBirdList();
            // Notice that it is not necessary to cast the objects explicitly
            // to an array of IDisplayables (and wasn't for Students, either) ...
```

![](bbox=[0.08, 0.66, 0.22, 0.79])