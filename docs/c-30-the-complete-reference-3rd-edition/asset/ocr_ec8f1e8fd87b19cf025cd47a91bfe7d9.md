```
if(!str.Contains("powerful"))
    Console.WriteLine("The sequence powerful was not found.");
}
```

The output is shown here:

The sequence power was found.
The sequence pow was found.
The sequence powerful was not found.

As the output shows, Contains() searches for a matching sequence, not for whole words. Thus, both “pow” and “power” are found. However, since there is no sequence that matches “powerful”, it is (correctly) not found.

Several of the search methods have additional forms that allow you to begin a search at a specified index or to specify a range to search within. All versions of the **String** search methods are shown in Table 22-3.

| Method | Description |
|---|---|
| public bool Contains(string str) | Returns true if the invoking string contains the string specified by str. **False** is returned if str is not found. |
| public bool EndsWith(string str) | Returns true if the invoking string ends with the string passed in str. Otherwise, **false** is returned. |
| public bool EndsWith(string str, StringComparison how) | Returns true if the invoking string ends with the string passed in str. Otherwise, **false** is returned. How the search is performed is specified by how. |
| public bool EndsWith(string str, bool ignoreCase, CultureInfo ci) | Returns true if the invoking string ends with the string passed in str. Otherwise, **false** is returned. If ignoreCase is **true**, the search ignores case differences. Otherwise, case differences matter. The search is conducted using the cultural information passed in ci. |
| public int IndexOf(char ch) | Returns the index of the first occurrence of ch within the invoking string. Returns -1 if ch is not found. |
| public int IndexOf(string str) | Returns the index of the first occurrence of str within the invoking string. Returns -1 if str is not found. |
| public int IndexOf(char ch, int start) | Returns the index of the first occurrence of ch within the invoking string. Searching begins at the index specified by start. Returns -1 if ch is not found. |
| public int IndexOf(string str, int start) | Returns the index of the first occurrence of str within the invoking string. Searching begins at the index specified by start. Returns -1 if str is not found. |

**Table 22-3** The Search Methods Offered by **String**