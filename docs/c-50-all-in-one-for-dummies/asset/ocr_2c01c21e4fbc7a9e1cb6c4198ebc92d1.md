```
return birds;
}

// Access read-only property.
public string Name { get; private set; }

// Implement the IComparable interface:
// CompareTo - Compare the birds by name; use the
// built-in String class compare method.
public int CompareTo(Bird rightBird)
{
    // We'll compare the "current" bird to the
    // "right hand object" bird.
    Bird leftBird = this;

    return String.Compare(leftBird.Name, rightBird.Name);
}

// Implement the IDisplayable interface:
// Display - returns the name of the bird.
public string Display() { return Name; }
}
```

The Student class (it's in the middle of the program listing) implements the IComparable<T> and IDisplayable interfaces, as described earlier. The CompareTo() method compares the students by grade, which results in the students being sorted by grade. Student's Display() method returns the name and grade of the student.

The other methods of Student include the read-only Name and Grade properties, a simple constructor, and a CreateStudentList() method. This method just returns a fixed list of students for the code to work on.

The Bird class at the bottom of the listing also implements the interfaces IComparable<T> and IDisplayable. The class implements CompareTo() by comparing the names of the birds using String.Compare(). So one bird is greater than another if its name is greater. Bird.CompareTo() alphabetizes the list. Bird's Display() method just returns the name of the bird.

# Getting back to the Main() event

If you've followed along so far, you're set up for the good part, back in Main(). The CreateStudentList() method is used to return an unsorted list, which is stored in the array students.

You might think it necessary to cast the array of students into an array of comparableObjects so that you can pass the students to Array's Sort() method:

```
IComparable<Student>[] comparables = (IComparable<Student>[])students;
```