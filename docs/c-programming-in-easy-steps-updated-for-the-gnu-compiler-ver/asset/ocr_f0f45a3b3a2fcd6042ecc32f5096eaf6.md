+   1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
+   `#include <stdio.h>`
+   
+   2. Declare a structure with two members and one tag
+   ```c
+   struct coords
+   {
+     int x;
+     int y;
+   } point;
+   ```
+   
+   3. Then, create another instance of the structure
+   `struct coords top ;`
+   
+   4. Next, add a main function that initializes both members of each structure
+   ```c
+   int main()
+   {
+     point.x = 5 ; point.y = 8 ;
+     top.x = 15 ; top.y = 24 ;
+   }
+   ```
+   
+   5. Now, output the value stored in each structure member
+   ```c
+   printf("\npoint x: %d, point y: %d\n", point.x , point.y );
+   printf("\ntop x: %d, top y: %d\n" , top.x , top.y );
+   ```
+   
+   6. At the end of the main function block, return a zero integer value, as required by the function declaration
+   `return 0 ;`
+   
+   7. Save the program file, then compile and execute the program to see the values stored in structure members

![](bbox=[0.68, 0.1, 0.82, 0.25])

![](bbox=[0.7, 0.58, 0.92, 0.8])

![](bbox=[0.12, 0.8, 0.7, 0.98])

```
struct coords
{
  int x;
  int y;
} point;
```

```
int main()
{
  point.x = 5 ; point.y = 8 ;
  top.x = 15 ; top.y = 24 ;
}
```

```
printf("\npoint x: %d, point y: %d\n", point.x , point.y );
printf("\ntop x: %d, top y: %d\n" , top.x , top.y );
```

```
return 0 ;
```