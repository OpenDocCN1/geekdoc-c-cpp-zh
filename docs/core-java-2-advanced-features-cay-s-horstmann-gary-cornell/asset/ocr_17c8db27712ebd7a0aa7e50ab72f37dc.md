```
```text
7 istore_2
8 iload_2
9 ireturn
```
```

Use a hex editor to change instruction 3 from `istore_1` to `istore_0`. That is, local variable 0 (which is m) is initialized twice, and local variable 1 (which is n) is not initialized at all. We need to know the hexadecimal values for these instructions; these values are readily available from *The Java™ Virtual Machine Specification, Second Edition*, by Tim Lindholm and Frank Yellin (Prentice Hall, 1999).

```
```text
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

You can use any hex editor to carry out the modification. In Figure 9.4, you see the class file `VerifierTest.class` loaded into the Gnome hex editor, with the bytecodes of the fun method highlighted.

Change 3C to 3B and save the class file. Then try running the `VerifierTest` program. You get an error message:

```
```text
Exception in thread "main" java.lang.VerifyError: (class: VerifierTest, method: fun signature:
()I) Accessing value from uninitialized register 1
```
```

That is good—the virtual machine detected our modification.

Now run the program with the `-noverify` (or `-Xverify:none`) option.

```
```text
java -noverify verifier.VerifierTest
```
```

The fun method returns a seemingly random value. This is actually 2 plus the value that happened to be stored in the variable n, which never was initialized. Here is a typical printout:

```
```text
1 + 2 == 15102330
```
```

To see how browsers handle verification, we wrote this program to run either as an application or an applet. Load the applet into a browser, using a file URL such as

```
```text
file:///C:/CoreJavaBook/v2ch9/verifier/VerifierTest.html
```
```

You then see an error message displayed indicating that verification has failed (Figure 9.5).