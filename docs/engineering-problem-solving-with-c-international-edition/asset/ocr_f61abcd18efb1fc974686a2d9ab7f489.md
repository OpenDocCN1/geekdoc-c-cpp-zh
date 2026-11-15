If x and y are simple variables, then a valid call to this function is
switch2(&x, &y);
If ptr_1 points to variable x, and ptr_2 points to the variable y, then the values in x and y
can be switched with this reference:
switch2(ptr_1,ptr_2);
Elements x[i] and x[j] could also be switched with the statements
switch2(&x[i],&x[j]);
switch2(x+i,x+j);
but not with the statement
switch2(x[i],x[j]); /* invalid statement */

![](bbox=[0.13, 0.29, 0.2, 0.35])

> The actual parameter that corresponds to a pointer argument must be an address or pointer.

# PRACTICE!

Consider the references to the switch2 function. For invalid references, explain why the reference is invalid. For valid references, give a memory snapshot before and after the reference.

+   1. float x=1.5, y=3.0, *ptr_x=&x, *ptr_y=&y;
+      ...
+      switch2(ptr_x,ptr_y);
+   2. int f2, g=7, *ptr_f=&f, *ptr_g=&g;
+      ...
+      switch2(ptr_f,ptr_g);
+   3. int f2, g=7, *ptr_f=&f, *ptr_g=&g;
+      ...
+      switch2(*ptr_f,*ptr_g);
+   4. int f2, g=7, *ptr_f=&f, *ptr_g=&g;
+      ...
+      switch2(&ptr_f,&ptr_g);
+   5. int f2, g=7, *ptr_f=&f, *ptr_g=&g;
+      ...
+      switch2(&f,&g);
+   6. int f2, g=7, *ptr_f=&f, *ptr_g=&g;
+      ...
+      switch2(f,g);