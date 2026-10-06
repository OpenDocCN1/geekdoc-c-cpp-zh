```
>> a = 5
=> 5
>> b = 3
=> 3
>> a / b
=> 1
>> MyConstant = a.to_f / b.to_f
=> 1.6666666666666667
>> MyConstant = 5
(irb):76: warning: already initialized constant MyConstant
(irb):75: warning: previous definition of MyConstant was here
=> 5
```

The `Constant` class allows us to create variables that should not change in value. This can be useful when we want to define values that require protection, such as the length of the User Datagram Protocol (UDP) header, while doing packet manipulation. Constants are differentiated from other variable types. They must start with a capital letter.

# Note

Even changing a constant generates a warning, notice that the value of `MyConstant` does change to 5 from its original value. It is possible to change the value of a constant, but doing so will generate a warning to indicate that something has happened.

# Arrays and hashes

In the preceding section, we looked at arrays and hashes in action. These structures are important enough that we should look a bit deeper before continuing.

Arrays in Ruby are indexed lists of values or objects starting with an index of 0. Arrays, like all Ruby objects, are classes with their own methods. Many of these methods will be reminiscent of the Python `List` object. These include methods for `push` and `pop` for removing values from the array, as well as an append operator, `<<`.

Let's take a look at hashes. Notice how we use symbols with our hashes.