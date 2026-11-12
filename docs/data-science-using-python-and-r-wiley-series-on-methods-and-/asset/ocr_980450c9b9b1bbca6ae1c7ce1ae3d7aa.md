+   20. Do the following for the *campaign* field.
+   a. Standardize the variable.
+   b. Identify how many outliers there are and identify the most extreme outlier.

# HANDS-ON ANALYSIS

For Exercises 21–25, work with the *Nutrition_subset* data set. The data set contains the weight in grams along with the amount of saturated fat and the amount of cholesterol for a set of 961 foods. Use either Python or R to solve each problem.

+   21. The elements in this data set are food items of various sizes, ranging from a teaspoon of cinnamon to an entire carrot cake.
+   a. Sort the data set by the saturated fat (*saturated_fat*) and produce a listing of the five food items highest in saturated fat.
+   b. Comment on the validity of comparing food items of different sizes.

+   22. Derive a new variable, *saturated_fat_per_gram*, by dividing the amount of saturated fat by the weight in grams.
+   a. Sort the data set by *saturated_fat_per_gram* and produce a listing of the five food items highest in saturated fat per gram.
+   b. Which food has the most saturated fat per gram?

+   23. Derive a new variable, *cholesterol_per_gram*.
+   a. Sort the data set by *cholesterol_per_gram* and produce a listing of the five food items highest in cholesterol fat per gram.
+   b. Which food has the most cholesterol fat per gram?

+   24. Standardize the field *saturated_fat_per_gram*. Produce a listing of all the food items that are outliers at the high end of the scale. How many food items are outliers at the low end of the scale?

+   25. Standardize the field *cholesterol_per_gram*. Produce a listing of all the food items that are outliers at the high end of the scale.

For Exercises 26–30, work with the *adult_ch3_training* data set. The response is whether education exceeds $50,000.

+   26. Add a record index field to the data set.

+   27. Determine whether any outliers exist for the *education* field.

+   28. Do the following for the age field.
+   a. Standardize the variable.
+   b. Identify how many outliers there are and identify the most extreme outlier.

+   29. Derive a flag for capital-gain, called capital-gain-flag, which equals 0 for capital gain equals zero, and 1 otherwise.

+   30. Age anomaly? Select only records with age at least 80. Construct a histogram of age. Explain what you see in one sentence and why it is like that in another sentence.