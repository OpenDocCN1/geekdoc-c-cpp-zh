If one prefers the object initializer syntax, then they can make all or most of the primary constructor parameters optional. Or, they can provide additional constructors that require no or fewer parameters.

The *Stock* record includes an instance method, `UpdatePrice()`: 

```
public Stock UpdatePrice(decimal newPrice) => this with { Price =
 newPrice, PreviousPrice = Price };
```

The implementation uses what is called the "non-destructive mutations". The data of the *Stock* object does not change when we call `UpdatePrice()`. Instead, it returns a *new* *Stock* object.

The `with` keyword is used to create a copy of an existing object (*this* object in this case) with a few select property values modified (inside the curly braces).

One can imagine that this can be very useful when dealing with large immutable record types. Instead of using a constructor or an object initializer, which may require initializing many variables, we simply use an existing record as a "template".

Furthermore, this syntax clearly indicates the underlying intention: The new object, or record, created this way is "based on" this particular existing object/record. Any properties that are not explicitly overwritten through this non-destructive mutation syntax will have the same values as those of the "template" object.

We have seen the use of the *this* keyword before, in the context of defining extension methods. That is a bit of a special case.

The keyword *this*, in general, is used to refer to "the current object", or "me", so to speak, inside a class, record, or struct definition. In particular, the *this* object is available in all instance properties and instance methods.

We have been carefully using the words, "types" and "objects", throughout this book. Unfortunately, the name of the base class in C# is *object*. This *object* is a