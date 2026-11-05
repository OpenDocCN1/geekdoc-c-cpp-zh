# 9.8.2. Ref readonly returns

The called method may also declare the return value as ref readonly to return the value by reference, and at the same time enforce that the calling code cannot modify the returned value. The calling method can avoid copying the returned value by storing the value in a local ref readonly. For example,

```
static class RefReturnDemo {
    static ref readonly Coord Move(ref Coord moving) =>
        ref moving; // return ref
    public static void PrintAfterMove(Coord here) {
        ref readonly var t = ref Move(ref here);
        Console.WriteLine($"Lat = {t.Lat}; Lon = {t.Lon}");
    }
}
```