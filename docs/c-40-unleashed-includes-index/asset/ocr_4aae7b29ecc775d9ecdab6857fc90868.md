![](bbox=[0.067, 0.088, 0.651, 0.374])

**FIGURE 3.14**  IL disassembler for the *Main* method.

What you’re looking at now is the code as the runtime sees it to execute. Notice a few things here:

+   - Metadata is stored with the compiled method to indicate its characteristics: `.method` tells it’s a method, `private` controls visibility, `cil` reveals the use of IL code in the method code, and so on.
+   - The execution model of the CLR is based on an evaluation stack, as revealed by the `.maxstack` directive and naming of certain IL instructions (`pop` and `push`, not shown in our little example).
+   - Method calls obviously refer to the methods being called, but observe how there’s no trace left of the C# using-directive namespace import and how all names of methods are fully qualified.
+   - Our local variable “name” has lost its name because the execution engine needs to know only about the existence (and type) of local variables, not their names. (The fact that it shows up as `str` is due to .NET Reflector’s attempt to be smart.)

The attentive reader will have noticed a few strange things in the IL instructions for the *Main* method: Why are those `nop` (which stands for *no operation*) instructions required? The answer lies in the way we compiled our application, with optimizations turned off. This default mode causes the compiler to preserve the structure of the input code as much as possible to make debugging easier. In this particular case, the curly braces surrounding the *Main* method code body were emitted as `nop` instructions, which allows a breakpoint to be set on that line.