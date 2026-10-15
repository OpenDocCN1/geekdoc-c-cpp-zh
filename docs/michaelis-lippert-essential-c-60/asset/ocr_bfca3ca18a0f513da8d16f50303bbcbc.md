For example, instances of a generic class, Pair<Contact> and Pair<PdaItem>, are not type-compatible even when the type arguments are themselves compatible. In other words, the compiler prevents the conversion (implicit or explicit) of Pair<Contact> to Pair<PdaItem>, even though Contact derives from PdaItem. Similarly, converting Pair<Contact> to the interface type IPair<PdaItem> will also fail. See Listing 11.40 for an example.

# LISTING 11.40: Conversion between Generics with Different Type Parameters

```
// ...
// Error: Cannot convert type ...
Pair<PdaItem> pair = (Pair<PdaItem>) new Pair<Contact>();
IPair<PdaItem> duple = (IPair<PdaItem>) new Pair<Contact>();
```

But why is this not legal? Why are List<T> and Pair<T> not covariant? Listing 11.41 shows what would happen if the C# language allowed unrestricted generic covariance.

# LISTING 11.41: Preventing Covariance Maintains Homogeneity

```
//...
Contact contact1 = new Contact("Princess Buttercup"),
Contact contact2 = new Contact("Inigo Montoya");
Pair<Contact> contacts = new Pair<Contact>(contact1, contact2);
```

```
// This gives an error: Cannot convert type ...
// But suppose it did not.
// IPair<PdaItem> pdaPair = (IPair<PdaItem>) contacts;
// This is perfectly legal, but not type-safe.
// pdaPair.First = new Address("123 Sesame Street");
...
```

An IPair<PdaItem> can contain an address, but the object is really a Pair<Contact> that can contain only contacts, not addresses. Type safety is completely violated if unrestricted generic covariance is allowed.

Now it should also be clear why a list of strings may not be used as a list of objects. You cannot insert an integer into a list of strings, but you can insert an integer into a list of objects; thus it must be illegal to cast a list of strings to a list of objects, an error the compiler can enforce.

# Enabling Covariance with the out Type Parameter Modifier in C# 4.0

You might have noticed that both of the problems described earlier as consequences of unrestricted covariance arise because the generic pair and the