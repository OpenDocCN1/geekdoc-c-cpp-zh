As a small side note, C# also lets you omit the parentheses before the open brace if you want to call a parameterless constructor. The line below produces the same IL as the line above:

```
```csharp
String s = new Employee { Name = "Jeff", Age = 45 }.ToString().ToUpper();
```
```

If a property’s type implements the **IEnumerable** or **IEnumerable<T>** interface, then the property is considered to be a collection, and initializing a collection is an additive operation as opposed to a replacement operation. For example, suppose I have the following class definition:

```
```csharp
public sealed class Classroom {
    private List<String> m_students = new List<String>();
    public List<String> Students { get { return m_students; } }

    public Classroom() {}
}
```
```

I can now have code that constructs a **Classroom** object and initializes the **Students** collection as follows:

```
```csharp
public static void M() {
    Classroom classroom = new Classroom {
        Students = { "Jeff", "Kristin", "Aidan", "Grant" }
    };

    // Show the 4 students in the classroom
    foreach (var student in classroom.Students)
        Console.WriteLine(student);
}
```
```

When compiling this code, the compiler sees that the **Students** property is of type **List<String>** and that this type implements the **IEnumerable<String>** interface. Now, the compiler assumes that the **List<String>** type offers a method called **Add** (because most collection classes actually offer an **Add** method that adds items to the collection). The compiler then generates code to call the collection’s **Add** method. So, the code shown above is converted by the compiler into this:

```
```csharp
public static void M() {
    Classroom classroom = new Classroom();
    classroom.Students.Add("Jeff");
    classroom.Students.Add("Kristin");
    classroom.Students.Add("Aidan");
    classroom.Students.Add("Grant");

    // Show the 4 students in the classroom
    foreach (var student in classroom.Students)
        Console.WriteLine(student);
}
```
```

If the property’s type implements **IEnumerable** or **IEnumerable<T>** but the type doesn’t offer an **Add** method, then the compiler does not let you use the collection initialize syntax to add items to the collection; instead, the compiler issues something like the following