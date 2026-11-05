```
for (int i = 0; i < 2; ++i)
  for (int j = 0; j < 3; ++j) {
    for (int k = 0; k < 4; ++k) {
      Console.Write("[ {0},{1},{2}] = {3,2} ", i, j, k,
        a[i,j,k]);
      Console.WriteLine();
    }
  }
}
```

which produces the output:

[0,0,0] = 1 [0,0,1] = 2 [0,0,2] = 3
[0,1,0] = 4 [0,1,1] = 5 [0,1,2] = 6 [0,1,3] = 7
[0,2,0] = 8 [0,2,1] = 9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23

end example]

[Example: In the following code

```
class Test
{
  unsafe static void Fill(int* p, int count, int value) {
    for (; count != 0; count--) *p++ = value;
  }
  static void Main() {
    int[] a = new int[100];
    unsafe {
      fixed (int* p = a) Fill(p, 100, -1);
    }
  }
}
```

a fixed statement is used to fix an array so its address can be passed to a method that takes a pointer.

end example]

A char* value produced by fixing a string instance always points to a null-terminated string. Within a fixed statement that obtains a pointer p to a string instance s, the pointer values ranging from p to p + s.Length - 1 represent addresses of the characters in the string, and the pointer value p + s.Length always points to a null character (the character with value '\0').

Modifying objects of managed type through fixed pointers can result in undefined behavior. [Note: For example, because strings are immutable, it is the programmer's responsibility to ensure that the characters referenced by a pointer to a fixed string are not modified. end note]

[Note: The automatic null-termination of strings is particularly convenient when calling external APIs that expect "C-style" strings. Note, however, that a string instance is permitted to contain null characters. If such null characters are present, the string will appear truncated when treated as a null-terminated char*. end note]

# 23.8 Fixed-size buffers

# 23.8.1 General

Fixed-size buffers are used to declare "C-style" in-line arrays as members of structs, and are primarily useful for interfacing with unmanaged APIs.

# 23.8.2 Fixed-size buffer declarations

A fixed-size buffer is a member that represents storage for a fixed-length buffer of variables of a given type. A fixed-size buffer declaration introduces one or more fixed-size buffers of a given element type. Fixed-size buffers are only permitted in struct declarations and may only occur in unsafe contexts (§23.2).