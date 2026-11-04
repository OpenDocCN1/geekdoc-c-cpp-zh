The last line, with the at IL keyword, is of interest. This number is an offset into a section of the generated assembly file (which gets stored in the standard executable format known as Portable Executable or PE), relative to the base for the executable image. If you're a real geek, read on; otherwise, just remember this: The compiler has turned our array initializer into a blob of binary data that's being loaded as a whole in a very efficient way.

If you want to dig deeper from this point on, you'll need a tool called dumpbin.exe, which gets installed with Visual Studio 2010 in the Visual C++ binaries folder. Your Visual Studio 2010 command prompt should have it on the search path by default. If you run dumpbin.exe /all, passing in the name of your assembly, you'll see a bunch of data flying over the screen. This is the binary dump of the assembly.

First you need to find the base address, which is found near the top in the Optional Header Values section. It's called “image base” and should have (assuming default settings) a value of 400000. Previously, we found an offset of 00002050 through the IL disassembly. This number can be different, so double-check it. Either way, add up the two numbers, and you've found the raw address where the array's initialization data lives (in my case, that's 402050).

If you scroll down farther in the dumpbin output, you'll find a section Raw Data #1. This is where you'll take a look next. Locate the address found previously in the left column (for example, 402050). At this point, you'll see the ten 4-byte values in hexadecimal.

![](bbox=[0.12, 0.65, 0.88, 0.76])

# Jagged Arrays

As you learned earlier, arrays have a type constructor nature, meaning any existing type can be used to create another array type (a recursive definition, that is). So what about arrays of arrays? Sure enough, that works:

```
int[][] vectors = new int[3][];
```

An array with elements that are arrays by themselves is called a jagged array.

In the preceding example, we're creating an array of integer arrays and specifying the number of such arrays we want. The vectors array contains arrays by itself, which are reference types. So right after the creation of the jagged array, it contains null references for the elements. Next, we can initialize those elements as follows:

```
vectors[0] = new int[4];
vectors[1] = new int[2];
vectors[2] = new int[3];
```

Notice how the dimensions of the jagged array's element arrays do not need to match; this is where the name jagged arrays comes from. Notice the jagged line on the right in Figure 4.34 where we illustrate this concept.