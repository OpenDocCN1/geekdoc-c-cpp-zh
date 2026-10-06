```
printf("The value of ptr_to_a is %d\n", ptr_to_a);
```

In this line, we're printing the value of ptr_to_a, not the value it's pointing at, but the value of the pointer itself. This prints a very large number, as it's the address in memory where a can be found.

```
printf("It stores the value %d\n", *ptr_to_a);
```

In this line, we're printing the value pointed to by ptr_to_a, note the asterisk before the name. This prints the value of a.

```
printf("The address of a is %d\n", &a);
```

In this line, we're printing the address of a itself note the & sign before the name Again, this prints a very large number, the same as the value of ptr_to_a we printed above

| When I was first learning pointers, I found it helpful to say out what a line of code was doing - an * is "what is pointed to" and an & is the "address of..."... |
| those two ideas fixed in your head, you've pretty much understand pointers |

The crucial thing to remember when working with pointers is this: you can't just declare a pointer, you also need to declare and associate the variable you want to point to. When a pointer is created, it points at a random location in memory; if you try to write something to it, you can cause all sorts of errors up and including crashing the computer completely! Always make sure your pointers are pointing at something before doing anything with them

Pointers are one of the ways C allows you in some cases (forced) to think about what the actual hardware of your computer is - a good understanding of pointers gives you a good understanding of how the compiler handles memory.