```
>= 60 => "LX",
>= 50 => "L",
>= 40 => "XL",
>= 30 => "XXX",
>= 20 => "XX",
_ => "X",
});
number %= 10;
} else {
sb.Append(number switch {
>= 9 => "IX",
>= 8 => "VIII",
>= 7 => "VII",
>= 6 => "VI",
>= 5 => "V",
>= 4 => "IV",
>= 3 => "III",
>= 2 => "II",
_ => "I",
});
number = 0;
}

return sb.ToString();
}
```
```

# # Euclidean Distance

*euclid-distance/SPoint.cs*

```
namespace Euclid;

public readonly struct SPoint : IPoint, IEquatable<SPoint>, IComparable<SPoint> {
public float X { get; init; }
```