The result? Garbage. To understand why this is the case, you should know about memory management in the operating system, which does not guarantee zeroing out acquired pieces of memory. In this case, the variable that's allocated on the stack contains some random data in it, and results can and will vary.

You'll wonder whether it would be better to have memory zeroed out to begin with. That certainly has its merits, eliminating the nondeterministic behavior that results from random data. And in fact, the common language runtime guarantees that memory is zeroed out before it's exposed to code: Allocating a new object (using `newobj`) makes sure the allocated memory consists of all-zero data and similar local variable slots are initialized with zero data. To illustrate this, we can really go hardcore by writing—for this one time, I promise—plain IL code in some text file:

```
```
.assembly extern mscorlib {}
.assembly Zero {}

.class Zero
{
    .method static void Main()
    {
        .entrypoint
        .locals init (int32 x)
        ldloc.0
        call       void [mscorlib]System.Console::WriteLine(int32)
        ret
    }
}
```
```

Feels a bit like C#, doesn’t it? Believe me, IL isn’t hard at all. Either way, the preceding code defines an assembly called `Zero` with a `Main` entry-point method that has one 32-bit integer local variable called `x`. The code itself simply loads the local variable (`ldloc.0`) and then calls the `Console.WriteLine` method on it. Don’t worry about `mscorlib`; this simply indicates the assembly in which the `System.Console` class is defined. For the same reason, the very first line adds a reference to the `mscorlib` external assembly, so the runtime knows it should be prepared to load that one when required by the code.

Save this code in a file with an `.il` extension and call `ILASM` (for IL assembler, the opposite of the disassembler) on it to produce an assembly. You’ll see the assembler doesn’t complain about uninitialized data because the common language runtime guarantees it will be initialized to zero as proven in Figure 5.27.

Notice the executable simply prints `0` because the local variable slot on the stack was allocated with zero memory. Reason for euphoria? Maybe, maybe not.