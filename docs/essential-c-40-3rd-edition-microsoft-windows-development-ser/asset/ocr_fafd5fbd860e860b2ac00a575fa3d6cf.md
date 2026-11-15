possible to implement IWriteableSettingsProvider without supplying any read capability. Listing 7.6's FileSettingsProvider is unaffected, but if it used explicit member implementation, specifying which interface a member belongs to changes slightly.

# Extension Methods on Interfaces

Perhaps one of the most important features of extension methods is the fact that they work with interfaces in addition to classes. The syntax is identical to that of extension methods for classes. The extended type (the first parameter and the parameter prefixed with this) is the interface that we extend. Listing 7.10 shows an extension method for IListable(). It is declared on IListable.

# LISTING 7.10: Interface Extension Methods

```
class Program
{
    public static void Main()
    {
        Contact[] contacts = new Contact[6];
        contacts[0] = new Contact(
            "Dick", "Traci",
            "123 Main St., Spokane, WA 99037",
            "123-123-1234");
        // ...

        // Classes are implicitly converted to
        // their supported interfaces
        contacts.List(Contact.Headers);

        Console.WriteLine();

        Publication[] publications = new Publication[3] {
            new Publication("Celebration of Discipline",
                "Richard Foster", 1978),
            new Publication("Orthodoxy",
                "G.K. Chesterton", 1908),
            new Publication(
                "The Hitchhiker's Guide to the Galaxy",
                "Douglas Adams", 1979)
        };
        publications.List(Publication.Headers);
    }
}
```