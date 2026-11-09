**ToString** method. This creates a new **String** object in the heap that contains the string that was in the **StringBuilder** at the time you called **ToString**. At this point, you can continue to manipulate the string inside the **StringBuilder**, and later you can call **ToString** again to convert it into another **String** object.

# ## Constructing a StringBuilder Object

Unlike with the **String** class, the CLR has no special information about the **StringBuilder** class. In addition, most languages (including C#) don't consider the **StringBuilder** class to be a primitive type. You construct a **StringBuilder** object as you would any other non-primitive type:

```
```
StringBuilder sb = new StringBuilder();
```
```

The **StringBuilder** type offers many constructors. The job of each constructor is to allocate and initialize the state maintained by each **StringBuilder** object:

+   - **Maximum capacity** An **Int32** value that specifies the maximum number of characters that can be placed in the string. The default is **Int32.MaxValue** (approximately 2 billion). It's unusual to change this value. However, you might specify a smaller maximum capacity to ensure that you never create a string over a certain length. Once constructed, a **StringBuilder**'s maximum capacity value can't be changed.

+   - **Capacity** An **Int32** value indicating the size of the character array being maintained by the **StringBuilder**. The default is 16. If you have some idea of how many characters you'll place in the **StringBuilder**, you should use this number to set the capacity when constructing the **StringBuilder** object.
+   
+     When appending characters to the character array, the **StringBuilder** detects if the array is trying to grow beyond the array's capacity. If it is, the **StringBuilder** automatically doubles the capacity field, allocates a new array (the size of the new capacity), and copies the characters from the original array into the new array. The original array will be garbage collected in the future. Dynamically growing the array hurts performance; avoid this by setting a good initial capacity.

+   - **Character array** An array of **Char** structures that maintains the set of characters in the "string." The number of characters is always less than or equal to the capacity and maximum capacity values. You can use the **StringBuilder**'s **Length** property to obtain the number of characters used in the array. The **Length** is always less than or equal to the **StringBuilder**'s capacity value. When constructing a **StringBuilder**, you can pass a **String** to initialize the character array. If you don't specify a string, the array initially contains no characters—that is, the **Length** property returns 0.