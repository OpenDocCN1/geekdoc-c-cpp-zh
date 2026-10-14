We might also be interested in whether a reference is null, so let’s look at the mechanics of comparing one reference with either another reference or the null reference.

# Comparing Two References

If x and y are both references to the same object, they have the same identity and so compare equal via either == or Equals. If they refer to different objects, even if those objects have the same state, x and y won’t compare equal. In Listing 5-6 we use == to compare two reference variables.

```
public sealed class MusicTrack
{
}

var x = new MusicTrack();
var y = new MusicTrack();

Assert.That(x == y, Is.False);
```

Listing 5-6: Comparing references

These x and y reference variables aren’t equal because they refer to different objects, even though both objects have the same state. Rather than assigning constant values to two variables as we did in Listing 5-1, we’re creating new objects on the heap, and the variables are references to those objects. When we examine the generated CIL, on the last line we can see that the two references are compared for equality by using the same ceq instruction as in Listing 5-1:

```
IL_0001: newobj instance void MusicTrack::.ctor()
IL_0006: stloc.0 // x
IL_0007: newobj instance void MusicTrack::.ctor()
IL_000c: stloc.1 // y
IL_000d: ldloc.0
IL_000e: ldloc.1
IL_000f: ceq
```

The newobj instruction creates a new instance of a type and stores a reference to it on the evaluation stack. We create two instances of MusicTrack on the heap, since MusicTrack is a class, and store references to them in the x and y variables, respectively. Since x and y refer to different instances, the variables have different values and thus aren’t equal when compared using ceq.

As far as the ceq instruction is concerned, at run time a reference is just a sequence of bits, in much the same way as a number is represented as a sequence of bits. The ceq instruction merely compares two bit patterns to determine whether they match. Two references to different object instances on the heap have different bit patterns, so they don’t compare equal.