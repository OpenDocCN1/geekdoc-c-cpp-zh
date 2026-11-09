G65 P8000 L2 E10 J20 J30 J40 H50 K60 K70 F80

| Argument | Argument Specification Type | Referred Variable | Assigned Value | Comment |
|---|---|---|---|---|
| E10 | Argument specification I | #8 | 10 | |
| J20 | Both specifications equivalent | #5 | 20 | |
| J30 | Argument specification II (J_j) | #8 | 30 | Overwrites old value |
| J40 | Argument specification II (J_j) | #11 | 40 | |
| H50 | Argument specification I | #11 | 50 | Overwrites old value |
| K60 | Argument specification II (K_k) | #12 | 60 | |
| K70 | Argument specification II (K_k) | #15 | 70 | |
| F80 | Argument specification I | #9 | 80 | |

**TABLE 7.6** Example of Mixed-Type Argument Specification

+   1. **Argument specification:** E10 K60 J20 J30 J40 H50 K60 K70 F80  
+      **Variable assignment:** #6 = 60, #8 = 20, #9 = 80, #11 = 50, #14 = 40, #15 = 60, #18 = 70
+   
+   2. **Argument specification:** B20 A10 D40 J50 K60  
+      **Variable assignment:** #1 = 10, #2 = 20, #5 = 50, #6 = 60, #7 = 40
+   
+   3. **Argument specification:** B20 A10 D40 K60 J50  
+      **Variable assignment:** #1 = 10, #2 = 20, #6 = 60, #7 = 40, #8 = 50
+   
+   4. **Argument specification:** I10 I10 I10 I10 D40 K60 J50  
+      **Variable assignment:** #4 = 10, #7 = 40, #10 = 10, #13 = 10, #15 = 60, #17 = 50

# ## An Example of a G-Code Macro Call with Arguments

Having discussed the methods of argument specification, we are now in a position to write a macro for redefining G01, a problem that was introduced at the end of Sec. 7.4. For redefining G01, one would need