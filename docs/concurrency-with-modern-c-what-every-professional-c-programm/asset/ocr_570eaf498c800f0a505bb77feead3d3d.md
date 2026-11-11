# ### 11.1.3 Minimize Waiting

You may have heard of Amdahl's law¹. It predicts the theoretical maximum speedup you can get using multiple processors. The law is quite simple. If p is the proportion of your code, that can run concurrently, you get a maximum speedup of $\frac{1}{1-p}$. So, if 90% of your code can run concurrently, you get at most a 10 times speedup: $\frac{1}{1-p} = \frac{1}{1-0.9} = \frac{1}{0.1} = 10$.

To see it from the opposite perspective, if 10% of your code has to run sequentially because you use a lock, you get at most a ten times speedup. Of course, I assumed that you have access to infinite processing resources.

The graphic shows a direct consequence of Amdahl's law explicitly.

![](bbox=[0.12, 0.335, 0.85, 0.77])

By Daniels220 at English Wikipedia, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=6678551

The optimum number of cores depends highly on the parallel portion of your code. For example: If you have 50% parallel code, you reach the peak performance with 16 cores. Using more cores makes

¹https://en.wikipedia.org/wiki/Amdahl%27s_law