```
```cpp
cout << num 1 << " " << num2 << " " << first % 5
     << " " << (second % 7) << endl;

return;
}
```
```

31. What is the difference between a pretest loop and a posttest loop? (2, 4, 5)

32. How many times will each of the following loops execute? What is the output in each case? (5)

+   a.
+   ```cpp
+   x = 5;  y = 50;
+   
+       x = x + 10;
+   while (x < y)
+   cout << x << " " << y << endl;
+   ```

+   b.
+   ```cpp
+   x = 5;  y = 80;
+   do
+       x = x * 2;
+   while (x < y)
+   cout << x << " " << y << endl;
+   ```

+   c.
+   ```cpp
+   x = 5;  y = 20;
+   do
+       x = x + 2;
+   while (x >= y)
+   cout << x << " " << y << endl;
+   ```

+   d.
+   ```cpp
+   x = 5;  y = 35;
+   while (x < y)
+       x = x + 10;
+   cout << x << " " << y << endl;
+   ```

+   e.
+   ```cpp
+   x = 5;  y = 30;
+   while (x <= y)
+       x = x * 2;
+   cout << x << " " << y << endl;
+   ```

+   f.
+   ```cpp
+   x = 5;  y = 30;
+   while (x <= y)
+       x = x + 2;
+   cout << x << " " << y << endl;
+   ```

33. Write an input statement validation loop that prompts the user to enter a number less than 20 or greater than 75. (2, 4, 5)

34. Rewrite the following as a for loop. (2, 4)

```
```cpp
int i = 0, value = 0;

while (i <= 20)
{
    if (i % 2 == 0 && i <= 10)
        value = value + i * i;
    else if (i % 2 == 0 && i > 10)
```
```

![](bbox=[0.926, 0.296, 0.999, 0.406])