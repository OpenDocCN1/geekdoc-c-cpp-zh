```
public IPoint Copy() => Copy((0, 0));
public IPoint Copy((float, float) delta) => new SPoint(X +
delta.Item1, Y + delta.Item2);

public void Deconstruct(out float X, out float Y) => (X, Y) = (
this.X, this.Y);
```