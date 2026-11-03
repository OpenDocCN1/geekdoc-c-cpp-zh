```
```c
• printf("The address of ‘pokey’ is %p\n",p);

  • printf("The contents of ‘pokey’ are %d\n",*p); 16
17 return(0);
18 }
19
20
```
```

Two sets of *printf* statements display the address and value of the variable. The first set uses ‘pokey’ directly. The second set uses pointer variable. In line 14, *p* is used without the asterisk, so it is a memory location. In line 15, *p* is used with the asterisk, so it peeks at the contents of that memory location. Build and run this code.

As you can see, the pointer variable *p* dutifully reports the correct values: the address and the contents. A logical question to ask at this point is, “Why bother?” At this level, using a pointer is pretty “pointless.” You can do many things in C without bothering with pointers, but they do have their purpose. Many functions expect you to understand and know how pointers work.