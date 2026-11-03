to the source code, click Build and Run, and you will see that the output only displays the string arguments you specified for the puts functions.

A second type of comment uses two slash symbols “//” at the start of the line. You can use this comment to disable a statement in the code, which happens a lot when you are hunting down bugs or trying to fix something. Let’s try it out in line 6 of our previous example:

+   - /* Charles Xavier October 10 , 2016 */
+   - #include 3
+     4 int main()
+     5 {
+   - // puts(“Hello Mr. Programmer”);
+   - puts(“I’m thrilled to meet you”); 8
+     9 return(0);
+     10 }
+     11

Save the code, and then click Build and Run. See how the output doesn’t appear? That’s because the compiler treated it like a