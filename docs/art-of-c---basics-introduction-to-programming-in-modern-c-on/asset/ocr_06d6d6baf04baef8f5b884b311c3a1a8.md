```
namespace Euclid;

public record RPoint(float X, float Y) : IPoint, IComparable<RPoint> {
    public float Radius() => (float)Math.Sqrt(X * X + Y * Y);

    public int CompareTo(IPoint? other) => other is RPoint rp ?
CompareTo(rp) : 1;

    public int CompareTo(RPoint? other) => other is null ? 1 : (Radius()
- other.Radius()) switch {
        < 0 => -1,
        > 0 => 1,
        _ => 0,
    };

    public static bool operator >(RPoint left, RPoint right) =>
left.Radius() > right.Radius();
    public static bool operator <(RPoint left, RPoint right) =>
left.Radius() < right.Radius();
    public static bool operator >=(RPoint left, RPoint right) =>
left.Radius() >= right.Radius();
    public static bool operator <=(RPoint left, RPoint right) =>
left.Radius() <= right.Radius();

    public IPoint Copy() => Copy((0, 0));
    public IPoint Copy((float, float) delta) => new RPoint(X +
delta.Item1, Y + delta.Item2);
}
```