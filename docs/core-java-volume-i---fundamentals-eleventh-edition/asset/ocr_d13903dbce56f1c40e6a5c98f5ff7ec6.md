must supply the type for the entries and the desired length as parameters to this method.

```
    Object newArray = Array.newInstance(componentType, newLength);
```

To actually carry this out, we need to get the length and the component type of the new array.

We obtain the length by calling Array.getLength(a). The static getLength method of the Array class returns the length of an array. To get the component type of the new array:

+   1. First, get the class object of a.
+   2. Confirm that it is indeed an array.
+   3. Use the getComponentType method of the Class class (which is defined only for class objects that represent arrays) to find the right type for the array.

Why is getLength a method of Array but getComponentType a method of Class? We don't know—the distribution of the reflection methods seems a bit ad hoc at times.

Here's the code:

```
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

Note that this copyOf method can be used to grow arrays of any type, not just arrays of objects.

```
    int[] a = { 1, 2, 3, 4, 5 };
    a = (int[]) goodCopyOf(a, 10);
```

To make this possible, the parameter of *goodCopyOf* is declared to be of type *Object*, not an array of objects (*Object[]*). The integer array type *int[]* can be converted to an *Object*, but not to an array of objects!

Listing 5.17 shows both methods in action. Note that the cast of the return value of *badCopyOf* will throw an exception.