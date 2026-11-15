```
var patent3 =
new
{
patent1.Title,
Year = patent1.YearOfPublication
};

System.Console.WriteLine("() ({1})",
patent1.Title, patent1.YearOfPublication);
System.Console.WriteLine("() ({1})",
patent2.Title, patent2.YearOfPublication);

Console.WriteLine();
Console.WriteLine(patent1);
Console.WriteLine(patent2);

Console.WriteLine();
Console.WriteLine(patent3);
}
```

The corresponding output is shown in Output 5.8.

# Output 5.8:

```
Bifocals (1784)
Phonograph (1877)
{ Title = Bifocals, YearOfPublication = 1784 }
{ Title = Phonograph, YearOfPublication = 1877 }
{ Title = Bifocals, Year = 1784 }
```

Listing 5.33 demonstrates the assignment of an anonymous type to an implicitly typed (var) local variable.

When the compiler encounters the anonymous type syntax, it generates a CIL class with properties corresponding to the named values and data types in the anonymous type declaration. Although there is no available name in C# for the generated type, it is still statically typed. For example, the properties of the type are fully accessible. In Listing 5.33, patent1.Title and patent2.YearOfPublication are called within the Console.WriteLine() statement. Any attempts to call nonexistent members will