```
}
public IEnumerator GetEnumerator()\{
    // skip the header line
    bool header = true;

    foreach (var line in _lines)
        if (header)
            header = false;
        else
            yield return new CsvLine(line, _headers);
}
}
```

Listing 8-9 shows the LINQ query that reads data from a CSV file and filters based on one of the column values. The important aspects of this example are the dynamic keyword in the from clause, and the ability to directly access the properties State, FirstName, and LastName from an instance of CsvLine dynamic type. Even though there is no explicit backing type for those properties, they are mapped from the header row in the CSV file itself. This code will only compile in C# 4.0, and its output is all of the rows (in this case just one) that have a value of “WA” in the third column position (State), as shown in Output 8-2.

# Listing 8-9 Sample LINQ query code that demonstrates how to use dynamic types in order to improve code readability and to avoid the need for strict backing classes—see Output 8-2

```
string content =
"FirstName, LastName, State\n
Troy, Magennis, TX\n
Janet, Doherty, WA";

var q = from dynamic c in new CsvParser(content)
    where c.State == "WA"
    select c;

foreach (var c in q)
```