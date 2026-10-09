```
namespace Example;

static class Rotator {
    internal static IEnumerable<T> Rotate<T>(IList<T> list, int delta =
1) {
        for (var i = 0; i < list.Count; i++) {
            yield return list[Mod(i + delta, list.Count)];
        }
    }

    internal static IEnumerable<T> Shift<T>(this IList<T> list, int delta
= 1) {
        for (var i = 0; i < list.Count; i++) {
            yield return list[Mod(i + delta, list.Count)];
        }
    }

    internal static string Str<T>(this IEnumerable<T> list) =>
$"{{string.Join(", ", list)}}";

    private static int Mod(int n, int b) => ((n % b) + b) % b;
}
```

# Sort Numbers