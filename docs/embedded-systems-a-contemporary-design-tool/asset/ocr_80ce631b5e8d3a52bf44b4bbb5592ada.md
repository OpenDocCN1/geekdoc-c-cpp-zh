held by the stack pointer to refer to the next lower address (the new top of the stack). The retrieved value is returned as the result of the pop operation.

# 1.9.3.5 PROCESS

Let's now return to the function call. From a high-level point of view, code execution proceeds in a sequential manner until the function call is encountered. Flow of control switches to the function, the code comprising the function body is executed, and flow returns to the original context, as seen in Figure 1.41.

```
3000 Code
3053 CALL F1(3)
3054 pop R2
3055 More Code
....
5000 code // Function Body....
5053 Return

Figure 1.41 Function Call Construct
```

Let's now examine the process in somewhat greater detail. In the code fragment shiwn in Figure 1.42, the program is initially loaded into memory and begins executing from address 3000. Code is executed until the flow reaches address 3053, at which point the function call is encountered. At this point, the sequence of operations shown in Figure 1.42 will occur.

+   1. The return address and parameters are pushed onto the stack.
+      The address saved is 3054.
+      The parameter saved is 3.
+   2. Address of function body 5000 is put into PC.
+   3. Instruction at 5000 begins executing.
+   4. Execution continues until 5053.
+   5. Return encountered
+      Stack gets
+      Return values
+      Stack loses
+      Return address
+   6. Return address is put into PC.
+   7. Flow returns to address 3054, and the top of stack is popped and put into register R2.
+   8. Execution continues at 3055.
+   
+   Figure 1.42 Function Call Flow of Control

Had an additional function call been encountered in function F1, an identical process would have occurred. The process can be repeated multiple times; however, we must be aware that stack can overflow. If too much is pushed onto the stack, we begin to lose information, particularly the return address.