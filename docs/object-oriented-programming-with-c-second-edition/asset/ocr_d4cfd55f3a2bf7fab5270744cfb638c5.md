![](bbox=[0.245, 0.098, 0.833, 0.443])

**Figure 4.3** Assigning a string to an object of the class *String*

at the base of a different memory block of four bytes that has been exclusively allocated for the purpose. The contents of the memory block whose base address is passed to the constructor should be copied into the memory block which 's1.cStr' points.
In Figure 4.3, 'cPtr' points at the memory block containing the string. In other words, the value of 'cPtr' is the address of the memory block containing the string.
The third case

```
char cArr[10] = "abc";
String s1(cArr);
```

is similar to the above. In this, we are passing the name of the array as a parameter to the constructor. But we know that an array is itself a fixed pointer that contains the base address of the memory block containing the actual contents of the array. We can now define the constructor that produces these effects. We must realize that 'p' (the formal argument of the constructor) should be as follows:

```
const char * const
```

First, it should be a constant pointer because throughout the execution of the constructor, it should continue to point at the same memory block. Second, it should be a pointer to a constant because even inadvertently, the library programmer should not dereference it to change the contents of the memory block at which it is pointing. Additionally, we would like to specify a default value for 'p' (NULL) so that there is no need to separately define a zero-argument constructor.
The definition of the class *String* with the prototype of the constructor and its definition are shown in Listing 4.8.