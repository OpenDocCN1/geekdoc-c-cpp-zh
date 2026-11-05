With call by reference, no copy is made of the contents. A copy is made of the reference (address) to the location in which the array is stored, and the copy is stored in a variable. As shown in Figure 7-7, the formal parameter, temp, references the same location in memory as temperature does. The values entered into the temp array in the InputValues() method are stored in the memory cells referenced by temperature.

# Array Assignment

The assignment operator = may not work as you would think it should when used with reference types such as arrays. If an additional array is defined and an assignment is made, the assignment operator and the array reference the same elements. Individual elements are not copied to another memory location. Consider the following statements that could be written after the temperature array is filled with values:

```
int [ ] t = new int[5];
t = temperature;
t[1] = 44;
```

Figure 7-8 illustrates the result of the assignment statements. Any reference to temperature[1] accesses 44.

![](bbox=[0.15, 0.62, 0.92, 0.9])

FIGURE 7-8 Assignment of an array to reference another array

Example 7-13 includes the complete code listing from the program statements used in Figures 7-7 and 7-8, which illustrate the assignment and use of arrays as method parameters.