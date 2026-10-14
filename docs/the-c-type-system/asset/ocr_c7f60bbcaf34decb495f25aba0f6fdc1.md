reference, known as a reference return value, or simply a ref return. We mark a value as being a ref return by adding the ref keyword, as we do when modifying by-reference method parameters. The Mail class in Listing 3-25 has a Destination property that returns the destination field value by reference.

```
public sealed class Mail
{
    public Mail(string name, Address address)
        => (Addressee, destination) = (name, address);

    public string Addressee { get; }

    public ref Address Destination => ref destination;

    private Address destination;
}
```

Listing 3-25: The Destination property returning the destination field value by reference

Note that we need to add the ref keyword to the property and to the variable being returned by reference.

When we access a property that returns its value by reference, we can also receive that value by reference without copying it at all. A by-reference variable, or ref local, is a local variable that refers to the same variable as the ref return. This is best illustrated with a simple example. In Listing 3-26, we receive the ref return value from Mail.Destination by using a local reference variable.

```
var address = new Address ("62 West Wallaby Street",
    "Wigan", "Lancashire", "WG7 7FU");

var letter = new Mail("G Lad Esq.", address);

ref var local = ref letter.Destination;
```

Listing 3-26: Consuming a value returned by reference

This local variable is an alias to the destination field within the letter instance, not a copy of its value. Again, note that we have to use the ref modifier on both the target variable and the property access; if we forget either, the compiler will give us an error. If we omit both, we simply copy the property’s value by value into a normal variable.

# Preventing Modifications to Data

Just as with by-reference parameters, ref return values and ref locals introduce an alias to a value. If we modify a value through such an alias, we need to make sure we know where those changes will be visible.

We can use the ref local reference to mutate the field in letter too, although in this example we can only assign it a completely new value, since Address is a read-only struct. Listing 3-27 demonstrates that modifying the ref local also changes the field of the letter variable.