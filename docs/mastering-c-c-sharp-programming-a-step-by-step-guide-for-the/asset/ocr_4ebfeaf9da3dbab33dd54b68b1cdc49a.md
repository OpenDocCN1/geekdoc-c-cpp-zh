What we have done here is created a collection that contains data from a specified class. We used the class called Cat which contains properties called Name and Age. From this, we want a list of the names of the Cats. Using the var keyword, we instruct the compiler that we want the variable type defined depending on what the result is that was assigned to the right of the operator’s equal sign.

# Using Lambda Expressions with Anonymous Types

This is an example of how lambda expressions are used with anonymous types:

```
using System;
using System.Collections.Generic;
using System.Linq;
class Cat
{
    public string Name { get; set; }
    public int Age { get; set; }
}
class demo{
    static void Main()
    {
        List<Cat> Cats = new List<Cat>() {
            new Cat { Name = "Molly", Age = 4 },
            new Cat { Name = "Simon", Age = 0 },
            new Cat { Name = "Serendipity", Age = 3 }
        };
        var newCatsList = Cats.Select(x => new { Age = x.Age, FirstLetter = x.Name[0] });
```