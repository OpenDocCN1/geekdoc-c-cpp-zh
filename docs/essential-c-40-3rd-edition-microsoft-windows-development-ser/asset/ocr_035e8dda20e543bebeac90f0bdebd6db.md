```
{
Dictionary<string,string> dictionary = new
Dictionary<string,string>();

int index = 0;

dictionary.Add(index++.ToString(), "object");
dictionary.Add(index++.ToString(), "byte");
dictionary.Add(index++.ToString(), "uint");
dictionary.Add(index++.ToString(), "ulong");
dictionary.Add(index++.ToString(), "float");
dictionary.Add(index++.ToString(), "char");
dictionary.Add(index++.ToString(), "bool");
dictionary.Add(index++.ToString(), "ushort");
dictionary.Add(index++.ToString(), "decimal");
dictionary.Add(index++.ToString(), "int");
dictionary.Add(index++.ToString(), "sbyte");
dictionary.Add(index++.ToString(), "short");
dictionary.Add(index++.ToString(), "long");
dictionary.Add(index++.ToString(), "void");
dictionary.Add(index++.ToString(), "double");
dictionary.Add(index++.ToString(), "string");

Console.WriteLine("Key Value Hashcode");
Console.WriteLine("--- ----- --------");

foreach (KeyValuePair<string, string> i in dictionary)
{
Console.WriteLine("{0,-5}{1,-9}{2}", i.Key, i.Value, i.Key.GetHashCode());
}
}
```

# OUTPUT 16.3:

| Key | Value | Hashcode |
|---|---|---|
| 0 | -- object -- | -843952752 |
| 1 | byte | -623352753 |
| 2 | uint | -642352754 |
| 3 | ulong | -842352755 |
| 4 | float | -842352756 |
| 5 | char | -842352757 |
| 6 | bool | -842352758 |
| 7 | ushort | -842352759 |
| 8 | decimal | -642352744 |
| 9 | int | -842352745 |
| 10 | sbyte | -842352749 |
| 11 | short | -643446LB5 |
| 12 | long | -843532401 |
| 13 | void | -843597937 |
| 14 | double | -843663473 |
| 15 | string | -843721009 |