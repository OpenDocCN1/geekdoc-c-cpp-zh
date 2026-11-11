Use a hex editor to change instruction 3 from istore 1 to istore 0. That is, local variable 0 (which is n) is initialized twice, and local variable 1 (which is m) is not initialized at all. We need to know the hexadecimal values for these instructions; these values are readily available from the Java Virtual Machine specification ([https://docs.oracle.com/javase/specs/jvms/se11/html/index.html](https://docs.oracle.com/javase/specs/jvms/se11/html/index.html)).

```
```
0 iconst_1 04
1 istore_0 3B
2 iconst_2 05
3 istore_1 3C
4 iload_0 1A
5 iload_1 1B
6 iadd 60
7 istore_2 3D
8 iload_2 1C
9 ireturn AC
```
```

You can use any hex editor to carry out the modification. In Figure 10.4, you see the class file VerifierTest.class loaded into the Gnome hex editor, with the bytecodes of the fun method highlighted.

![](bbox=[0.29, 0.49, 0.84, 0.82])

Figure 10.4 Modifying bytecodes with a hex editor

Change 3C to 3B and save the class file. Then try running the VerifierTest program. You get an error message: