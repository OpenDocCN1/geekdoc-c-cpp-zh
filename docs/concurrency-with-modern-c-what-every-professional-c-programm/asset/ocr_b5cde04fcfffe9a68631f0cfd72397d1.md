# 6.4.1.1.4 Fourth Execution

![](bbox=[0.23, 0.145, 0.8, 0.405])

Fourth execution

Now everything goes wrong. The expressions (e) and (f) read from the expressions (d) and (c) concurrently.

# 6.4.1.1.5 A Short Conclusion

Although I just used the default configuration of CppMem, I got a lot of valuable information and insight. In particular, the graphs from CppMem showed:

+   - All four combinations of x and y are possible: (0,0), (11,0), (0,2000), and (11,2000).
+   - The program has at least one data race and, therefore, has undefined behavior.
+   - Only one of the four possible executions is consistent.