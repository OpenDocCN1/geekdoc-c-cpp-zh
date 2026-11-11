in the class files is well documented, and it is an easy matter for someone with experience in assembly programming and a hex editor to manually produce a class file containing valid but unsafe instructions for the Java virtual machine. The verifier is always guarding against maliciously altered class files, not just checking the class files produced by a compiler.

Here’s an example of how to construct such an altered class file. We start with the program `VerifierTest.java` of Listing 9.3. This is a simple program that calls a method and displays the method’s result. The program can be run both as a console program and as an applet. The fun method itself just computes 1 + 2.

```
```java
static int fun()
{
    int m;
    int n;
    m = 1;
    n = 2;
    int r = m + n;
    return r;
}
```
```

As an experiment, try to compile the following modification of this program:

```
```java
static int fun()
{
    int m = 1;
    int n;
    m = 1;
    n = 2;
    int r = m + n;
    return r;
}
```
```

In this case, n is not initialized, and it could have any random value. Of course, the compiler detects that problem and refuses to compile the program. To create a bad class file, we have to work a little harder. First, run the javap program to find out how the compiler translates the fun method. The command

```
```shell
javap -c verifier.VerifierTest
```
```

shows the bytecodes in the class file in mnemonic form.

```
```text
Method int fun()
  0 iconst_1
  1 istore_0
  2 iconst_2
  3 istore_1
  4 iload_0
  5 iload_1
  6 iadd
```
```