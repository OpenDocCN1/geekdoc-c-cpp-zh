# Note

If you’re interested in finding out more about functional programming with Haskell, visit the Haskell programming language website at http://www.haskell.org/haskellwiki/Haskell.

Chapter 3, “Writing methods and applying scope,” explained that a typical method consists of four elements: a return type, a method name, a list of parameters, and a method body. A lambda expression contains two of these elements: a list of parameters and a method body. Lambda expressions do not define a method name, and the return type (if any) is inferred from the context in which the lambda expression is used. In the case of the Find method, the predicate processes each item in the collection in return true or false on whether it matches the search criteria. The example that follows the Find method (highlighted in bold) on a List<Person> collection, where Person is a struct. The Find method returns the first item in the list that has the ID property set to 3:

Click here to view code image

```
struct Person
{
    public int ID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}

// // Create and populate the personnel list
List<Person> personnel = new List<Person>();

new Person({ ID = 1, Name = "John", Age = 53 });
new Person({ ID = 2, Name = "Sid", Age = 28 });
new Person({ ID = 3, Name = "Fred", Age = 34 });
new Person({ ID = 4, Name = "Paul", Age = 22 });
```

```
// Find the member of the list that has an ID of 3
Person match = personnel.Find((Person p) => { return p.ID == 3; });
Console.WriteLine("ID: {match.ID}\nName: {match.Name}\nAge:{match.Age}");
```