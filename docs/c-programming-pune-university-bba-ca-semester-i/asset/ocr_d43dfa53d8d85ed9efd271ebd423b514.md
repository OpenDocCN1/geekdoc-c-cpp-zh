```
```c
printf("Content of pointer pc:%d\n\n",*pc);
c=11;
printf("Address of pointer pc:%u\n",pc);
printf("Content of pointer pc:%d\n\n",*pc);
*pc=2;
printf("Address of c:%u\n",&c);
printf("Value of c:%d\n\n",c);
return 0;
}
```
```

**Output:**
Address of c: 2686784
Value of c: 22
Address of pointer pc: 2686784
Content of pointer pc: 22
Address of pointer pc: 2686784
Content of pointer pc: 11
Address of c: 2686784
Value of c: 2

![](bbox=[0.16, 0.525, 0.83, 0.625])

# ### Explanation of Program and Figure

+   1. **int&#42; pc;** creates a pointer **pc** and **int c;** creates a normal variable **c**.
+      Since **pc** and **c** are both not initialized, pointer **pc** points to either no address or a random address. Likewise, variable **c** is assigned an address but contains a random/garbage value.
+   2. **c=22;** assigns 22 to the variable **c**, i.e., 22 is stored in the memory location of variable **c**.
+      Note that, when printing **&c** (address of c), we use **%u** rather than **%d** since address is usually expressed as an unsigned integer (always positive).
+   3. **pc=&c;** assigns the address of variable **c** to the pointer **pc**.
+      When printing, you see value of **pc** is the same as the address of **c** and the content of **pc** (&#42;pc) is 22 as well.
+   4. **c=11;** assigns 11 to variable **c**.
+      We assign a new value to **c** to see its effect on pointer **pc**.
+   5. Since, pointer **pc** points to the same address as **c**, value pointed by pointer **pc** is 11 as well.
+      Printing the address and content of **pc** shows the updated content as 11.
+   6. **&#42;pc=2;** changes the contents of the memory location pointed by pointer **pc** to 2.
+      Since the address of pointer **pc** is same as address of **c**, value of **c** also changes to 2.