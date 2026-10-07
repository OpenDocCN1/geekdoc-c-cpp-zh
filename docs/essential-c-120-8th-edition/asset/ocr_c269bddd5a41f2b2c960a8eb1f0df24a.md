# 416  Chapter 7: Inheritance

LISTING 7.18: Using Polymorphism to List the PdaItems

```
public class Program
{
    public static void Main()
    {
        PdaItem[] pda = new PdaItem[3];

        Contact contact = new("Sherlock Holmes")
        {
            Address = "221B Baker Street, London, England";n        }
        pda[0] = contact;

        Appointment appointment = new(
            "Soccer tournament", "Estádio da Machava",
            new DateTime(2008, 7, 18), new DateTime(2008, 7, 19));
        pda[1] = appointment;

        contact = new Contact("Anne Frank")
        {
            Address = "Apt 56B, Whitehaven Mansions, Sandhurst, London";
        }
        pda[2] = contact;

        List(pda);
    }

public static void List(PdaItem[] items)
{
    // Implemented using polymorphism. The derived
    // type knows the specifics of implementing
    // GetSummary().
    foreach(PdaItem item in items)
    {
        Console.WriteLine("-");
        Console.WriteLine(item.GetSummary());
    }
}
```

# OUTPUT 7.5

FirstName: Sherlock
LastName: Holmes