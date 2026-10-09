If you run the program as before:

```
```
dotnet build -t:Rebuild -p:StartupObject=Roman.RcNumeral
dotnet run
```
```

Here’s the sample output:

```
```
$ dotnet run

r1 = RcNumeral { Number = 1234, Roman = MCCXXXIV }
r2 = RcNumeral { Number = 2022, Roman = MMXXII }
r3 = RcNumeral { Number = 2022, Roman = MMXXII }

r1 != r2
r2 == r3
```
```

Although these are reference variables, they follow the value-equality semantics. In particular, r2 and r3, which are distinct reference variables which point to two different underlying data (e.g., in two different memory locations), are *considered equal* in this implementation using records, by default.

Note that we get a reasonable implementation of the `ToString()` method for free (based on the two public properties that we declare, `Number` and `Roman`) when we use records (unlike in the case of structs or classes).

We can still override this method if a different output format is desired. For example, as before,

```
```
public override string ToString() =>
    NumeralHelper.ToNumeralString(number);
```
```

Note the interesting syntax when we define the `RcNumeral` record: