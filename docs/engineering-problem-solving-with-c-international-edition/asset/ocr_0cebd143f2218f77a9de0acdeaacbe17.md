```
/* Print height estimates. */
printf("\nHeight Estimates in Inches \n");
printf("Femur Female Estimate: %5.1f \n",femur_ht_f);
printf("Femur Male Estimate: %5.1f \n",femur_ht_m);
printf("Humerus Female Estimate: %5.1f \n",humerus_ht_f);
printf("Humerus Male Estimate: %5.1f \n",humerus_ht_m);

/* Exit program. */
return 0;
}
********************************************************************/
```

# 5. TESTING

We first test the program using the data from the hand example. This generates the following interaction:

Enter Values in Inches.
Enter femur length:
15
Enter humerus length:
12

Height Estimates in Inches
Femur Female Estimate: 57.8
Femur Male Estimate: 60.2
Humerus Female Estimate: 61.8
Humerus Male Estimate: 62.7

The values computed match the hand example, so we can then test the program with additional lengths. If the values computed had not matched the result from the hand example, we would then need to determine if the error is in the hand example or in the C program.

# MODIFY!

These problems relate to the program developed in this section for computing height estimates from bone lengths.

+   1. Modify the program so that it converts the output values from inches to feet. The input would still be entered in inches. Use a single value for the output, such as 6.5 feet.
+   2. Modify the program so that it asks the user to enter the values in feet. The program would then need to convert the values in feet to centimeters before doing the computations. The output would also print the output heights in feet, as in 6.5 feet.
+   3. Modify the program so that it reads the input values in inches and then estimates the output heights using feet and inches. (Note that you are printing two output values for each height estimate.)