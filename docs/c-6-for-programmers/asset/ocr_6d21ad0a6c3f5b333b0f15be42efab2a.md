x squared: 100

**Fig. 7.9 |** Square method used to demonstrate the method-call stack and activation records. (Part 2 of 2.)

First, the operating system calls Main—this pushes an activation record onto the stack (Fig. 7.10). This tells Main how to return to the operating system (i.e., transfer to return address R1) and contains the space for Main’s local variable x, which is initialized to 10.

# Step 1: Operating system calls Main to begin program execution

```
```csharp
static void Main()
{
    int x = 10;
    Console.WriteLine("x squared: {Square(x)}");
}
```
```

![](bbox=[0.2, 0.43, 0.85, 0.74])

**Fig. 7.10 |** Method-call stack after the operating system calls main to execute the program.

Method Main—before returning to the operating system—calls method Square in line 11 of Fig. 7.9. This causes a stack frame for Square (lines 15–18) to be pushed onto the method-call stack (Fig. 7.11). This stack frame contains the return address that Square needs to return to Main (i.e., R2) and the memory for Square’s local variable y.

After Square performs its calculation, it needs to return to Main—and no longer needs the memory for y. So Square’s stack frame is popped from the stack—giving Square the return location in Main (i.e., R2) and losing Square’s local variable (Step 3). Figure 7.12 shows the method-call stack after Square’s activation record has been popped.

Method Main now displays the result of calling Square (Fig. 7.9, line 11). Reaching the closing right brace of Main causes its stack frame to be popped from the stack, giving Main the address it needs to return to the operating system (i.e., R1 in Fig. 7.10)—at this point, Main’s local variable x no longer exists. You’ve now seen how valuable the stack data structure is in implementing a key mechanism that supports program execution. There’s a significant omission in the sequence of illustrations in this section. See if you can spot it before reading the next sentence. The call to the method Console.WriteIn, of course, also involves the stack, which should be reflected in this section’s illustrations and discussion.