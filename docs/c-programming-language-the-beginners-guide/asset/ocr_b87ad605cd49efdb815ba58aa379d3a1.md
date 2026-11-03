The function itself requires no arguments. It simply generates a random integer value. That value is stored in variable r at line 8 of the above code. The printf function at line 10 displays the result. Build and run the code.

For the rand function to work best, you must ‘seed’ the randomizer. That's a software machine that generates random numbers. The random seeding function is called which is also defined in the stdlib.h header file. In the code, insert the srand function in the line above rand like so:

+   - #include
+   - #include 3
+   4 int main()
+   5 {
+   6 int r;
+   7
+   - srand(66);
+   - r = rand();
+   
+   10
+   11 printf("%d is a random number.\n",r); 12
+   13 return(0);
+   14 }
+   15