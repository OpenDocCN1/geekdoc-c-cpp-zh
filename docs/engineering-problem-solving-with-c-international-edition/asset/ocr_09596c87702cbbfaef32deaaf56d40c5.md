```
// Determine maximum value in the array.
max_x = x[0];
for (k=1; k<=n-1; k++)
if (x[k] > max_x)
max_x = x[k];
// Return maximum value.
return max_x;
}
//----------------------------------------------
```

# 8.5 Problem Solving Applied: Hand Recognition

In this section, we use the new C++ statements presented in this chapter to solve a problem related to hand recognition. For simplicity, we are going to use just five measurements: the length of the five fingers on the right hand. Write a function that has the inputs from an unknown hand and one from an entry in the database. The function should compute the sum of the absolute value of the differences between corresponding fingers. This sum represents the distance between the two hands. The recognition program would use this function to compare the unknown to each hand in the database and then choose the hand from the database that is closest to the unknown. If this difference is less than a specified threshold, then the unknown identify is identified as a match to the database and access is allowed. A program will also be developed to allow us to test this function.

# 1. PROBLEM STATEMENT

Write a function that will compute the overall distance between measurements of two hands.

# 2. INPUT/OUTPUT DESCRIPTION

The following diagram shows that the inputs to the function are the 5 finger lengths for the unknown and the 5 finger lengths from a record in the database. The output is the overall distance measurement.

![](bbox=[0.33, 0.76, 0.82, 0.86])