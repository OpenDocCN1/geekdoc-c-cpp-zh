The following code (excerpted from the example) shows how to instantiate a new, empty list for the string type. In other words, this list can hold only strings:

```
```csharp
// List<T>: note angle brackets plus parentheses in
// List<T> declaration; T is a "type parameter".
// List<T> is a "parameterized type."
// Instantiate for string type.
List<string> nameList = new List<string>();
sList.Add("one");               // Compiler error here!
sList.Add(3);                    // Compiler error here!
sList.Add(new Student("du Bois"));   // Compiler error here!
```
```

You add items to a List<T> by using its Add() method. The preceding code snippet successfully adds one string to the list, but then it runs into trouble trying to add first an integer and then a Student. The list was instantiated for strings, so the compiler rejects both attempts.

The next code fragment instantiates a completely new list for type int and then adds two int values to the list. Afterward, the foreach loop iterates the int list, printing out the ints:

```
```csharp
// Instantiate for int.
List<int> intList = new List<int>();
intList.Add(3);                 // Fine.
intList.Add(4);
Console.WriteLine("Printing intList:");
foreach (int i in intList)  // foreach just works for all collections.
{
    Console.WriteLine("int i = " + i);
}
```
```

The following bit of code instantiates a new list to hold Students and adds two students with its Add() method. But then notice the array of Students, which I add to the student list using its AddRange() method. AddRange() lets you add a whole array or (almost) any other collection to the list, all at once:

```
```csharp
// Instantiate for Student.
List<Student> studentList = new List<Student>();
Student student1 = new Student("Vigil");
Student student2 = new Student("Finch");
studentList.Add(student1);
studentList.Add(student2);
Student[] students = { new Student("Mox"), new Student("Fox") };
studentList.AddRange(students);  // Add whole array to List
Console.WriteLine("Num students in studentList = " + studentList.Count);
```
```

(Don't worry about the "new Student" stuff. I get to that topic in Book II.)

![](bbox=[0.05, 0.9, 0.2, 1.0])

You can easily convert lists to arrays and vice versa. To put an array into a list, use the list's AddRange() method as just described. To convert a list to an array, call the list's ToArray() method: