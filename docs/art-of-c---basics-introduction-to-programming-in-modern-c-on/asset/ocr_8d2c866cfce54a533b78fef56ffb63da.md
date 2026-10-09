# 7.2. Code Reading - Print the Multiplication Table

```
```csharp
internal static void WriteTable(int low, int high) {
    var table = CreateTable(low, high);
    var axis = System.Linq.Enumerable.Range(low, high - low);

    Write("          ");
    foreach (var v in axis) {
        Write("{0,4:D}", v);
    }
    WriteLine("");

    Write("     ---");
    foreach (var _ in axis) {
        Write("{0,4:S}", "--");
    }
    WriteLine("");

    foreach (var l in axis) {
        Write("{0,4:D}", l);
        Write("{0,4:C}", '|');
        foreach (var r in axis) {
            Write("{0,4:D}", table[l - low, r - low]);
        }
        WriteLine("");
    }
}
```
```

There is some small differences in these two implementations (for example, we use the *string.Format()* style formatting in this version, just for illustration), but the main difference is that this version uses *foreach* rather than *for*.

In order to do this, we create a variable of a certain collection type, *axis*.

```
```csharp
var axis = System.Linq.Enumerable.Range(low, high - low);
```
```

We will learn more about the *System.Linq* namespace later in the book, but the