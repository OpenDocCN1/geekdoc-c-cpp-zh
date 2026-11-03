# Exercise 18-9: Type the source code from Listing 18-6 into your editor. Build and run.

Here's the output I see on my screen:

```
About variable 'lead':
Size              1
Contents          A
Location          0x7fff5bff8ff
About variable 'sidekick':
Contents          0x7fff5bff8ff
```

The addresses (in the example) are unique for each system, but the key thing to note is that the contents of pointer sidekick are equal to the memory location of variable lead. That's because of the initialization that takes place on Line 9 in the code:

```
sidekick = &lead;
```

It would be pointless for a pointer to merely contain a memory address. The pointer can also peek into its address and determine the value that's stored there. To make that happen, the * operator is prefixed to the pointer's variable name.

# Exercise 18-10: Modify your source code from Exercise 18-9 by adding the following statement after Line 16:

```
printf("Peek value\t% c\n",*sidekick);
```

Build and run. Here's the output I see as output:

```
About variable 'lead':
Size              1
Contents          A
Location          0x7fff5bff8ff
And variable 'sidekick':
Contents          0x7fff5bff8ff
Peek value        A
```

When you specify the * (asterisk) before an initialized pointer variable's name, the results are the contents of the address. The value is interpreted based on the type of pointer. In this example, *sidekick represents the char value stored at a memory location kept in the sidekick variable, which is really the same as the memory location variable lead.