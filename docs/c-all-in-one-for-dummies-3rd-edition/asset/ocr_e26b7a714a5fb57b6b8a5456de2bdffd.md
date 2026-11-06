# Tracing through assembly code

If you feel the urge, you can view the actual assembly code. The only time we ever do this is when we absolutely must get down to the hardcore nitty-gritty. Code::Blocks lets you do this. Choose Debug»Debugging Windows»Disassembly to see the Disassembly window. We strongly suggest checking the Mixed Mode option so that you can see a mix of C++ and assembly code, as shown in Figure 4-2. This approach makes it a lot easier to understand how Code::Blocks turns your C++ code into assembly language. Notice that the top of the window tells you the name of the function you’re viewing and which file contains the function, and the C++ code includes line numbers so that you know precisely where you are in the source code.

![](bbox=[0.23, 0.357, 0.684, 0.665])

**Figure 4-2:** The Disassembly window shows the assembly code that results from the C++ code you write.

![](bbox=[0.134, 0.7, 0.207, 0.775])

Some readers have noted that Code::Blocks will sometimes freeze when displaying the Disassembly window. The IDE will report that the disassembly is being loaded, but the process never completes. In this case, close the sample code and restart the IDE. In most cases, the disassembly will load on the second try.

The window shown in Figure 4-2 is the disassembly of the SeatsPerCar() function, shown in Listing 4-1. Here’s the function again so that you can compare it to Figure 4-2:

```
int SeatsPerCar()
{
    return 4;
}
```