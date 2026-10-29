# Pointer Arithmetic

![](bbox=[0.161, 0.122, 0.906, 0.309])

**Figure 8.17**  The nums array in memory

After nPt contains a valid address, values can be added and subtracted from the address to produce new addresses. When adding or subtracting numbers to pointers, the computer adjusts the number automatically to ensure that the result still “points to” a value of the correct type. For example, the statement `nPt = nPt + 4;` forces the computer to scale the 4 by the correct number to make sure the resulting address is the address of an integer. Assuming each integer requires 4 bytes of storage, as shown in Figure 8.17, the computer multiplies the 4 by 4 and adds 16 to the address in nPt. The resulting address is 18950, which is the correct address of `nums[4]`.

The computer’s automatic scaling ensures that the expression `nPt + i`, where i is any positive integer, points to the ith element beyond the one currently pointed to by nPt. Therefore, if nPt initially contains the address of `nums[0]`, `nPt + 4` is the address of `nums[4]`, `nPt + 50` is the address of `nums[50]`, and `nPt + i` is the address of `nums[i]`. Although actual addresses are used in Figure 8.17 to illustrate the scaling process, programmers don’t need to be concerned with the actual addresses the computer uses. Manipulating addresses with pointers generally doesn’t require knowledge of the actual addresses.

Addresses can also be incremented or decremented with the prefix and postfix increment and decrement operators. Adding 1 to a pointer causes the pointer to point to the next element of the type being pointed to. Decrementing a pointer causes the pointer to point to the previous element. For example, if the pointer variable p is a pointer to an integer, the expression `p++` increments the address in the pointer to point to the next integer, as shown in Figure 8.18.

![](bbox=[0.318, 0.716, 0.752, 0.87])

**Figure 8.18**  Increments are scaled when used with pointers