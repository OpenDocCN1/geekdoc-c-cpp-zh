
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

## Putting it all together

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

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_368_0.png)

```
Array.Sort(birds);
DisplayArray(birds);
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
// DisplayArray -- Display an array of objects that
// implement the IDisplayable interface.
public static void DisplayArray(IDisplayable[] displayables)
{
foreach(IDisplayable displayable in displayables)
Console.WriteLine("{0}", displayable.Display());
}
}
// ------------ Students -- Sort students by grade ------
// Student -- Description of a student with name and grade
class Student : IComparable<Student>, IDisplayable
{
// Constructor -- Initialize a new student object.
public Student(string name, double grade)
{ Name = name; Grade = grade; }
// CreateStudentList -- To save space here, just create
// a fixed list of students.
static string[] names = {"Homer", "Marge", "Bart", "Lisa", "Maggie"};
static double[] grades = {0, 85, 50, 100, 30};
public static Student[] CreateStudentList()
{
Student[] students = new Student[names.Length];
for (int i = 0; i < names.Length; i++)
{
students[i] = new Student(names[i], grades[i]);
}
return students;
}
// Access read-only properties.
public string Name { get; private set; }
public double Grade { get; private set; }
// Implement the IComparable interface:
// CompareTo -- Compare another object (in this case, Student objects)
// and decide which one comes after the other in the sorted array.
public int CompareTo(Student rightStudent)
{ // Compare the current Student (call her 'left')
// the other student (call her 'right').
Student leftStudent = this;
// Now generate a -1, 0 or 1 based on the Sort criteria (the student's
// grade). Double's CompareTo method would work, too.
if (rightStudent.Grade < leftStudent.Grade)
{
return -1;
}
if (rightStudent.Grade > leftStudent.Grade)
{
return 1;
}
return 0;
}
// Display -- Implement the IDisplayable Interface:
```

```
public string Display()
{
    string padName = Name.PadRight(9);
    return String.Format("{0}: {1:N0}", padName, Grade);
}
// --------Birds -- Sort birds by their names--------
// Bird -- Just an array of bird names
class Bird : IComparable<Bird>, IDisplayable
{
    // Constructor -- initialize a new Bird object.
    public Bird(string name) { Name = name; }
    // CreateBirdList -- Return a list of birds to the caller.
    // Use a canned list here to save space.
    static string[] birdNames =
        {"Oriole", "Hawk", "Robin", "Cardinal", "Bluejay", "Finch", "Sparrow"};
    public static Bird[] CreateBirdList()
    {
        Bird[] birds = new Bird[birdNames.Length];
        for(int i = 0; i < birds.Length; i++)
        {
            birds[i] = new Bird(birdNames[i]);
        }
        return birds;
    }
    public string Name { get; private set; }
    // Implement the IComparable interface:
    // CompareTo -- Compare the birds by name; use the
    // built-in String class compare method.
    public int CompareTo(Bird rightBird)
    {
        // Compare the "current" bird to the "right hand object" bird.
        Bird leftBird = this;
        return String.Compare(leftBird.Name, rightBird.Name);
    }
    // Display -- Implement the IDisplayable interface.
    public string Display() { return Name; }
}
```

The Student class (it's in the middle of the program listing) implements the IComparable<T> and IDisplayable interfaces, as described earlier. The CompareTo() method compares the students by grade, which results in the students being sorted by grade. Student's Display() method returns the name and grade of the student.

The other methods of Student include the read-only Name and Grade properties, a simple constructor, and a CreateStudentList() method. This method just returns a fixed list of students for the code to work on.

The Bird class at the bottom of the listing also implements the interfaces IComparable<T> and IDisplayable. The class implements CompareTo() by comparing the names of the birds using String.Compare(). So one bird is greater than another if its name is greater. Bird.CompareTo() alphabetizes the list. Bird's Display() method just returns the name of the bird.

## Getting back to the Main() event

If you've followed along with us so far, you're set up for the good part, back in Main(). The CreateStudentList() method is used to return an unsorted list, which is stored in the array students.

You might think it necessary to cast the array of students into an array of comparableObjects so that you can pass the students to Array's Sort() method:

```
IComparable<Student>[] comparables = (IComparable<Student>[])students;
```

But not so, my friend. Sort() sees that the array passed in consists of objects that implement IComparable<something> and simply calls CompareTo() on each Student object to sort them. Great, eh?

The sorted array of Student objects is then passed to the locally defined DisplayArray() method. DisplayArray() uses foreach to iterate through an array of objects that implement a Display() method (guaranteed by the objects' having implemented IDisplayable). In the loop, it calls Display() on each object and displays the result to the console using WriteLine().

The program in Main() continues by sorting and displaying birds! I think we can agree that birds have nothing to do with students. Yet the same Sort() and DisplayArray() methods work on Bird as on Student.

The output from the program appears:

```
Sorting the list of students
Lisa : 100
Marge : 85
Bart : 50
Maggie : 30
Homer : 0

Sorting the list of birds
Bluejay
Cardinal
Finch
Hawk
Oriole
Robin
Sparrow
Press Enter to terminate...
```

## Unifying Class Hierarchies

Figure 8-1 shows the Robot and Animal hierarchies. Some, but not all, of the classes in each hierarchy not only inherit from the base classes, Robot or Animal, but they also implement the IPet interface (not all animals are pets, you see), as shown in the following code — I skipped lots of details:
