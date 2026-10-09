+   4. In the foreach loop, you iterate through each item in ArrayList and assign the items to count. As you saw earlier, the items within ArrayList are references to objects, so assigning them to a double is, in effect, unboxing each of them.

+   5. The signature for Console.WriteLine(), which is called within the foreach loop, is void Console.Write(string format, object arg). As a result, each call to it boxes the double to object.

Every boxing operation involves both an allocation and a copy; every unboxing operation involves a type check and a copy. Doing the equivalent work using the unboxed type would eliminate the allocation and type check. Obviously, you can easily improve this code's performance by eliminating many of the boxing operations. Using an object rather than double in the last foreach loop is one such improvement. Another would be to change the ArrayList data type to a generic collection (see Chapter 12). The point being made here is that boxing can be rather subtle, so developers need to pay special attention and notice situations where it could potentially occur repeatedly and affect performance.

Another unfortunate boxing-related problem also occurs at runtime: If you wanted to change the initial two Add() calls so that they did not use a cast (or a double literal), you would have to insert integers into the array list. Since ints will implicitly be converted to doubles, this would appear to be an innocuous modification. However, the casts to double from within the for loop, and again in the assignment to count in the foreach loop, would fail. The problem is that immediately following the unbox operation is an attempt to perform a memory copy of the value of the boxed int into a double. You cannot do this without first casting to an int, because the code will throw an InvalidCastException at execution time. Listing 9.6 shows a similar error commented out and followed by the correct cast.

# **LISTING 9.6: Unboxing Must Be to the Underlying Type**

```
```
// ...
int number;
object thing;
double bigNumber;

number = 42;
thing = number;
```
```