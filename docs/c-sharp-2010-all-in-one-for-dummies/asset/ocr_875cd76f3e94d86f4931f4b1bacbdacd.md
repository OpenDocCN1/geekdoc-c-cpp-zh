Thus you could write the previous example this way:

```
```
public class Student
{
    public string firstName;
    public string lastName;
    public void SetName(string firstName, string lastName)
    {
        // Explicitly reference the "current object" referenced by this.
        this.SetFirstName(firstName);
        this.SetLastName(lastName);
    }
    public void SetFirstName(string name)
    {
        this.firstName = name;
    }
    public void SetLastName(string name)
    {
        this.lastName = name;
    }
}
```
```

Notice the explicit addition of the keyword this. Adding it to the member references doesn't add anything because this is assumed. However, when Main() makes the following call, this references student1 throughout SetName() and any other method it may call:

Book II  
Chapter 4  
Let Me Say This  
about This

```
```
student1.SetName("John", "Smith");
```
```

# ### When is this explicit?

You don't normally need to refer to this explicitly because it is understood where necessary by the compiler. However, two common cases require this. You may need it when initializing data members, as in this example:

```
```
class Person
{
    public string name;     // This is this.name below.
    public int id;          // And this is this.id below.
    public void Init(string name, int id)   // These are method arguments.
    {
        this.name = name;   // Argument names same as data member names
        this.id = id;
    }
}
```
```

The arguments to the Init() method are named name and id, which match the names of the corresponding data members. The method is then easy to read because you know immediately which argument is stored where. The only problem is that the name name in the argument list obscures the name of the data member. The compiler complains about it.