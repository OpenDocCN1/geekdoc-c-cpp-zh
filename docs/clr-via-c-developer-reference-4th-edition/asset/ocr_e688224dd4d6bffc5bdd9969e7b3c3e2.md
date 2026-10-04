to the referenced types. In Figure 1-4, the Main method refers to a single type, Console, causing the CLR to allocate a single internal structure. This internal data structure contains an entry for each method defined by the Console type. Each entry holds the address where the method's implementation can be found. When initializing this structure, the CLR sets each entry to an internal, undocumented function contained inside the CLR itself. I call this function JITCompiler.

When Main makes its first call to WriteLine, the JITCompiler function is called. The JITCompiler is responsible for compiling a method's IL into native CPU instructions. Because the IL is being compiled "just in time," this component of the CLR is frequently referred to as a JITter or a JIT compiler.

> Note If the application is running on an x86 version of Windows or in WoW64, the JIT compiler produces x86 instructions. If your application is running as a 64-bit application on an x64 version of Windows, the JIT compiler produces x64 instructions. If the application is running on an ARM version of Windows, the JIT compiler produces ARM instructions.

![](bbox=[0.058, 0.245, 0.102, 0.365])

| Managed EXE | |
| :--- | :--- |
| static void Main() { Console.WriteLine("Hello"); Console.WriteLine("Goodbye"); } | static void WriteLine() JITCompiler |
| static void WriteLine(string) JITCompiler | Native CPU instructions |
| (remaining members) | ...

FIGURE **1-4** Calling a method for the first time.

**12** PART I CLR Basics *\*\*\*

```
JITCompiler function {
1. In the assembly that implements the type (Console), look up the method (WriteLine) being called in the metadata.
2. From the metadata, the IL for this method.
3. Allocate a block of memory.
4. Compile the IL into native CPU instructions; the native code is saved in the memory allocated in step 3.
5. Modify the method's entry in the Table's so that it now points to the memory block allocated in step 3.
6. Jump to the native code contained inside the memory block.
}
```