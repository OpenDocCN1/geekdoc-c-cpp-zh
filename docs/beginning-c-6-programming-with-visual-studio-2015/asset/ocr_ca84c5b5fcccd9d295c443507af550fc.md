```
}
set
{
    Dictionary[name] = value;
}
}
}
```

# Exercise 2

```
public class Person
{
    private string name;
    private int age;
    public string Name
    {
        get
        {
            return name;
        }
        set
        {
            name = value;
        }
    }
    public int Age
    {
        get
        {
            return age;
        }
        set
        {
            age = value;
        }
    }
    public static bool operator >(Person p1, Person p2) =>
        p1.Age > p2.Age;
    public static bool operator <(Person p1, Person p2) =>
        p1.Age < p2.Age;
    public static bool operator >=(Person p1, Person p2) =>
        !(p1 < p2);
    public static bool operator <=(Person p1, Person p2) =>
        !(p1 > p2);
}
```

# Exercise 3

```
public Person[] GetOldest()
{
    Person oldestPerson = null;
    People oldestPeople = new People();
    Person currentPerson;
    foreach (DictionaryEntry p in Dictionary)
```