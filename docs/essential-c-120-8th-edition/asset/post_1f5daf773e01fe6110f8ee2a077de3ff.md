
```csharp
public override int GetHashCode() =>
    (Degrees, Minutes, Seconds).GetHashCode();
#endif UsingTupleToGenerateHashCode
}
```

# Boxing

We know that variables of value types directly contain their data, whereas variables of reference types contain a reference to another location. What happens when a value type is converted to one of its implemented interfaces or to its root class, object? The result of the conversion must be a reference to a storage location that contains something that looks like an instance of a reference type, but the variable contains a value of value type. Such a conversion, which is known as boxing, has special behavior. Converting a value of value type that directly refers to its data to a reference type that refers to a location on the garbage-collected heap involves several steps.

- Memory is allocated on the heap that will contain the value type’s data and the other overhead necessary to make the object look like every instance of a managed object of the reference type (namely, a SyncBlockIndex and method table pointer).

- The value of the value type is copied from its current storage location into the newly allocated location on the heap.

- The result of the conversion is a reference to the new storage location on the heap.

The reverse operation is called unboxing. The unboxing conversion first checks the type of the boxed value is the same as the type to which the value is unboxed, and results in a copy of the value stored in the heap location.

Boxing and unboxing are important to consider; boxing has some performance and behavioral implications. Besides learning how to recognize these conversions within C# code, a developer can count the box/unboxing instructions in a

```csharp
Console.Write("Enter an integer between 2 and 1000: ");
```

# Boxing 525

```csharp
Console.WriteLine($"{inputText} is not a valid integer.");
return;
if (totalCount == 7) // Magic number used for testing
{
    // Triggers exception when retrieving value as double.
    list.Add(0); // Cast to double or 'D' suffix required.
    // Whether cast or using 'D' suffix,
    // CIL is identical.
}
else
{
    list.Add((double)0);
}
list.Add((double)1);
for(int count = 2; count < totalCount; count++)
{
    list.Add(
        (double)list[count - 1] +
        (double)list[count - 2]
    );
}
// Using a foreach to clarify the box operation rather than
// Console.WriteLine(string.Join(", ", list.ToArray()));
foreach (double? count in list)
{
    Console.Write("{0},", count);
}
```

OUTPUT 9.1
Enter a number between 2 and 1000: **42**
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418, 317811, 514229, 832040, 1346269, 2178309, 3254587, 5702887, 9227465, 14930352, 24157817, 39088169, 63245986, 102334155, 165580141,

The code shown in List 9.9, when compiled, produces five box instructions and three unbox instructions in the resultant CIL.

- 1. The first two box instructions occur in the initial calls to list.Add(). The signature for the ArrayList method is Add(object value). As such, any value type passed to this method is boxed.

- 2. Next are two unbox instructions in the call to Add() within the for loop. The return from an ArrayList's index operator is always object because that is what ArrayList contains. To add the two values, you need to cast them back to doubles. This cast from a reference to an object to a value type is implemented as an unbox call.

- 3. Now you take the result of the addition and place it into the ArrayList instance, which again results in a box operation. Note that the first two unbox instructions and this box instruction occur within a loop.

- 4. In the foreach loop, you iterate through each item in ArrayList and assign the items to count. As you saw earlier, the items within ArrayList are references to objects, so assigning them to a double is, in effect, unboxing each of them.

- 5. The signature for Console.WriteLine(), which is called within the foreach loop, is void Console.Write(string format, object arg). As a result, each call to the double converts to object.

Every boxing operation involves both an allocation and a copy; every unboxing operation involves a type check and a copy. Doing the equivalent work using the unboxed type would eliminate the allocation and type check. Obviously, you can easily improve this code's performance by eliminating many of the boxing operations. Using an object rather than double in the last foreach loop is one such improvement. Another would be to change the ArrayList data type to a generic collection (see Chapter 12). The point being made here is boxing can be rather subtle, so developers need to pay special attention and notice situations where it could potentially occur repeatedly and affect performance.

Another unfortunate boxing-related problem also occurs at runtime: calling Add() without first casting to a double (or using a double list), you could insert integers into the array list. Since ints will implicitly be converted to doubles, this would appear to be an innocuous modification. However, the casts to double when retrieving the value from within the foreach loop would fail. The problem is that the unbox operation is immediately followed by an attempt to perform a memory copy of the value of the boxed int.

- 9. It is important that we use a collection of type object, not a strongly typed collection like a generic collection, as discussed in Chapter 12.

# Boxing 527

# 528 Chapter 9: Introducing Structs

# ADVANCED TOPIC

# Value Types in lock

# Value Types in lock

C# supports a lock statement for synchronizing code. The problem with using value types in the lock statement is that lock requires a reference type. Listing 9.2 points out the idiosyncrasies of mutable value types and, in so doing, demonstrates the importance of the guideline that advocates making structs immutable.

# 9.27 Subtle Boxing Idiosyncrasies

```csharp
interface IAngle {
    void MoveTo(int degrees, int minutes, int seconds);
}

struct Angle : IAngle {
    private int _degrees;
    private int _minutes;
    private int _seconds;

    public Angle(int degrees, int minutes, int seconds)
    {
        _degrees = degrees;
        _minutes = minutes;
        _seconds = seconds;
    }

    public int Degrees
    {
        get => _degrees;
        set { _degrees = value; }
    }

    public int Minutes
    {
        get => _minutes;
        set { _minutes = value; }
    }

    public int Seconds
    {
        get => _seconds;
        set { _seconds = value; }
    }

    public void MoveTo(int degrees, int minutes, int seconds)
    {
        _degrees = degrees;
        _minutes = minutes;
        _seconds = seconds;
    }
}
```

# 9.26 Unboxing Must Be to Type

```csharp
int number;
object thing;
double bigNumber;

Angle angle = new(25, 58, 23);
thing = angle; // Box
Console.WriteLine(((double)thing).Degrees); // ERROR: Cannot convert type 'Angle' to 'double'
```

# 5.1

# 529

```csharp
Angle angle = new(25, 58, 23);
// Example 1: Simple box operation
object objectAngle = angle; // Box
Console.Write(((Angle)objectAngle).Degrees);
```

```csharp
// Example 2: Unbox, modify unboxed value,
// and discard value
((Angle)objectAngle).MoveTo(26, 58, 23);
Console.Write("" + ((Angle)objectAngle).Degrees);
```

```csharp
// Example 3: Box, modify boxed value,
// and discard reference to box
((IAngle)angle).MoveTo(26, 58, 23);
Console.Write("" + ((Angle)angle).Degrees);
```

```csharp
// Example 4: Modify boxed value directly
((IAngle)objectAngle).MoveTo(26, 58, 23);
Console.WriteLine("" + ((Angle)objectAngle).Degrees);
```

```text
{
  ...
}
```

# OUTPUT 9.2

```
25, 25, 25, 26
```

Listing 9.11 uses the Angle struct and IAngle interface. Note also that the IAngle.MoveTo() interface changes Angle to be mutable. This change brings out the idiosyncrasies of mutable value types and, in so doing, demonstrates the importance of the guideline that advocates making structs immutable.

In Example 1 of Listing 9.11, after you initialize angle, no change occurs the variable called objectAngle. Next, Example 2 calls MoveTo() to change _Degrees to 26. However, as the output demonstrates, no actually occurs the first time. The problem is to call MoveTo(), the compiler unboxes objectAngle and (by definition) makes a copy of the value. Value types are copied by value—that is why they are called value types. Although the resultant value is successfully modified at execution time, this copy of the value is discarded and no change occurs on the heap location referenced by objectAngle.
