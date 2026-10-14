The expressions for x and y are both now multiplying a Distance value by the double values returned from Math.Cos and Math.Sin. This code will fail to compile because Distance needs its own overload of operator*.

As with Speed values, multiplying a Distance by a simple number produces a new Distance. The results of Math.Cos and Math.Sin, apart from being out of our control, are scalar values, so when we multiply them by a Distance, the result is another Distance.

Distance also requires an overload of operator- so that the subtraction operation used in the calculation for the y value will compile. As with the multiplication, the expression on the right of the subtraction gives a scalar value, so we add the multiplication and subtraction operators for Distance in Listing 1-21.

```
public static Distance operator*(Distance left, double right)
    => new (left.Amount * right);

public static Distance operator-(Distance left, double right)
    => new (left.Amount - right);
```

*Listing 1-21: Arithmetic operations for Distance values*

With these overloads, we can use the Speed and TimeSpan values naturally together to produce Distance values. Those values, in turn, work seamlessly with the other required expressions.

# Dealing with Design Imperfection

Our displacement method returns a tuple of two double values. However, with our changes, the x and y values being returned have become instances of Distance rather than plain double values. This introduces another terminology problem with respect to the return value: in physics, a distance, like a speed, is always either 0 or a positive value. Combining a distance with the result of a trigonometric function like Cos is a coordinate position, rather than a distance, and can be negative.

We identified the Distance type from the result of multiplying a speed by a time, but there is no straightforward way to distinguish the result of Math.Cos or Math.Sin from a plain number like 0.5, denying us the opportunity to add an overload of the multiplication operator in Distance to return a new type, such as Position, rather than another Distance. We have reached the limits of exploiting the types we have chosen for modeling real-world concepts.

An obstacle like this may be the symptom of a deeper design smell, an indication that the problem might be resolved by a change in design perspective. In this instance, we may be able to achieve a more complete solution by reworking Displacement’s algorithm in terms of a full-fledged Velocity type instead of the relatively primitive Speed and Angle types. Exploring that solution is fairly complex, however, and best left to a text dedicated to modeling physics problems, leaving us with a pragmatic decision to make.