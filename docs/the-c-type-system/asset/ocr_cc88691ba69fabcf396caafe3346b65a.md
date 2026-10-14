# Comparing with the null Reference

The value of a reference variable is either a reference to an object on the heap or null. We can use == to compare any reference with null to determine whether it refers to an object. If the reference refers to an object, as in Listing 5-7, the reference isn’t equal to null.

```
var x = new MusicTrack();

Assert.That(x == null, Is.False);
```

Listing 5-7: Comparing a reference with null

This comparison also uses the built-in ceq instruction:

```
IL_0016: newobj    instance void MusicTrack::.ctor()
IL_001c: ldloc.1    // x
IL_001d: ldnull
IL_001e: ceq
```

The null reference is a constant value pushed onto the evaluation stack by the ldnull instruction; null doesn’t have a type of its own but can be implicitly converted to any reference type. When we assign null to a reference variable or pass it as an argument to a method, it’s converted automatically to the type of the target variable. Here we can compare x with null because the null reference is compatible with the MusicTrack reference type.

# Comparing Array Variables

C# arrays are always reference types, so comparing array variables works the same way as comparing references. C# arrays are the built-in syntax for declaring and using a sequence of elements that are always allocated on the heap. An array variable is a reference to the elements of the array. In Listing 5-8, we create two arrays with identical elements and use == to compare them.

```
int[] x = { 10, 20 };
int[] y = { 10, 20 };

Assert.That(x == y, Is.False);
```

Listing 5-8: Implicitly initializing and comparing two arrays

The compiler deduces the size of each array based on the values we use to initialize them. The two arrays have identical elements but compare unequal because comparing two arrays with == performs a reference comparison using the intrinsic ceq instruction. The x and y variables in Listing 5-8 are references to different arrays and thus don’t compare equal, so the test passes.

When we compare two array variables, the comparison doesn’t consider the array elements; it uses only the identity of the two array variables, so two array references compare equal only if they refer to the same array instance. To check whether two arrays have the same elements, we must manually