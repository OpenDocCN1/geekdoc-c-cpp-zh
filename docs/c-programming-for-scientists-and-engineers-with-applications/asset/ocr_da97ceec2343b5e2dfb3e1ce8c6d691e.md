# 7.6 Sample Programs

# 7.6.4 Maximum and Minimum Values

Problem Write a program to locate and print the maximum and the minimum values of real data stored in an array. Use a function to find the maximum and minimum values. This example shows the use of a function to process an array using call by name and address. Since the function returns two values, the maximum and minimum values must be passed by address.

Method

+   Input the values into an array
Assume the first value is the maximum and the minimum
For each value of the array:
  If the value is less than the minimum value, update the minimum value
  If the value is greater than the maximum value, update the maximum value
  End for
Output the maximum and the minimum values
Stop

Data

+   List of integer numbers.

Pseudocode

```
main:
Input the array having n elements
Call maxmin(n, a, amax, amin)
Print amax and amin
Stop
```

```
function maxmin:
amax ← a[0]\amin ← a[0]
for each array element i
if a[i] > amax
amax ← a[i]
else if a[i] < amin
```