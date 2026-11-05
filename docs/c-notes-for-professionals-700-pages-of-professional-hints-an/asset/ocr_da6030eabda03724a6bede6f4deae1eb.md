```
```csharp
public int Age { get; set; }
public string Clothes { get; set; }

public override bool Equals(object obj)
{
    var person = obj as Person;
    if(person == null) return false;
    return Name == person.Name && Age == person.Age; //the clothes are not important when comparing two persons
}

public override int GetHashCode()
{
    return Name.GetHashCode() + Age;
}
}
```
```

```
```csharp
var person1 = new Person { Name = "Jon", Age = 20, Clothes = "some clothes" };
var person2 = new Person { Name = "Jon", Age = 20, Clothes = "some other clothes" };

bool result = person1.Equals(person2); // result is true
```
```

Also using LINQ to make different queries on persons will check both Equals and GetHashCode:

```
```csharp
var persons = new List<Person>
{
    new Person{ Name = "Jon", Age = 20, Clothes = "some clothes"},
    new Person{ Name = "Dave", Age = 20, Clothes = "some other clothes"},
    new Person{ Name = "Jon", Age = 20, Clothes = ""}
};

var distinctPersons = persons.Distinct().ToList();//distinctPersons has Count = 2
```
```

# Section 6.4: Equals and GetHashCode in IEqualityComparator

For given type Person:

```
```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string Clothes { get; set; }
}
```
```

```
```csharp
List<Person> persons = new List<Person>
{
    new Person{ Name = "Jon", Age = 20, Clothes = "some clothes"},
    new Person{ Name = "Dave", Age = 20, Clothes = "some other clothes"},
    new Person{ Name = "Jon", Age = 20, Clothes = ""}
};

var distinctPersons = persons.Distinct().ToList();// distinctPersons has Count = 3
```
```

But defining Equals and GetHashCode into an IEqualityComparator:

```
```csharp
public class PersonComparator : IEqualityComparer<Person>
{
    public bool Equals(Person x, Person y)
    {
        return x.Name == y.Name && x.Age == y.Age; //the clothes are not important when comparing
    }
```
```