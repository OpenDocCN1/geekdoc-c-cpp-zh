![](bbox=[0.08, 0.074, 0.907, 0.225])

**FIGURE 4.2** Venn diagram representation for bitwise AND, OR, and XOR.

three logical operations are associative. So, for example, #1 AND #2 is equivalent to #2 AND #1.

Some examples of bitwise logical operations are given below:

+   #1 = 4;             (Same as binary 0100)
+   #2 = 3;             (Same as binary 0011)
+   #3 = 1;             (Same as binary 0001)
+   #4 = #1 AND #2;     (Result in binary form is 0000. So, #4 is set to 0.000)
+   #5 = #2 AND #3;     (Result in binary form is 0001. So, #5 is set to 1.000)
+   #6 = #1 OR #2;       (Result in binary form is 0111. So, #6 is set to 7.000)
+   #7 = #2 OR #3;       (Result in binary form is 0011. So, #7 is set to 3.000)
+   #8 = #1 XOR #2;      (Result in binary form is 0111. So, #8 is set to 7.000)
+   #9 = #2 XOR #3;      (Result in binary form is 0010. So, #9 is set to 2.000)

The logical functions are operated upon integers. If an integer value (or a variable containing an integer value) is not specified, rounding is automatically done to the nearest integer:

+   #1 = 1.5;
+   #2 = 1.4999999;
+   #3 = #1 AND #2;
+   
+   (Equivalent to #3 = 2 AND 1; which is bitwise AND of binary numbers 010 and 001. The result is binary 000, which is the same as decimal 0. So, 0.000 is stored in #3)
+   
+   #4 = 2.5 XOR 2.4999999;
+   
+   (Equivalent to #4 = 3 XOR 2; which is bitwise XOR of binary numbers 011 and 010. The result is binary 001, which is the same as decimal 1. So, 1.000 is stored in #4)

Though the bitwise operations are actually logical operations, they look similar to arithmetic operations. In fact, the result of bitwise operations can be used in arithmetic calculations also, though their purpose is entirely different. So, a statement like

```
#1 = #2 * #3 AND #4;
```