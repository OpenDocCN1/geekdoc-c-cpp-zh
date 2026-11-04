```
office.Area = 4200;
 office.Floors = 3;

Console.WriteLine("house has:\n " +
    house.Floors + " floors\n " +
    house.Occupants + " occupants\n " +
    house.Area + " total area");

Console.WriteLine();

Console.WriteLine("office has:\n " +
    office.Floors + " floors\n " +
    office.Occupants + " occupants\n " +
    office.Area + " total area");
    office.AreaPerPerson();
}
```

This program generates the following output, which is the same as before:

```
house has:
  2 floors
  4 occupants
  2500 total area
  625 area per person

 office has:
  3 floors
  25 occupants
  4200 total area
  168 area per person
```

Let's look at the key elements of this program, beginning with the AreaPerPerson() method, itself. The first line of AreaPerPerson() is

```
public void AreaPerPerson() {
```

This line declares a method called AreaPerPerson that has no parameters. It is specified as public, so it can be used by all other parts of the program. Its return type is void. Thus, AreaPerPerson() does not return a value to the caller. The line ends with the opening curly brace of the method body.

The body of AreaPerPerson() consists solely of this statement:

```
Console.WriteLine("  " + Area / Occupants + " area per person");
```