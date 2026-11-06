easily transfer a class object than a struct. This means that a struct should not be used
when one is need of transferring data to other classes.

Here is another example of a struct in C#:

```
```csharp
using System;
struct Cars {
  public string model;
  public int cc;
  public int passengers;
  public int year;
};
public class carStructure {
  public static void Main(string[] args) {
    Cars Premio;  /* Declare prenio of type Car */
    Cars X6;  /* Declare X6 of type Car */
    /* premio specification */
    Premio.model = "Saloon";
    Premio.cc = 1800;
    Premio.passengers = 5;
    Premio.year = 2010;
    /* X6 specification */
    X6.model = "Saloon";
    X6.cc = 3500;
    X6.passengers = 5;
    X6.year = 2012;
    /* print premio info */
    Console.WriteLine( "Premio model: {0}", Premio.model);
    Console.WriteLine("Premio CC : {0}", Premio.cc);
    Console.WriteLine("Premio passengers : {0}", Premio.passengers);
```
```