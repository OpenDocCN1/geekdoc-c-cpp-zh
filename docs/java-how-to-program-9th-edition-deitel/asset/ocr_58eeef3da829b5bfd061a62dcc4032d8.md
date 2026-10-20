scope of a declaration is the portion of the program that can refer to the declared entity by its name. Such an entity is said to be “in scope” for that portion of the program. This section introduces several important scope issues.

The basic scope rules are as follows:

+   1. The scope of a parameter declaration is the body of the method in which the declaration appears.
+   2. The scope of a local-variable declaration is from the point at which the declaration appears to the end of that block.
+   3. The scope of a local-variable declaration that appears in the initialization section of a for statement’s header is the body of the for statement and the other expressions in the header.
+   4. A method or field’s scope is the entire body of the class. This enables non-static methods of a class to use the fields and other methods of the class.

Any block may contain variable declarations. If a local variable or parameter in a method has the same name as a field of the class, the field is “hidden” until the block terminates execution—this is called shadowing. In Chapter 8, we discuss how to access shadowed fields.

# Error-Prevention Tip 6.3

Use different names for fields and local variables to help prevent subtle logic errors that occur when a method is called and a local variable of the method shadows a field in the class.

Figure 6.9 demonstrates scoping issues with fields and local variables. Line 7 declares and initializes the field x to 1. This field is shadowed (hidden) in any block (or method) that declares a local variable named x. Method main (lines 11–23) declares a local variable x (line 13) and initializes it to 5. This local variable’s value is output to show that the field x (whose value is 1) is shadowed in main. The program declares two other methods—useLocalVariable (lines 26–35) and useField (lines 38–45)—that each take no arguments and return no results. Method main calls each method twice (lines 17–20). Method useLocalVariable declares local variable x (line 28). When useLocalVariable is first called (line 17), it creates local variable x and initializes it to 25 (line 28), outputs the value of x (lines 30–31), increments x (line 32) and outputs the value of x again (lines 33–34). When useLocalVariable is called a second time (line 19), it recreates local variable x and reinitializes it to 25, so the output of each useLocalVariable call is identical.

```
1  // Fig. 6.9: Scope.java
2  // Scope class demonstrates field and local variable scopes.
3
4  public class Scope
5  {
6      // field that is accessible to all methods of this class
7      private static int x = 1;
8
```

Fig. 6.9 | Scope class demonstrates field and local variable scopes. (Part 1 of 2.)