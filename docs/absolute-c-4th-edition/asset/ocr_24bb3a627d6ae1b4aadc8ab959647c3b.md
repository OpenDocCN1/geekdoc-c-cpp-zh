# Self-Test Exercises

+   18. What is the output of the following?
+   
+   ```cpp
+   int count = 3;
+   while (count-- > 0)
+       cout << count << " ";
+   ```
+   
+   19. What is the output of the following?
+   
+   ```cpp
+   int count = 3;
+   while (--count > 0)
+       cout << count << " ";
+   ```
+   
+   20. What is the output of the following?
+   
+   ```cpp
+   int n = 1;
+   do
+       cout << n << " ";
+   while (n++ <= 3);
+   ```
+   
+   21. What is the output of the following?
+   
+   ```cpp
+   int n = 1;
+   do
+       cout << n << " ";
+   while (++n <= 3);
+   ```
+   
+   22. What is the output produced by the following? (x is of type int.)
+   
+   ```cpp
+   int x = 10;
+   while (x > 0)
+   {
+       cout << x << endl;
+       x = x - 3;
+   }
+   ```
+   
+   23. What output would be produced in the previous exercise if the > sign were replaced with <?
+   
+   24. What is the output produced by the following? (x is of type int.)
+   
+   ```cpp
+   int x = 10;
+   do
+   {
+       cout << x << endl;
+       x = x - 3;
+   } while (x > 0);
+   ```