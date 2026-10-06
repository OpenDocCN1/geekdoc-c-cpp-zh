```
abc123 = pointer to object      offset
mov eax, [abc123]      eax = ea        offset = abc123+0*word_size
      abc123
mov ebx, [abc123+4]   ebx = ebx       offset = abc123+2*word_size
      abc123+4
mov ecx, [abc123+8]   ecx = ec        offset = abc123+4*word_size
      abc123+8
```

**Figure 3:** This shows how to offset a pointer to retrieve the address of variable 'a' into eax. The second line places the address of variable 'b' into ebx. And the last line places the variable 'c' into ecx.

# 20.2.2 Methods

At a low level, there is almost no difference between a function and a method. When decompiling, it sometimes seems hard to tell a difference between the two. They reside in the text memory space, and both are called the same. An example of how a method is called can be seen in **Figure 4.

A:

```
//method call
abc123->foo(1, 2, 3);
```

B:

```
push 3               ; int c
push 2               ; int b
push 1               ; int a
push [ebp-4]        ; the address of the object
call 0x00434125      ; call to method
```

**Figure 4:** A method call in the C++ syntax. abc123 is a pointer to an object that has a method, foo(). foo() is taking three integer arguments, 1, 2, and 3.

**Figure 4.B** The same method call in x86 assembly. It takes four arguments, the address of the object and three integers. The pointer to the object is at ebp-4 and 00434125.

A notable characteristic of a method call is that the address of the object being passed in as an argument. This, however, is not always a good indicator. **Figure 5** shows function with the first argument being an object passed by reference. The result is function that looks identical to a method call.

A:

```
//function call
foo(abc123, 1, 2, 3);
```

B:

```
push 3               ; int c
push 2               ; int b
```