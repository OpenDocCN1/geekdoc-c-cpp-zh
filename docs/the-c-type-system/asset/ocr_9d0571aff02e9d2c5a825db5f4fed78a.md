by refactoring the implementation. Listing 1-9 shows our current code for `Displacement`.

```
public static (double, double)
Displacement(Angle angle, Speed speed, TimeSpan elapsedTime)
{
    var x = speed.Amount * elapsedTime.TotalSeconds * Math.Cos(angle.Size);
    var y = speed.Amount * elapsedTime.TotalSeconds * Math.Sin(angle.Size)
          - 0.5 * 9.81 * Math.Pow(elapsedTime.TotalSeconds, 2);

    return (x, y);
}
```

*Listing 1-9: The current Displacement implementation*

This code works correctly, but we have some issues to take care of. We’ve made the code more verbose by using the Speed, Angle, and TimeSpan types as parameters, requiring us to access properties of those parameters to obtain their values. Note that we use the TotalSeconds property here; one common error is to use the Seconds property of a TimeSpan object when the intention is to obtain the total number of seconds being represented, but Seconds returns only the seconds component of the TimeSpan. Given a TimeSpan representing 1 minute precisely, the Seconds property would return 0, while the value for TotalSeconds would be 60.

The Displacement method would be clearer if we could use the variables *directly* in the algorithm, like this:

```
var x = speed * elapsedTime * Math.Cos(angle);
var y = speed * elapsedTime * Math.Sin(angle)
      - 0.5 * 9.81 * Math.Pow(elapsedTime, 2);
```

The algorithm also relies on three hard-coded values. Magic numbers like this often indicate that we need to provide names to clarify their purpose. It’s common to find the same magic number used in more than one place, so if the value changed for any reason, we’d need to hunt for every use and make sure we updated them all.

While we can see that multiplying by 0.5 is the same as dividing by 2, the meaning of 9.81 is much less obvious. The value 0.5 and the 2 used in the call to Math.Pow are simply arithmetic values; giving them names might obscure their purpose rather than clarifying it. The value 9.81, on the other hand, stands out as having a more significant purpose. Once again, to understand the meaning of this number, we need prior knowledge that 9.81 is an approximation of the effects of Earth’s gravity on an object. We’ll address this issue first with the simple fix of naming this value.

# Replacing Magic Numbers with Named Constants

Replacing magic numbers in code with a descriptive name clarifies their meaning to readers unfamiliar with the algorithm’s details. One way to do this is to create a new value type, similar to Speed, to represent the measurement. However, when we need only a few well-known values, using named