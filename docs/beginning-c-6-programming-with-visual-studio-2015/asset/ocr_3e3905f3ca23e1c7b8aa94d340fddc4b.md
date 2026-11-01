> > **NOTE** Interestingly, multiplying two short values together doesn’t return a short value. Because the result of this operation is quite likely to exceed 32767 (the maximum value a short can hold), it actually returns an int.
> >
> > The conversion process can seem complex at first glance, but as long as you break expressions down into parts by taking the operator precedence order into account, you should be able to work things out.

# COMPLEX VARIABLE TYPES

In addition to all the simple variable types, C# also offers three slightly more complex (but very useful) sorts of variables: enumerations (often referred to as enums), structs (occasionally referred to as structures), and arrays.

# Enumerations

Each of the types you’ve seen so far (with the exception of `string`) has a clearly defined set of allowed values. Admittedly, this set is so large in types such as double that it can practically be considered a continuum, but it is a fixed set nevertheless. The simplest example of this is the bool type, which can take only one of two values: `true` or `false`.

There are many other circumstances in which you might want to have a variable that can take one of a fixed set of results. For example, you might want to have an orientation type that can store one of the values north, south, east, or west.

In situations like this, *enumerations* can be very useful. Enumerations do exactly what you want in this orientation type: They allow the definition of a type that can take one of a finite set of values that you supply. What you need to do, then, is create your own enumeration type called orientation that can take one of the four possible values.

Note that there is an additional step involved here — you don’t just declare a variable of a given type; you declare and detail a user-defined type and then declare a variable of this new type.

# Defining Enumerations

You can use the enum keyword to define enumerations as follows:

```
```text
enum <typeName>
{
    <value1>,
    <value2>,
    <value3>,
    ...
    <valueN>
}
```
```