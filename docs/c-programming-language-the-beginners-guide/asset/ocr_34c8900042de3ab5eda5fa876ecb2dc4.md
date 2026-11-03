```
• printf("Value is %d\n",value); 12
13 return(0);
14 }
15
16 void minus10(int *v)
17 {
18 *v = *v - 10;
19 }
20
21
```

As you can see in line 3 of the code above, the minus 10 function is prototyped. It also takes in an argument: a pointer variable. The pointer variable is basically a memory address, so the function basically accepts a memory address as an argument. The variable value's memory location/address is then transferred to the function, which you can see at line 10. As usual, the ampersand symbol fetches that address.

Within the function, the value of the transferred variable is changed using the asterisk. Since the variable's values are straightaway scanned in memory, no returned value is required. Build and run this code.

As you can see, the function has a direct impact on the value of the variable. This is true even though the only thing that was transferred to the function was the memory address and there was no return value. Now look at the code below: