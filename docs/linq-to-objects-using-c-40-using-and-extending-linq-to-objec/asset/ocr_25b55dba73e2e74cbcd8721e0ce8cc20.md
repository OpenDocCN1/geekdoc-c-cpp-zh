# Listing 5-27 The SkipWhile and TakeWhile operators skip or return elements while their predicate argument returns true—see Output 5-15

```
string sampleString =
@"# comment line 1
# comment line 2
Data line 1
Data line 2

This line is ignored
"

var q = sampleString.Split('\n')
  .SkipWhile(line => line.StartsWith("#"))
  .TakeWhile(line => !string.IsNullOrEmpty(line.Trim()));

foreach (var s in q)
  Console.WriteLine(s);
```

# Output 5-15

Data line 1
Data line 2

# Quantifier Operators–All, Any, and Contains

The Quantifier operators, All, Any, and Contains return Boolean result values based on the presence or absence of certain data within a sequence. These operators could all be built by creating queries that filter the data using a Where clause and comparing the resulting sequence element count to see if it is greater than zero. But these operators are optimized for their purpose and return a result at the first possible point, avoiding iterating an entire sequence (often referred to as short-circuit evaluation).

# All Operator

The All operator returns the Boolean result of true if all elements in a sequence pass the predicate function supplied.