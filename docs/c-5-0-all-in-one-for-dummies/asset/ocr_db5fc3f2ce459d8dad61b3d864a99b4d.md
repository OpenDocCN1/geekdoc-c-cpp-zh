I define "public enough" as having a strong enough access specifier from the viewpoint of Class1, the caller. This issue involves access control, extended earlier in this chapter and covered in the discussion of access specifiers in Chapter 5 of this minibook.

# *Determining whether the class and method you need are visible and accessible to you*

To determine whether Class1 in NamespaceA can call NamespaceB.Class2.AMethod(), consider these two questions:

+   - **Is Class2 over in NamespaceB visible to the calling class, Class1?**
+     This issue involves namespace visibility, discussed at the end of this list.
+   - **If the answer to the first question is True, are Class2 and its AMethod() also "public enough" for Class1 to access?**

If Class2 is in a different assembly from Class1, it must be public for Class1 to access its members. Class2, in the same assembly needs to be declared at least internal. Classes can only be public, protected, internal, or private.

Likewise, the Class2 method must have at least a certain level of access in each of those situations. Methods add the protected internal option to the list of access specifiers that classes have. Chapter 5 in this minibook and the earlier section "Going Beyond Public and Private: More Access Keywords" supply the gory details.

You need to answer Yes to both questions before Class1 can call the Class2 method.

# *Making classes and methods in another namespace visible*

C# provides two ways to make items in NamespaceB visible in NamespaceA:

+   - **Fully qualify names from NamespaceB wherever you use them in NamespaceA.** This method results in code such as the following line, which starts with the namespace name and then adds the class and lists the method:
+     ```
+     System.Console.WriteLine("my string");
+     ```
+   - **Eliminate the need for fully qualified names in NamespaceA by giving your files a using directive for NamespaceB:**
+     ```
+     using System;  // These are namespace names.
+     using NamespaceB;
+     ```

Programs throughout this book make items in NamespaceB visible in NamespaceA with the using directive. I discuss full qualification and using directives in the next two sections.