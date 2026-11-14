The results of the three calculations not only yield three different answers, but, depending on which formula is used, have substantially different error magnitudes as well.

These simple examples illustrate rather graphically that when one is performing mathematical computations, it is important to understand where errors can arise, how they can propagate under mathematical operations, and how such phenomena can affect any calculations. Such errors can have serious consequences for the safety of any applications if we are not careful.

# 1.6 ADDRESSES

In the earlier functional diagram as well as in the block diagram for a microprocessor, we learned that information is stored in memory. Each location in memory has an associated address much like an index in an array. If an array has 16 locations to hold information, it will have 16 indices. If a memory has 16 locations to store information, it will have 16 addresses. Information is accessed in memory by giving its address. As we begin with encoded characters, each address has a unique binary pattern. Addresses begin at binary 0 and range to the maximum value the word size will permit.

For a word size of 32 bits, the addresses will range (in hex) from 00000000 to FFFFFFFF. Thus, with 32 bits, we have up to 4294967296 unique combinations and, therefore, that same number of possible addresses. Of course, you may not use them all, but they are there. Figure 1.12 illustrates how a word might look if the bits are interpreted as expressing an address. In fact, an address does not look any different from an unsigned integer, which, in reality, it is. It is important that it is not a signed integer. The microprocessor does not support negative addresses.

The following C or C++ declarations place the integer value 10 in binary into some location in memory. Let’s say at address 3000.

```
int myVar = 10;
int* myVarPtr = &myVar; // take the address of myVar
// assign it to the pointer variable myVarPtr
```

When interpreted by the system, the code fragment directs the system to set aside another memory word to hold the address of the signed integer, *myVar* (let’s say at address 5000) and puts 3000 into that address. The *value* at address 5000 points to address 3000. The accompanying diagram in Figure 1.13 illustrates such an arrangement.

![](bbox=[0.13, 0.69, 0.38, 0.88])

![](bbox=[0.48, 0.69, 0.75, 0.88])