
a list of references to objects, so adding an integer or floating-point number to the list will box the value so that a reference can be obtained.

## LISTING 8.5: Subtle Box and Unbox Instructions

```
class DisplayFibonacci
{
    static void Main()
    {
        int totalCount;
        System.Collections.ArrayList list =
            new System.Collections.ArrayList();

        Console.Write("Enter a number between 2 and 1000:");
        totalCount = int.Parse(Console.ReadLine());

        // Execution-time error:
        // list.Add(0);  // Cast to double or 'D' suffix required.
        //                       Whether cast or using 'D' suffix,
        //                       CIL is identical.
        list.Add((double)0);
        list.Add((double)1);
        for (int count = 2; count < totalCount; count++)
        {
            list.Add(
                ((double)list[count - 1] +
                 (double)list[count - 2]));
        }

        foreach (double count in list)
        {
            Console.Write("{0}, ", count);
        }
    }
}
```

## OUTPUT 8.1

```
Enter a number between 2 and 1000:42
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597,
2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418,
317811, 514229, 832040, 1346269, 2178309, 3524578, 5702887, 9227465,
14930352, 24157817, 39088169, 63245986, 102334155, 165580141,
```

The code shown in Listing 8.5, when compiled, produces five box and three unbox instructions in the resultant CIL.

- 1. The first two box instructions occur in the initial calls to list.Add(). The signature for the ArrayList method is int Add(object value). As such, any value type passed to this method is boxed.
- 2. Next are two unbox instructions in the call to Add() within the for loop. The return from an ArrayList’s index operator is always object because that is what ArrayList contains. To add the two values, you need to cast them back to doubles. This cast from a reference to an object to a value type is implemented as an unbox call.
- 3. Now you take the result of the addition and place it into the ArrayList instance, which again results in a box operation. Note that the first two unbox instructions and this box instruction occur within a loop.
- 4. In the foreach loop, you iterate through each item in ArrayList and assign the items to count. As you saw earlier, the items within ArrayList are references to objects, so assigning them to a double is, in effect, unboxing each of them.
- 5. The signature for Console.WriteLine(), which is called within the foreach loop, is void Console.Write(string format, object arg). As a result, each call to it boxes the double to object.

Every boxing operation involves both an allocation and a copy; every unboxing operation involves a type check and a copy. Doing the equivalent work using the unboxed type would eliminate the allocation and type check. Obviously, you can easily improve this code’s performance by eliminating many of the boxing operations. Using an object rather than double in the last foreach loop is one such improvement. Another would be to change the ArrayList data type to a generic collection (see Chapter 11). The point being made here is that boxing can be rather subtle, so developers need to pay special attention and notice situations where it could potentially occur repeatedly and affect performance.

Another unfortunate boxing-related problem also occurs at runtime: If you wanted to change the initial two Add() calls so that they did not use a cast (or a double literal), you would have to insert integers into the array list. Since ints will implicitly be converted to doubles, this would appear to be an innocuous modification. However, the casts to double from within the for loop, and again in the assignment to count in the foreach loop, would

```
struct Angle : IAngle
{
    // ...
    // NOTE: This makes Angle mutable, against the general
    //         guideline
    public void MoveTo(int degrees, int minutes, int seconds)
    {
        _Degrees = degrees;
        _Minutes = minutes;
        _Seconds = seconds;
    }
}
```

```
class Program
{
    static void Main()
    {
        // ...
        Angle angle = new Angle(25, 58, 23);
        object objectAngle = angle; // Box
        Console.Write(((Angle)objectAngle).Degrees);
        
        // Unbox, modify unboxed value, and discard value
        ((Angle)objectAngle).MoveTo(26, 58, 23);
        Console.Write(", " + ((Angle)objectAngle).Degrees);
        
        // Box, modify boxed value, and discard reference to box
        ((IAngle)angle).MoveTo(26, 58, 23);
        Console.Write(", " + ((Angle)angle).Degrees);
        
        // Modify boxed value directly
        ((IAngle)objectAngle).MoveTo(26, 58, 23);
        Console.WriteLine(", " + ((Angle)objectAngle).Degrees);
        
        // ...
    }
}
```

## OUTPUT 8.2

```
25, 25, 25, 26
```

Listing 8.7 uses the Angle struct and IAngle interface. Note also that the IAngle.MoveTo() interface changes Angle to be mutable. This change brings out some of the idiosyncrasies of mutable value types and, in so doing, demonstrates the importance of the guideline to make structs immutable.

In the first two lines of Listing 8.6, you initialize `angle` and then box it into a variable called `objectAngle`. Next, you call `MoveTo` to change `Hours` to 26. However, as the output demonstrates, no change actually occurs the first time. The problem is that to call `MoveTo()`, the compiler unboxes `objectAngle` and (by definition) makes a copy of the value. Value types are copied by value—that is why they are called value types. Although the resultant value is successfully modified at execution time, this copy of the value is discarded and no change occurs on the heap location referenced by `objectAngle`.

Recall our analogy that suggested variables of value type are like pieces of paper with the value written on them. When you box a value, you make a photocopy of the paper and put the copy in a box. When you unbox the value, you make a photocopy of the paper in the box. Making an edit to this second copy does not change the copy that is in the box.

In the next example, labeled with the comment “box, modify boxed value, and discard reference to box,” a similar problem occurs in reverse. Instead of calling `MoveTo()` directly, the value is cast to `IAngle`. The conversion to an interface type boxes the value, so the runtime copies the data in `angle` to the heap and provides a reference to that box. Next, the method call modifies the value in the referenced box. The value stored in variable `angle` remains unmodified.

In the last case, the cast to `IAngle` is a reference conversion, not a boxing conversion. The value has already been boxed by the conversion to `object` in this case, so no copy of the value occurs on this conversion. The call to `MoveTo()` updates the `_Hours` value stored in the box, and the code behaves as desired.

As you can see from this example, mutable value types are quite confusing because it is often unclear when you are mutating a copy of the value, rather than the storage location you actually intend to change. By avoiding mutable value types in the first place, you can eliminate this sort of confusion.

> **Guidelines**
> 
> **AVOID** mutable value types.

## ADVANCED TOPIC

### How Boxing Can Be Avoided during Method Calls

Anytime a method is called with a receiver of value type, the receiver (represented by `this` in the body of the method) must be a variable, not a value, because the method might be trying to mutate the receiver. Clearly, it must be mutating the receiver’s storage location, rather than mutating a copy of the receiver’s value and then discarding it. The second and fourth cases in Listing 8.7 illustrate how this fact affects the performance of a method invocation on a boxed value type.

In the second case, the unboxing conversion logically produces the boxed value, not a reference to the storage location on the heap that contains the boxed copy. Which storage location, then, is passed as the `this` to the mutating method call? It cannot be the storage location from the box on the heap, because the unboxing conversion produces a copy of that value, not a reference to that storage location.

When this situation arises—a variable of value type is required but only a value is available—one of two things happens: Either the C# compiler generates code that makes a new, temporary storage location and copies the value from the box into the new location, resulting in the temporary storage location becoming the needed variable, or the compiler produces an error and disallows the operation. In this case, the former strategy is used. The new temporary storage location is then the receiver of the call; after it is mutated, the temporary storage location is discarded.

This process—performing a type check of the boxed value, unboxing to produce the storage location of the boxed value, allocating a temporary variable, copying the value from the box to the temporary variable, and then calling the method with the location of the temporary storage—happens every time you use the unbox-and-then-call pattern, regardless of whether the method actually mutates the variable. Clearly, if it does not mutate the variable, some of this work could be avoided. Because the C# compiler does not know whether any particular method you call will try to mutate the receiver, it must err on the side of caution.

These expenses are all eliminated when calling an interface method on a boxed value type. In such a case, the expectation is that the receiver will be the storage location in the box if the interface method mutates the storage
