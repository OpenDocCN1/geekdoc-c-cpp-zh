5. See solution file pgm3-5ex5.cpp. Answers are shown in italics:

| Substance | Average Surface Temperature (° Celsius) | Emissivity | Heat Radiated (watts/m²) |
|---|---:|---:|---:|
| Automobile | 47 | .3 | _.082999_ |
| Brick | 45 | .9 | _.209244_ |
| Commercial roof | 48 | .05 | _.0150486_ |

# Chapter 4

# EXERCISES 4.1

+   1. 
+      a. True. Value is 1.
+      b. True. Value is 1.
+      c. True. Value is 1.
+      d. True. Value is 1.
+      e. True. Value is 1.
+      f. False. Value is 10.
+      g. False. Value is 4.
+      h. False. Value is 0.
+      i. False. Value is 10.

```
2. Note: In any relational expression, a non-zero value is considered true and a zero value is considered false.

a. ((a % b) * c) && ((c % b) * a)
   = ((5 % 2) * 4) && ((4 % 2) * 5)
   = (1 * 4) && (0 * 5)
   = 4 && 0   // same as True AND False
   = 0

b. ((a % b) * c) || ((c % b) * a)
   = ((5 % 2) * 4) || ((4 % 2) * 5)
   = (1 * 4) || (0 * 5)
   = 4 || 0   // same as True OR False
   = 1

c. ((b % c) * a) && ((a % c) * b)
   = ((2 % 4) * 5) && ((5 % 4) * 2)
   = (2 * 5) && (1 * 2)
   = 10 && 2   // same as True AND True
   = 1

d. ((b % c) * a) || ((a % c) * b)
   = ((2 % 4) * 5) || ((5 % 4) * 2)
   = (2 * 5) || (1 * 2)
   = 10 || 2   // same as True OR True
   = 1
```