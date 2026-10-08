# Looking at a Program That CAN_BE_USED_AS Example 345

```
public string Display() {
    string padName = Name.PadRight(9);
    return String.Format('{0}: {1:NO}', padName, Grade);
}
```

```
// Sort birds by their names
// Bird -- Just an array of bird names.
class Bird : IComparable<Bird>, IDisplayable {
    // Constructor -- Initialize a new Bird object.
    public Bird(string name) : base(name) {}
    // CreateBirdList -- Return a list of birds to the caller;
    static string[] _birdnames = {
        "Robin", "Cardinal", "Bluejay", "Finch", "Sparrow";
    };
    public static List<Bird> CreateBirdList() {
 }
```

```
{
Bird[] birds = new Bird[_birdNames.Length];
for (int i = 0; i < birds.Length; i++) {
    birds[i] = new Bird(_birdNames[i]);
}
return birds;
}
public string Name { get; set; }
// Implement the IDisplayable interface:
// Compare birds by name; use the
// Built-in String.Compare method.
public int CompareTo(Bird right) {
    // Compare the 'current' bird to the 'right hand object' bird.
    Bird leftBird = this;
    return String.Compare(leftBird.Name, rightBird.Name);
}
// Display -- Implement the IDisplayable interface.
public string Display() { return Name; }
}
```

The Student class (it's in the middle of the program list) implements the IComparable<T> and IDisplayable interfaces, described earlier. The CompareTo() method compares the students by grade, which results in the students being sorted by grade. Student's Display() method returns the name and grade of the student.

The other methods of Student include the read-only Name and Grade properties, a simple constructor, and a CreateStudentList() method. This method just creates a fixed list of students to work on.

The Bird class at the bottom of the list also implements the interfaces IComparable<T> and IDisplayable. The class implements CompareTo() by comparing the names of the birds using String.Compare(). So one bird is greater than another if its name is greater. Bird.CompareTo() alphabetizes the list. Bird's Display() method returns the name of the interfaces