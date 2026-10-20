the values 4 and 5 on the I/O stack, forward execution of the stored procedure would yield the correct result of 10 and an undo stack, as depicted in Figure 8-2. Based on this undo stack, if the user tried to undo, rather than undoing the triangle area stored procedure, the user would undo only the top operation on the stack, the final multiply. The I/O stack would read

4
5
0.5

(and the undo stack would have a * between the 5and 0.5) instead of
4
5
* 0.5
* 5
4
Figure 8-2. The undo stack without a StoredProcedure class

To fully undo a stored procedure, the user needs to press undo n times, where n is equal