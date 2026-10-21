As you might expect, typeof returns "string" when the value is a string; "number" when the value is a number (regardless of integer or floating-point values); "boolean" when the value is a Boolean; and "undefined" when the value is undefined.

The tricky part involves null.

```
console.log(typeof null); // "object"
```

When you run typeof null, the result is "object". But why an object when the type is null? (In fact, this has been acknowledged as an error by TC39, the committee that designs and maintains JavaScript. You could reason that null is an empty object pointer, making "object" a logical return value, but that’s still confusing.)

The best way to determine if a value is null is to compare it against null directly, like this:

```
console.log(value === null); // true or false
```

# **COMPARING WITHOUT COERCION**

Notice that this code uses the triple equals operator (===) instead of the double equals operator. The reason is that triple equals does the comparison without coercing the variable to another type. To understand why this is important, consider the following:

```
console.log("5" == 5); // true
console.log("5" === 5); // false
console.log(undefined == null); // true
console.log(undefined === null); // false
```

When you use the double equals, the string "5" and the number 5 are considered equal because the double equals converts the string into a number before it makes the comparison. The triple equals operator doesn’t consider these values equal because they are two different types. Likewise, when you compare undefined and null, the double equals says that they are equivalent, while the triple equals says they are not. When you’re trying to identify null, use triple equals so that you can correctly identify the type.