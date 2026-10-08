This function returns the file extension from the filename parameter as an option. It will only succeed if the filename has passed a dot (.) in it, and then it will return the tail from dot as a Some value. In every other case, it will return None. A bit of F# Interactive exploration helps to test this:

```
> FileExtension "data";
val it : string option = None
> FileExtension "data";
val it : string option = Some "*
> FileExtension "data.dat";
val it : string option = Some "*.dat"
> FileExtension "*";
val it : string option = None
> FileExtension null;
val it : string option = None
>
```

# Using Records

You can define a record type by listing its fields and types inside braces:

```
type Person =
  { FirstName: string
  LastName: string
  Age: int
  Children: Person list
  mutable LastSeen: System.DateTime option }
```

You can just create a new record value by giving the values of its fields inside braces:

```
let john =
  { FirstName = "John"
  LastName = "Smith"
  Age = 32
  Children = []
  LastSeen = None }
```

In the definition and the value constructor, fields can be separated by semicolons — this comes in handy when you want to put multiple fields on the same line.

At times, you may need to copy records to create new ones, perhaps with certain fields changed:

```
let sally =
  { john with
  FirstName = "Sally"
  Age = 25 }
```

One important thing to remember is that records are not value types. Switching one of the fields to mutable will reveal this:

```
let shadowOfSally = sally
```