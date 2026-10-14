```
public double DistanceInKm(Speed speed, TimeSpan elapsed)
    => speed.InMetersPerSecond / 1000 * elapsed.TotalSeconds;

var velocity = new Velocity(initial, direction);

var distance = DistanceInKm(velocity, TimeSpan.FromHours(2));
```

Listing 4-22: Using an implicit conversion to pass an argument

Although this looks to be a regular call to the DistanceInKm method, the velocity argument first needs to be converted to a Speed. Our type conversion operator makes this possible, and since we made the conversion implicit, the compiler simply inserts the call to that operator when we call DistanceInKm, copying the Velocity argument and Speed return value in the process.

Type conversions need to be used wisely. They can hide all sorts of complexity, quite apart from the copies they usually represent. Implicit conversions happen invisibly by design, leaving only subtle clues in code that employs them, such as in method calls like DistanceInKm in Listing 4-22. Explicit user-defined conversions are syntactically more obvious in the code that uses them, but it’s still easy to overlook that they, too, represent a call to a method.

When a method returns a variable by reference—which we first examined in Chapter 3—we can use that by-reference variable to directly alter the underlying variable, provided neither is read-only. However, remember that ref returns are an optimization feature and shouldn’t be introduced indiscriminately.

All other non-void methods produce values, not variables, meaning we can’t assign to the result directly. If we forget this and misuse a return value, it can result in surprising behavior.

# Modifying Return Type Instances

You saw in Chapter 2 that a variable can be assigned to, but a value can’t. Values are the result of expressions, including method calls, and are immutable. We can’t directly modify the value returned from any method.

One common source of confusion is that value type instances and reference type instances have different behavior in this regard: if the method returns a reference to a mutable type, we can use the returned reference to directly modify the instance in memory, but we can’t modify a mutable value type instance unless we first copy the returned value to a variable. Understanding how value types differ from reference types in this respect will help us avoid some common hazards and better appreciate the best practice of making all value types immutable.

When a return value is a value type instance, we can’t use it to set property values or change any of the value’s public fields. We must assign that value to a variable before we can change it. To demonstrate, Listing 4-23