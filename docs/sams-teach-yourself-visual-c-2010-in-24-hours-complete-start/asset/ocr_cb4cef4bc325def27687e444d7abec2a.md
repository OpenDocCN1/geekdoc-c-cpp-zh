Collection initializers enable you to specify one or more element initializers, which enable you to initialize a collection that implements IEnumeerable. Using a collection initializer enables you to omit multiple calls to the Add method of the collection, instead letting the compiler add the calls for you. An element initializer can be a value, an expression, or an object initializer.

> **Collection Initializers Work Only with Add Methods**  
Collection initializers can be used only with collections that contain an Add method. This means they cannot be used for collections such as Stack<T> and Queue<T>.

The syntax for a collection initializer is similar to an array initializer. You must still call the new operator but can then use the array initialization syntax to populate the collection. Listing 9.3 shows the same example as Listing 9.2, but uses List<int> and a collection initializer.

# **LISTING 9.3** Collection Initialization

```
class Program
{
    static void Main()
    {
        List<int> list = new List<int>() { 0, 2, 4, 6, 8 };
    }
}
```

Collection initializers can also be more complex, enabling you to use object initializers for the element initializers, as shown in Listing 9.4.

# **LISTING 9.4** Complex Collection Initialization

```
class Program
{
    static void Main()
    {
        List<Contact> list = new List<Contact>()
        {
            new Contact() { FirstName = "Scott", LastName = "Dorman" },
            new Contact() { FirstName = "Jim", LastName = "Morrison" },
            new Contact() { FirstName = "Ray", LastName = "Manzarek" }
        };
        
        foreach(Contact c in list)
        {
            Console.WriteLine(c);
        }
    }
}
```