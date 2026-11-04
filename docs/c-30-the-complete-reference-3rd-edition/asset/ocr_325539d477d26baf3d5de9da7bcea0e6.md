```
// Return a zero balance.
static double GetZeroBal() {
    Console.WriteLine("In GetZeroBal().");
    return 0.0;
}

static void Main() {
    double? balance = 123.75;
    double currentBalance;

    // Here, GetZeroBal() is not called because balance
    // contains a value.
    currentBalance = balance ?? GetZeroBal();
    Console.WriteLine(currentBalance);
}
```

In this program, the method GetZeroBal() is not called because balance contains a value. As explained, when the left-hand expression of ?? contains a value, the right-hand expression is not evaluated.

# Nullable Objects and the Relational and Logical Operators

Nullable objects can be used in relational expressions in just the same way as their corresponding non-nullable types. However, there is one additional rule that applies. When two nullable objects are compared using the <, >, <=, or >= operators, the result is false if either of the objects is null. For example, consider this sequence:

```
byte? lower = 16;
byte? upper = null;

// Here, lower is defined, but upper isn't.
if(lower < upper) // false
```

Here, the result of the test for less than is false. However, somewhat counterintuitively, so is the inverse comparison:

```
if(lower > upper) // .. also false!
```

Thus, when one (or both) of the nullable objects used in a comparison is null, the result of that comparison is always false. Thus, null does not participate in an ordering relationship.

You can test whether a nullable object contains null, however, by using the == or != operators. For example, this is a valid test that will result in a true outcome:

```
if(upper == null) // ...
```

When a logical expression involves two bool? objects, the outcome of that expression will be one of three values: true, false, or null (undefined). Here are the entries that are added to the truth table for the & and | operators that apply to bool?.