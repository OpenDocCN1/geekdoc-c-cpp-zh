+   9. **Click Next Line one more time and the highlight is on the closing brace of `main()`.**

Now things get just a little strange. Unknownst to us, there’s really more code than we see. When you compile and link your application, the linker includes some special start-up code that calls your `main()` function.

+   10. **Click Next Line one more time and you are time-warped out of your source file and into some assembly language code. The Debugger window shows the following message:**

```
`In __mingw_CRTStartup () {`
```

+   11. **Click a new button, Next Instruction (six buttons from the left on the Debugger toolbar), to advance to the next instruction. The Debugger window shows the following message again:**

```
`In __mingw_CRTStartup () {`
```

+   12. **To see what this all means, click Debugging Windows (ten buttons from the left on the Debugger toolbar) and choose Disassembly from the drop-down list box.**

Code::Blocks displays a new window called Disassembly, as shown in Figure 2-2. The numbers in your figure may differ from ours, but the code is the same.

![](bbox=[0.253, 0.548, 0.729, 0.893])

**Figure 2-2:** The Disassembly displays the assembly language version of your code.