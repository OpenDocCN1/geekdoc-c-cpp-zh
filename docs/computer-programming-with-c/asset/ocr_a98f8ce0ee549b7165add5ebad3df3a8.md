# The statement

```
s3 = s1+s2;
```

will invoke an operator function using object s1 and object s2 will be passed as an argument to the function. This means that the member str of object s1 can be directly accessed inside the operator function because the function is invoked by object s1 itself. Also, object s2 is passed as an argument and will be initialized to the formal argument t which is created as a part of operator function, and hence the member str of s2 can now be accessed using object as t.str as shown in the code.

Also, we create a pointer res inside the operator function to point to the resultant String, which should be the concatenation of individual Strings present in objects s1 and s2. This means that the length of the resultant string will be the addition of length of s1's string and length of s2's string. Hence, we allocate the memory for result using the statement below:

```
res = new char[strlen(str) + strlen(t.str) + 1];
```

Further, the strcat() function used inside the operator function makes the pointer res to point to the concatenation of strings pointed by member str of object s1 and member str of object s2 ("Computer" + "Programming" = "ComputerProgramming"). Also, the object of class String is created using the new and returned to the main() function. Hence, the object s3 now contains the concatenation of strings present in s1 and s2 as shown in the Figure 13.39.

The statement s3.output(); invokes the output() function to print the result string stored inside object s3 as seen from the last line of main() function.

![](bbox=[0.216, 0.489, 0.754, 0.613])

**Figure 13.39:** State of object s3

# Quiz

+   1. Operator overloading in C++ facilitates.
+      (a) Runtime polymorphism
+      (b) Compile time polymorphism
+      (c) Abstraction
+      (d) a and c
+      (e) b and c
+   
+   2. Which of the following operators cannot be overloaded?
+      (a) +
+      (b) ++
+      (c) sizeof
+      (d) ->