```
// Define the Contact class as inheriting the PdaItem class
public class Contact : PdaItem
{
    public string Address { get; set; }
    public string Phone { get; set; }
}
```

Listing 6.2 shows how to access the properties defined in Contact.

# LISTING 6.2: Using Inherited Methods

```
public class Program
{
    public static void Main()
    {
        Contact contact = new Contact();
        contact.Name = "Inigo Montoya";
        // ...
    }
}
```

![](bbox=[0.19, 0.5, 0.88, 0.86])

Figure 6.1: Refactoring into a Base Class