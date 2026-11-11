
It is possible that future libraries will use *variable handles* instead of reflection for reading and writing fields. A `VarHandle` is similar to a `Field`. You can use it to read or write a specific field of any instance of a specific class. However, to obtain a `VarHandle`, the library code needs a `Lookup` object:

```java
public Object getFieldValue(Object obj, String fieldName,
                             Lookup lookup)
        throws NoSuchFieldException, IllegalAccessException
{
    Class<?> cl = obj.getClass();
    Field field = cl.getDeclaredField(fieldName);
    VarHandle handle = MethodHandles.privateLookupIn(cl, lookup)
        .unreflectVarHandle(field);
    return handle.get(obj);
}
```

This works provided the `Lookup` object is generated in the module that has the permission to access the field. Some method in the module simply calls `MethodHandles.lookup()`, which yields an object encapsulating the access rights of the caller. In this way, one module can give permission for accessing private members to another module. The practical issue is how those permissions can be given with a minimum of hassle.

While we can still do so, let us look at a generic `toString` method that works for any class (see [Listing 5.16]). The generic `toString` method uses `getDeclaredFields` to obtain all instance fields and the setAccessible convenience method to make all fields accessible. For each field, it obtains the name and the value. Each value is turned into a string by recursively invoking `toString`.

The generic `toString` method needs to address a couple of complexities. Cycles of references could cause an infinite recursion. Therefore, the `ObjectAnalyzer` keeps track of objects that were already visited. Also, to peek inside arrays, you need a different approach. You’ll learn about the details in the next section.

```java
57            }
58        }
59        r += "]";
60        cl = cl.getSuperclass();
61      }
62      while (cl != null);
63
64      return r;
65   }
66 }
```

## java.lang.reflect.AccessibleObject 1.2

- `void setAccessible(boolean flag)`  
  sets or clears the accessibility flag for this accessible object, or throws an `IllegalAccessException` if the access is denied.
- `boolean trySetAccessible()`⁹  
  sets the accessibility flag for this accessible object, or returns `false` if the access is denied.
- `boolean canAccess(Object obj)`⁹  
  checks if the caller can access `obj` through this field, method, or constructor object. Pass `null` for a static field or method, or for a constructor.
- `static void setAccessible(AccessibleObject[] array, boolean flag)`  
  is a convenience method to set the accessibility flag for an array of objects.

## java.lang.Class 1.1

- `Field getField(String name)`
- `Field[] getFields()`  
  gets the public field with the given name, or an array of all fields.
- `Field getDeclaredField(String name)`
- `Field[] getDeclaredFields()`  
  gets the field that is declared in this class with the given name, or an array of all fields.

## java.lang.reflect.Field 1.1

- `Object get(Object obj)`  
  gets the value of the field described by this Field object in the object obj.
- `void set(Object obj, Object newValue)`  
  sets the field described by this Field object in the object obj to a new value.

## 5.9.6 Using Reflection to Write Generic Array Code

The Array class in the java.lang.reflect package allows you to create arrays dynamically. This is used, for example, in the implementation of the copyOf method in the Arrays class. Recall how this method can be used to grow an array that has become full.

```java
var a = new Employee[100];
. . .
// array is full
a = Arrays.copyOf(a, 2 * a.length);
```

How can one write such a generic method? It helps that an `Employee[]` array can be converted to an `Object[]` array. That sounds promising. Here is a first attempt:

```java
public static Object[] badCopyOf(Object[] a, int newLength) // not useful
{
    var newArray = new Object[newLength];
    System.arraycopy(a, 0, newArray, 0, Math.min(a.length, newLength));
    return newArray;
}
```

However, there is a problem with actually using the resulting array. The type of array that this code returns is an array of *objects* (`Object[]`) because we created the array using the line of code

```java
new Object[newLength]
```

An array of objects *cannot* be cast to an array of employees (`Employee[]`). The virtual machine would generate a `ClassCastException` at runtime. The point is that, as mentioned earlier, a Java array remembers the type of its entries—that is, the element type used in the new expression that created it. It is legal to cast an `Employee[]` temporarily to an `Object[]` array and then cast it back, but an array that started its life as an `Object[]` array can never be cast into an `Employee[]` array. To write this kind of generic array code, we need to be able to make a new array of the *same* type as the original array. For this, we need the methods of the `Array` class in the `java.lang.reflect` package. The key is the static `newInstance` method of the `Array` class that constructs a new array. You must supply the type for the entries and the desired length as parameters to this method.

```java
Object newArray = Array.newInstance(componentType, newLength);
```

To actually carry this out, we need to get the length and the component type of the new array. We obtain the length by calling `Array.getLength(a)`. The static `getLength` method of the `Array` class returns the length of an array. To get the component type of the new array:

- 1. First, get the class object of `a`.
- 2. Confirm that it is indeed an array.
- 3. Use the `getComponentType` method of the `Class` class (which is defined only for class objects that represent arrays) to find the right type for the array.
- 4. Conversely, for any `Class` object representing a class `C`, the `arrayType` method yields the `Class` object representing `C[]`.

Why is `getLength` a method of `Array` but `getComponentType` a method of `Class`? I don’t know—the distribution of the reflection methods seems a bit ad hoc at times.

Here’s the code:

```java
public static Object goodCopyOf(Object a, int newLength)
{
    Class cl = a.getClass();
    if (!cl.isArray()) return null;
    Class componentType = cl.getComponentType();
    int length = Array.getLength(a);
    Object newArray = Array.newInstance(componentType, newLength);
    System.arraycopy(a, 0, newArray, 0, Math.min(length, newLength));
    return newArray;
}
```

Note that this `copyOf` method can be used to grow arrays of any type, not just arrays of objects.

```java
int[] a = { 1, 2, 3, 4, 5 };
a = (int[]) goodCopyOf(a, 10);
```

To make this possible, the parameter of `goodCopyOf` is declared to be of type `Object`, *not an array of objects* (`Object[]`). The integer array type `int[]` can be converted to an `Object`, but not to an array of objects!

[Listing 5.18](#) shows both methods in action. Note that the cast of the return value of `badCopyOf` will throw an exception.

### **Listing 5.18** arrays/CopyOfTest.java

```java
package arrays;

import java.lang.reflect.*;
import java.util.*;

/**
 * This program demonstrates the use of reflection for
 * manipulating arrays.
 * @version 1.2 2012-05-04
 * @author Cay Horstmann
 */
public class CopyOfTest
{
   public static void main(String[] args)
   {
      int[] a = { 1, 2, 3 };
      a = (int[]) goodCopyOf(a, 10);
      System.out.println(Arrays.toString(a));

      String[] b = { "Tom", "Dick", "Harry" };
      b = (String[]) goodCopyOf(b, 10);
      System.out.println(Arrays.toString(b));

      System.out.println("The following call will generate an exception.");
      b = (String[]) badCopyOf(b, 10);
   }

   /**
    * This method attempts to grow an array by allocating a new
```
