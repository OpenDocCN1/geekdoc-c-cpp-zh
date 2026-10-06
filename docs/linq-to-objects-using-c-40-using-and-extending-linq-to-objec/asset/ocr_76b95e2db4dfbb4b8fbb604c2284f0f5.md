```
(DateTime.Now - c.DateBirth).Days / 365
};

// ContactName class definition
public class ContactName {
    public string FullName { get; set; }
    public int YearsOfAge { get; set; }

    // constructor needed for
    // object initialization example
    public ContactName() {
    }

    // constructor required for
    // type projection example
    public ContactName(string name, int age) {
        this.FullName = name;
        this.YearsOfAge = age;
    }
}
```

# Return an Anonymous Type-
IEnumerable<TAnonymous>

Anonymous types are a new language feature introduced in C# 3.0 where the compiler creates a type-on-the-fly based on the object initialization expression (the expression on the right side of the initial = sign). Discussed in detail in Chapter 2, this new type is given an uncallable name by the compiler, and without the var keyword (implicitly typed local variables), there would be no way to compile the query. The following query demonstrates projecting to an IEnumerable<T> collection where T is an anonymous type:

```
List<Contact> contacts = Contact.SampleData();

var q = from c in contacts
    select new
{
```