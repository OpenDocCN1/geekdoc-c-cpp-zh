|  |  |  |
|---|---:|---:|
| Remove routine calls and put all the code in line | 0:45 | 53% |
| Rewrite the whole routine in assembler | 0:22 | 51% |
| **Final** | **0:22** | **98%** |

Note: The steady progress of optimizations in this table doesn’t imply that all optimizations work. I haven’t shown all the things I tried that doubled the run time. At least two-thirds of the optimizations I tried didn’t work.

# 25.6 Summary of the Approach to Code Tuning

You should take the following steps as you consider whether code tuning can help you improve the performance of a program:

+   1. Develop the software by using well-designed code that’s easy to understand and modify.
+   
+   2. If performance is poor,
+      a. Save a working version of the code so that you can get back to the “last known good state.”
+      b. Measure the system to find hot spots.
+      c. Determine whether the weak performance comes from inadequate design, data types, or algorithms and whether code tuning is appropriate. If code tuning isn’t appropriate, go back to step 1.
+      d. Tune the bottleneck identified in step (c).
+      e. Measure each improvement one at a time.
+      f. If an improvement doesn’t improve the code, revert to the code saved in step (a). (Typically, more than half the attempted tunings will produce only a negligible improvement in performance or degrade performance.)
+   
+   3. Repeat from step 2.

# Additional Resources

This section contains resources related to performance improvement in general. For additional resources that discuss specific code-tuning techniques, see the “Additional Resources” section at the end of Chapter 26.

# Performance

Smith, Connie U. and Lloyd G. Williams. *Performance Solutions: A Practical Guide to Creating Responsive, Scalable Software*. Boston, MA: Addison-Wesley, 2002. This book covers software performance engineering, an approach for building performance into