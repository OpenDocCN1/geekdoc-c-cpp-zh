# Program 9.9　Using indexes and pointers with an array (Continued)

```
```cpp
17    }
18    cout << endl;
19    // Accessing elements through the pointers
20    cout << "Accessing elements through pointers" << endl;
21    for (int i = 0; i < 5; i++)
22    {
23        cout << *(numbers + i) << " ";
24    }
25    return 0;
26    }

Run:
Accessing elements through indexes
10  11  12  13  14
Accessing elements through pointers
10  11  12  13  14
```
```

# Pointer Arithmetic

Pointer types are not integer types. However, pointer arithmetic allows a limited number of arithmetic operators to be applied to pointer types. We must look at these operators with a new definition in mind. When we use these operators, we must remember that because the result is another pointer value, that value must point to a memory location in our control; otherwise, the result is nonsense. This is why using these operators makes sense when we apply them to pointers to the elements of the array: When we declare an array, the memory locations involved are in our control.

**Integer Addition or Subtraction**  We can use the addition operator to add an integer to, or the subtraction operator to subtract an integer from, a pointer:

| Addition | Subtraction |
|---|---|
| `ptr1 = ptr + n` | `ptr2 = ptr - n` |

Using the addition and subtraction operators this way creates a new definition for them. It creates a new pointer *n × m* bytes forward or backward; *m* is the size of the pointed variable, where *m* is the number of bytes occupied by each element. So the operation moves the pointer *n* elements forward or backward as shown in Figure 9.16. Addition creates a pointer

![](bbox=[0.254, 0.752, 0.826, 0.906])

**Figure 9.16**　Integer addition and subtraction of pointers