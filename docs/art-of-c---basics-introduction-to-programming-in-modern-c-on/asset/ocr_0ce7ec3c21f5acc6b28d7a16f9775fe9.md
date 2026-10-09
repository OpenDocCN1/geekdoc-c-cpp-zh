```
```
14    private static int Compare<T>(T l, T r, T pivot) where T :
        IEquatable<T>, IComparable<T> {
15    var (dl, dr) = (Distance(l, pivot), Distance(r, pivot));
16    return dl.Equals(dr) ? 0 : (dl.CompareTo(dr) > 0 ? 1 : -1);
17    }

19    private static T Distance<T>(T l, T r) where T : IComparable<T> =>
20        (l.Compare(r) > 0) ? Subtract(l, r) : Subtract(r, l);

22    private static T Subtract<T>(T l, T r) where T : notnull =>
23    (l, r) switch {
    (sbyte il, sbyte ir) => (T)(dynamic)(il - ir),
    (short il, short ir) => (T)(dynamic)(il - ir),
    (int il, int ir) => (T)(dynamic)(il - ir),
    (long il, long ir) => (T)(dynamic)(il - ir),
    (nint il, nint ir) => (T)(dynamic)(il - ir),
    (float il, float ir) => (T)(dynamic)(il - ir),
    (double il, double ir) => (T)(dynamic)(il - ir),
    (decimal il, decimal ir) => (T)(dynamic)(il - ir),
    _ => (T)((dynamic)l - (dynamic)r),
33    };

        internal static void Print<T>(IEnumerable<T> arr) =>
36        Console.WriteLine($"{{string.Join(", ", arr)}}");
    }
```
```

# 13.2.1. Explanation

Here’s a sample output:

```
```
$ dotnet run

Pivot = 20
Original array: {64, 34, 25, 12, 22, 11, 90}
Sorted array:  {22, 25, 12, 11, 34, 64, 90}
```
```