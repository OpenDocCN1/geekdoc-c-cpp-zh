24. Repeat the previous exercise, this time reporting the row percentages. Explain the difference between the interpretation of this table and the previous contingency table.

+   25. Produce the following graphs. What is the strength of each graph? Weakness?
+   a. Histogram of duration.
+   b. Histogram of duration, with overlay of response.
+   c. Normalized histogram of duration, with overlay of response.

26. Using the graph from Exercise 25c, describe the relationship between duration and response.

27. Examine the non-normalized and normalized histograms of duration, with overlay of response. Identify cutoff point(s) for duration, which separate low values of response from high values. Define a new categorical variable, duration_binned, using the cutoff points you identified.

+   28. Provide the following. Describe each of the results.
+   a. Contingency table of duration_binned with response, with counts and column percentages.
+   b. Non-normalized bar graph of duration_binned, with response overlay.
+   c. Normalized bar graph of duration_binned, with response overlay.

29. Construct a contingency table of job with response, with counts and column percentages.

+   30. Referring to the previous exercise, do the following:
+   a. Combine the job categories according to the following response percentages: 0 < 10, 10 < 25, 25 < 33. Name the new variable job2.
+   b. Provide a contingency table of job2 with response, with counts and column percentages. Describe what you see.
+   c. Provide a normalized histogram of job2 with response. Describe the relationship.

For Exercises 31–36, work with the cereals data set. Use either Python or R to solve each problem.

31. Create a bar graph of the Manuf variable with Type overlay.

32. Create a normalized bar graph of the Manuf variable with Type overlay.

33. Create a contingency table of Manuf and Type.

34. Create a histogram of Calories with Manuf overlay.

35. Create a normalized histogram of Calories with Manuf overlay.

36. Bin the Calories variable using bins for 0–90, 90–110, and over 110 calories. Create a bar chart of the binned calories variable with Manuf overlay.

For Exercises 37–60, use the adult_ch3_training data set.

For Exercises 37–40 we demonstrate an example of why it is not recommended to delete outliers at the EDA stage, because it results in changing the character of the data set.