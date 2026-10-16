```
{
    string[] cities = {"Berlin", "New York ", "Sofia", "Istanbul", "London"};
    List<string> citiesendingwiths = cities.Where(c => c.Length >= 6 && c.Contains("o")).ToList();
    foreach(string c in citiesendingwiths)
    {
        Console.WriteLine(c);
    }
    Console.Read();
}
}
```

This time, you will only see the cities of Sofia and New York on the screen as these are the only ones with the letter ‘o’ and greater than or equal to 6.

# Select Query Operator

Select queries are used mostly with objects that contain several members. It can be used for the retrieval of a specified member in all collection objects and it can be used by any entire object. The basic usage of this query is in the next example:

```
using System;
using System.Collections;
```