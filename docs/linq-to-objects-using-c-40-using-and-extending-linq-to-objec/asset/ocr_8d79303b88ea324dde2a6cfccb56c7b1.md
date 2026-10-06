# 66 CHAPTER 3 WRITING BASIC QUERIES

**Table 3-2** The Built-in StringComparer Functions to Control Case Sensitivity and Culture-aware String Ordering

| Comparator | Description |
| InvariantCulture | Performs a case-sensitive string comparison using the word comparison rules of the invariant culture. |
| InvariantCultureIgnoreCaseCase | Performs a case-insensitive string comparison using the word comparison rules of the invariant culture. |
| Ordinal | Performs a case-sensitive ordinal string comparison. |
| OrdinalIgnoreCase | Performs a case-insensitive ordinal string comparison. |

Listing 3-10 demonstrates the syntax and effect of using the built-in string comparer instances offered by the .NET Framework. The Console output is shown in Output 3-7, where the default case-sensitive result can be forced to case-insensitive.

**Listing 3-10** Case and culture sensitive/insensitive ordering using StringComparer functions—see Output 3-7

```
string[] words = new string[] {
    "Janet", "Janet", "janet", "Janet" 
};

var cs = words.OrderBy(w => w);
var ci = words.OrderBy(w => w,
    StringComparer.CurrentCultureIgnoreCase);

Console.WriteLine("Original:");
foreach (string s in cs)
    Console.WriteLine(" " + s);

Console.WriteLine("Case Sensitive (default):");
foreach (string s in cs)
    Console.WriteLine(" " + s);

Console.WriteLine("Case Insensitive:");
foreach (string s in ci)
    Console.WriteLine(" " + s);
```