
Here’s an example of how to construct such an altered class file. We start with the program VerifierTest.java of Listing 10.3. This is a simple program that calls a method and displays the method’s result. The program can be run both as a console program and as an applet. The fun method itself just computes 1 + 2.

```
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

As an experiment, try to compile the following modification of this program:

```
static int fun()
{
    int m = 1;
    int n;
    m = 1;
    m = 2;
    int r = m + n;
    return r;
}
```

Here, n is not initialized, so it could have any random value. Of course, the compiler detects that problem and refuses to compile the program. To create a bad class file, we have to work a little harder. First, run the javap program to find out how the compiler translates the fun method. The command

```
javap -c verifier.VerifierTest
```

shows the bytecodes in the class file in mnemonic form.

```
Method int fun()
 0 iconst_1
 1 istore_0
 2 iconst_2
 3 istore_1
 4 iload_0
 5 iload_1
 6 iadd
 7 istore_2
 8 iload_2
 9 ireturn
```

Use a hex editor to change instruction 3 from istore 1 to istore 0. That is, local variable 0 (which is m) is initialized twice, and local variable 1 (which is n) is not initialized at all. We need to know the hexadecimal values for these instructions; these values are readily available from the Java Virtual Machine specification ([https://docs.oracle.com/javase/specs/jvms/se11/html/index.html](https://docs.oracle.com/javase/specs/jvms/se11/html/index.html)).

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

You can use any hex editor to carry out the modification. In Figure 10.4, you see the class file VerifierTest.class loaded into the Gnome hex editor, with the bytecodes of the fun method highlighted.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_566_0.png)

**Figure 10.4** Modifying bytecodes with a hex editor

Change 3C to 3B and save the class file. Then try running the VerifierTest program. You get an error message:

```
Exception in thread "main" java.lang.VerifyError: (class: VerifierTest, method: fun signature:
()I) Accessing value from uninitialized register 1
```

That is good—the virtual machine detected our modification.

Now run the program with the -noverify (or -Xverify:none) option:

```
java -noverify verifier.VerifierTest
```

The fun method returns a seemingly random value. This is actually 2 plus the value that happened to be stored in the variable n, which was never initialized. Here is a typical printout:

```
1 + 2 == 15102330
```

### Listing 10.3  verifier/VerifierTest.java

```
package verifier;

import java.awt.*;

/**
 * This application demonstrates the bytecode verifier of the virtual machine. If you use a
 * hex editor to modify the class file, then the virtual machine should detect the tampering.
 * @version 1.10 2018-05-05
 * @author Cay Horstmann
 */
public class VerifierTest
{
   public static void main(String[] args)
   {
      System.out.println("1 + 2 == " + fun());
   }

   /**
    * A function that computes 1 + 2.
    * @return 3, if the code has not been corrupted
    */
   public static int fun()
   {
      int m;
      int n;
      m = 1;
      n = 2;
      // use hex editor to change to "m = 2" in class file
      int r = m + n;
      return r;
   }
}
```

The security manager now checks if the exit request came from the browser or an individual applet. If the security manager agrees with the exit request, the checkExit method simply returns and normal processing continues. However, if the security manager doesn’t want to grant the request, the checkExit method throws a SecurityException.

The exit method continues only if no exception occurred. It then calls the *private native* exitInternal method that actually terminates the virtual machine. There is no other way to terminate the virtual machine, and since the exitInternal method is private, it cannot be called from any other class. Thus, any code that attempts to exit the virtual machine must go through the exit method and thus through the checkExit security check without triggering a security exception.

Clearly, the integrity of the security policy depends on careful coding. The providers of system services in the standard library must always consult the security manager before attempting any sensitive operation.

The security manager of the Java platform allows both programmers and system administrators fine-grained control over individual security permissions. We will describe these features in the following section. First, we’ll summarize the Java 2 platform security model. We’ll then show how you can control permissions with *policy files*. Finally, we’ll explain how you can define your own permission types.

## 10.2.2 Java Platform Security

JDK 1.0 had a very simple security model: Local classes had full permissions, and remote classes were confined to the *sandbox*. Just like a child that can only play in a sandbox, remote code was only allowed to paint on the screen and interact with the user. The applet security manager denied all access to local resources. JDK 1.1 implemented a slight modification: Remote code that was signed by a trusted entity was granted the same permissions as local classes. However, both versions of the JDK used an all-or-nothing approach. Programs either had full access or they had to play in the sandbox.

Starting with Java 1.2, the Java platform has a much more flexible mechanism. A *security policy* maps code sources to permission sets (see Figure 10.5).

A *code source* is specified by a *code base* and a set of *certificates*. The code base specifies the origin of the code. For example, the code base of some remote applet code is the HTTP URL from which the applet was loaded. The code base of code in a JAR file is the file’s URL. A certificate, if present, is an assurance by some party that the code has not been tampered with. We’ll cover certificates later in this chapter.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_570_0.png)

**Figure 10.5** A security policy

A *permission* is any property that is checked by a security manager. The Java platform supports a number of permission classes, each encapsulating the details of a particular permission. For example, the following instance of the *FilePermission* class states that it is OK to read and write any file in the /tmp directory:

```
var p = new FilePermission("/tmp/*", "read,write");
```

More importantly, the default implementation of the *Policy* class reads permissions from a *permission file*. Inside a permission file, the same read permission is expressed as

```
permission java.io.FilePermission "/tmp/*", "read,write";
```

We'll discuss permission files in the next section.

Figure 10.6 shows the hierarchy of the permission classes that were supplied with Java 1.2. Many more permission classes have been added in subsequent Java releases.

In the preceding section, you saw that the *SecurityManager* class has security check methods such as *checkExit*. These methods exist only for the convenience of the programmer and for backward compatibility. They all map to standard

The FileReader constructor calls the FileInputStream constructor, which calls the checkRead method of the security manager, which finally calls checkPermission with a FilePermission(name, "read") object. Table 10.1 shows the call stack.

**Table 10.1** Call Stack During Permission Checking

| Class | Method | Code Source | Permissions |
|---|---|---|---|
| SecurityManager | checkPermission | null | AllPermission |
| SecurityManager | checkRead | null | AllPermission |
| FileInputStream | Constructor | null | AllPermission |
| FileReader | Constructor | null | AllPermission |
| Servlet | init | Servlet code source | Tomcat web app permissions |

The FileInputStream and SecurityManager classes are *system classes* for which `CodeSource` is null and the permissions consist of an instance of the `AllPermission` class, which allows all operations. Clearly, their permissions alone can't determine the outcome of the check. As you can see, the `checkPermission` method must take into account the restricted permissions of the applet class. By checking the entire call stack, the security mechanism ensures that one class can never ask another class to carry out a sensitive operation on its behalf.

> **NOTE:** This brief discussion of permission checking explains the basic concepts. However, we omit a number of technical details here. With security, the devil lies in the details, and we encourage you to read the book by Li Gong for more information. For a more critical view of the Java platform's security model, see the book *Securing Java: Getting Down to Business with Mobile Code, Second Edition*, by Gary McGraw and Ed W. Felten (Wiley, 1999). You can find an online version of that book at www.securingjava.com.

**java.lang.SecurityManager** 1.0

- `void checkPermission(Permission p)` 1.2
  
  checks whether this security manager grants the given permission. The method throws a `SecurityException` if the permission is not granted.
