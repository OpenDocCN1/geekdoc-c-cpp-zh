Step 2: Then variable has been tested for a given condition, if the condition results in true then C statements enclosed in loop body get executed by compiler, otherwise control skips the loop and continues with the next statements following loop.

Step 3: After successful execution of loop's body, the counter variable is incremented or decremented, depending on the operation (++ or --).

# Various Forms of for LOOP

Here we use variable num in all the below examples:

+   1. Here instead of num++, We can use num=num+1, which is the same as num++.
+   
+   ```c
+   for(num=10;num<20;num=num+1)
+   ```

+   2. Initialization part can be skipped from loop as shown below, the counter variable is declared before the loop itself.
+   
+   ```c
+   int num=10;
+   for(;num<20;num++)
+   ```
+   
+   Must Note: Although we can skip init part but semicolon (;) before condition is must, without which you will get compilation error.

+   3. Like initialization, you can also skip the increment part as we did below. In this case semicolon (;) is must, after condition logic. The increment part is being done in for loop body itself.
+   
+   ```c
+   for(num=10;num<20;)
+   {
+       //Code
+       num++;
+   }
+   ```

+   4. Below case is also possible, increment in body and in it during declaration of counter variable.
+   
+   ```c
+   int num=10;
+   for(;num<20;)
+   {
+   //Statements
+   num++;
+   }
+   ```

+   5. Counter can be decremented also. In the below example the variable gets decremented each time the loop runs until the condition num>10 becomes false.
+   
+   ```c
+   for(num=20;num>10;num--)
+   ```

# 3.3.4 Nested for Loop

Nested loops or nesting of loop is placing one loop into another loop to execute a program based on multiple conditions and checks.

Here we have an example of nesting of for loop, likewise you can use nesting of various loops such as while, while do or for.