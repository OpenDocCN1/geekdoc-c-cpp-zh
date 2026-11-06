+   7. Hand-trace the following code, showing the value of n and the output. What potential error do you notice?
+   
+   ~~~cpp
+   int n = 1;
+   while (n <= 3)
+   {
+       cout << n << ", ";
+       n++;
+   }
+   ~~~

+   8. Hand-trace the following code, assuming that a is 2 and n is 4. Then explain what the code does for arbitrary values of a and n.
+   
+   ~~~cpp
+   int r = 1;
+   int i = 1;
+   while (i <= n)
+   {
+       r = r * a;
+       i++;
+   }
+   ~~~

+   9. Trace the following code. What error do you observe?
+   
+   ~~~cpp
+   int n = 1;
+   while (n != 50)
+   {
+       cout << n << endl;
+       n = n + 10;
+   }
+   ~~~

+   10. The following pseudocode is intended to count the number of digits in the number n:
+   
+   ~~~text
+   count = 1
+   temp = n
+   while (temp > 10)
+       Increment count.
+       Divide temp by 10.
+   ~~~
+   
+   Trace the pseudocode for n = 123 and n = 100. What error do you find?

**Practice It** Now you can try these exercises at the end of the chapter: R4.1, R4.5.

# ## 4.3 The for Loop

The for loop is used when a value runs from a starting point to an ending point with a constant increment or decrement.

It often happens that you want to execute a sequence of statements a given number of times. You can use a *while* loop that is controlled by a counter, as in the following example:

```
~~~cpp
counter = 1; // Initialize the counter
while (counter <= 10) // Check the counter
{
    cout << counter << endl;
    counter++; // Update the counter
}
~~~
```

Because this loop type is so common, there is a special form for it, called the for loop (see Syntax 4.2).