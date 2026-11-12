
the previous normalized bar chart. The resulting normalized bar graph is shown in Figure 4.11.

We can construct a contingency table of our categorical variable and the response variable using the table() command, and a table of column proportions using the prop.table() command. The details of both commands have been discussed previously. The code is given below.

```
t2 <- table(bank_train$response, bank_train$age_bin); t2
round(prop.table(t2, margin = 2)*100, 1)
```

Note how the use of the semicolon in the first line allows both the construction and saving of the table, and the printing of the table, to happen in one line. The resulting tables are shown in Figures 4.12 and 4.13.

Further methods in EDA may be found in Data Mining and Predictive Analytics.1

## REFERENCES

Python's matplotlib package has a wide range of graphical options. To start investigating further, see the publication: John D. Hunter. Matplotlib: a 2D graphics environment, Computing in Science & Engineering, 9, 90–95, 2007, doi:https://doi.org/10.1109/MCSE.2007.55

We have just brushed the surface of the ggplot2 package! For more information, see the following publication: H. Wickham, ggplot2: Elegant Graphics for Data Analysis, Springer-Verlag, New York, 2009.

## EXERCISES

### CLARIFYING THE CONCEPTS

- 1. When should analysts use exploratory data analysis (EDA) rather than hypothesis testing?
- 2. What are some examples of what EDA allows the user to do?
- 3. Which graph do we use to explore the relationship between a categorical predictor and the target variable?
- 4. What are (non-normalized) bar graphs useful for?
- 5. State one advantage and one disadvantage of using a normalized bar graph.
- 6. State the two best practices when working with bar graphs for EDA?
- 7. What does a contingency table help us to do?
- 8. Explain the two best practices when working with contingency tables in EDA?
- 9. What is a histogram?
- 10. Describe one advantage and one disadvantage of using a normalized histogram.
- 11. What are the best practices for working with histograms in EDA?
- 12. Why might it be useful for the analyst to bin a numeric variable?
- 13. Why do we use the binning method shown in this chapter rather than automatic binning methods?
- 14. Extrapolate from your answer to the previous question and explain why data scientists should use automatic methods of data analysis very carefully.

### WORKING WITH THE DATA

For the following exercises, work with the bank_marketing_training data set. Use either Python or R to solve each problem.

- 15. Create a bar graph of the previous_outcome variable, with response overlay.
- 16. Create a normalized bar graph of previous_outcome variable with response overlay. Describe the relationship between previous_outcome and response.
- 17. Create a contingency table of previous_outcome and response. Compare the contingency table with the non-normalized bar graph and the normalized bar graph.
- 18. Create a histogram of age with response overlay.
- 19. Create a normalized histogram of age with response overlay. Describe the relationship between age and response.
- 20. Bin the age variable using the bins specified in this chapter and create a bar chart of the binned age variable with response overlay.

### HANDS-ON ANALYSIS

For Exercises 21–30, continue working with the bank_marketing_training data set. Use either Python or R to solve each problem.

- 21. Produce the following graphs. What is the strength of each graph? Weakness?
  - a. Bar graph of marital.
  - b. Bar graph of marital, with overlay of response.
  - c. Normalized bar graph of marital, with overlay of response.
- 22. Using the graph from Exercise 21c, describe the relationship between marital and response.
- 23. Do the following with the variables marital and response.
  - a. Build a contingency table, being careful to have the correct variables representing the rows and columns. Report the counts and the column percentages.
  - b. Describe what the contingency table is telling you.
- 24. Repeat the previous exercise, this time reporting the row percentages. Explain the difference between the interpretation of this table and the previous contingency table.
- 25. Produce the following graphs. What is the strength of each graph? Weakness?
  - a. Histogram of duration.
  - b. Histogram of duration, with overlay of response.
  - c. Normalized histogram of duration, with overlay of response.
- 26. Using the graph from Exercise 25c, describe the relationship between duration and response.
- 27. Examine the non-normalized and normalized histograms of duration, with overlay of response. Identify cutoff point(s) for duration, which separate low values of response from high values. Define a new categorical variable, duration_binned, using the cutoff points you identified.
- 28. Provide the following. Describe each of the results.
  - a. Contingency table of duration_binned with response, with counts and column percentages.
  - b. Non-normalized bar graph of duration_binned, with response overlay.
  - c. Normalized bar graph of duration_binned, with response overlay.
- 29. Construct a contingency table of job with response, with counts and column percentages.
- 30. Referring to the previous exercise, do the following:
  - a. Combine the job categories according to the following response percentages: 0 < 10, 10 < 25, 25 < 33. Name the new variable job2.
  - b. Provide a contingency table of job2 with response, with counts and column percentages. Describe what you see.
  - c. Provide a normalized histogram of job2 with response. Describe the relationship.

For Exercises 31–36, work with the cereals data set. Use either Python or R to solve each problem.

- 31. Create a bar graph of the Manuf variable with Type overlay.
- 32. Create a normalized bar graph of the Manuf variable with Type overlay.
- 33. Create a contingency table of Manuf and Type.
- 34. Create a histogram of Calories with Manuf overlay.
- 35. Create a normalized histogram of Calories with Manuf overlay.
- 36. Bin the Calories variable using bins for 0–90, 90–110, and over 110 calories. Create a bar chart of the binned calories variable with Manuf overlay.

For Exercises 37–60, use the adult_ch3_training data set.

For Exercises 37–40 we demonstrate an example of why it is not recommended to delete outliers at the EDA stage, because it results in changing the character of the data set.

- 37. Consider capital-loss. Identify the outliers in capital-loss using the Z-score method. How many outliers are there?
- 38. Construct a bar graph of Income for these outlier records.
- 39. Construct a bar graph of Income for the adult_ch3_training data set as a whole, without omitting the outliers.
- 40. Compare your bar graphs from the previous two exercises. Describe the difference between the two bar graphs. Describe the change to the character of the data set that will result if we delete these outlier records. State your conclusion regarding deleting outliers at the EDA stage.
- 41. Derive a flag for capital-loss, called capital-loss-flag, which equals 0 when capital-loss equals 0, and 1 otherwise. Provide a bar graph of capital-loss-flag.
- 42. Repeat the previous exercise for capital-gain-flag.
- 43. Construct a contingency table of capital-loss-flag vs Income. Include counts and column percentages. Clearly describe the effect of having any capital losses on Income.
- 44. Construct a contingency table of capital-gain-flag vs Income. Include counts and column percentages. Clearly describe the effect of having any capital gains on Income.
- 45. To prepare for further work, rename workclass as workclass-old, marital-status as marital-status-old, and occupation as occupation-old.
- 46. Construct a contingency table with income for the rows and workclass-old for the columns, asking for counts and column percentages.
- 47. Referring to the contingency table from the previous exercise, do the following:
  - a. Provide a one-sentence rationale for why we should combine never-worked and without-pay into no-pay.
  - b. Provide a one-sentence rationale for why we may combine local-gov and state-gov into state-local-gov.
- 48. Perform the changes mentioned in the previous exercise, along with changing "?" to "unknown". Call the new variable workclass. Construct a contingency table with Income for the rows and workclass for the columns, with counts and column percentages. Describe your table using a couple of sentences.
- 49. Construct a contingency table with income for the rows and marital-status-old for the columns, asking for counts and column percentages.
- 50. Referring to the contingency table from the previous sentence, provide two sentences of rationale for why we should combine Married-AF-spouse and Married-civ-spouse into the new category Married, and combine the other statuses into the new category Other.
- 51. Perform the changes mentioned in the previous exercise. Construct a contingency table with income for the rows and marital-status for the columns, with counts and column percentages. Describe your table using a couple of sentences.
- 52. Construct a contingency table with income for the rows and occupation-old for the columns, asking for counts and column percentages.
