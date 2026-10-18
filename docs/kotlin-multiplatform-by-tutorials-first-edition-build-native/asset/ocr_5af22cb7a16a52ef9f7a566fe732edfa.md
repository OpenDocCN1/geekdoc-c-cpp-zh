`content` doesn’t.

Try to remove the type from `content` declaration. Android Studio immediately underlines this expression, and if you check the error it says:

> > Not enough information to infer type variable T

This is because `decodeFromString` doesn’t know which type of object it should return. When you define the type at the variable level, `decodeFromString` uses it to know which objects it should return. You can define this type directly on the function if you want to use type inference on the variable declaration:

```
```kotlin
val content by lazy {
    json.decodeFromString<List<RWContent>>(RW_CONTENT)
}
```
```

# Type checks

Both languages use the `is` to check if an object is from a specific type.

# Cast

Casting a variable is similar in both languages. You just need to use the keyword `as` followed by the type of the class that you want to cast.

# Converting between different types

You can easily convert between primitive types by calling `.to<>()` for the type that you want:

```
```kotlin
// Convert String to Integer
"raywenderlich".toInt()

// Convert String to Long
"raywenderlich".toLong()

// Convert String to Float
"raywenderlich".toFloat()

// Convert Int to String
42.toString()

// Convert Int to Long
42.toLong()

// Convert Int to Float
42.toFloat()
```
```