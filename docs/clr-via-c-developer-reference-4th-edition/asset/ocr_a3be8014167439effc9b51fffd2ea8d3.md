Now that you know boxing works, let's talk about unboxing. Let's say that you want to grab the first element out of the ArrayList by using the following code.

```
Point p = (Point) a[0];
```

Here you're taking the reference (or pointer) contained in element 0 of the ArrayList and trying to put it into a Point value type, for this to work, all the fields contained in the boxed Point object must be copied into the value type variable, p, which is on the thread's stack. The CLR accomplishes this in two steps. First, the address of the Point fields in the boxed Point object is obtained. Then, this process is called unboxing. Then, the values of these fields are copied from the heap to the stack-based value type instance.

Unboxing is not the exact opposite of boxing. The unboxing operation is much less costly than boxing. Unboxing is really just the operation of obtaining a pointer to the raw value type (data fields) contained within an object. In fact, the pointer refers to the unboxed portion in the boxed instance. So, unlike boxing, unboxing does not involve the copying of any bytes. Having made this important clarification, it is important to note that an unboxing operation is typically followed by copying.

Obviously, boxing and unboxing operations hurt your application's performance in terms of speed and memory, so you should be aware of what the compiler generates to perform these operations and try to write code that minimizes this code generation.

Internally, here's exactly what happens when a boxed value type is unboxed:

+   1. If the variable reference to the boxed value type instance is null, a NullReferenceException is thrown.

+   2. If the reference does not refer to an object that is a boxed instance of the desired value type, an InvalidCastException is thrown.

The second item in the list means the following list that your code will not work as you might expect.

```
public static void Main() {
Int32 x = 5;
Object o = x; // Box x refers to the boxed object
Int16 y = (Int16)o; // Throws InvalidCastException
}
```

Logically, it makes sense to take the boxed Int32 that o refers to and cast it to Int16. However, the cast must be the exact unboxed value type—Int32 in this case. Here's the right way to write this code.

```
public static void Main() {
Int32 x = 5;
Object o = x; // Box x refers to the boxed object
Int16 y = (Int16)(Int32) o; // Unbox to the correct type and
}
```

> The CLR also allows you to unbox a value type into a nullable version of the same value type. This is discussed in Chapter 19.