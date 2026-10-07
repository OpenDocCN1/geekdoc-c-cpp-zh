# Pattern Matching 435

```
// Discard last name portion of tuple
,
{
  // Property of Princess Buttercup tuple
  FirstName: string buttercupFirstName
  Console.WriteLine("$ { inigoFirstNameLength }, { buttercupFirstName }}");
}
else {
  // ...
}
// ...
```

In this example, couple is of the following type:

(Person, (string FirstName, string LastName))

As such, the first match occurs on the outer tuple, (inigo, buttercup). Next, positional pattern matching is used against inigo, leveraging the Person deconstructor. This selects a (FirstName, LastName) tuple, from which property pattern matching is used to extract the Length of the inigo.FirstName value. The LastName portion of the positional pattern matching is discarded with an underscore. Finally, property pattern matching is used to select buttercup.FirstName.

While pattern matching is a powerful means to select data, it is not without a caution: Be mindful of the comments of Listing 7.32, it is likely challenging to understand the code. Without them, it would be even harder:

```
if (couple is ( { Length: int inigoFirstNameLength }, _ ), { FirstName: string buttercupFirstName }}) { ...}
```

Even so, where pattern matching really proves useful is in switch statements and expressions.