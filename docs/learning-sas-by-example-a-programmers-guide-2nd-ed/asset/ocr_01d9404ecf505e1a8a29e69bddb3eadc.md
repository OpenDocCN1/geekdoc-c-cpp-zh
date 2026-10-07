# 10.16 Problems

Solutions to odd-numbered problems are located at the back of this book. Solutions to all problems are available to professors. If you are a professor, visit the book's companion website at support.sas.com/codery for information about how to obtain the solutions to all problems.

+   1. Using the SAS data sett, create two temporary SAS data sets called Subset_A and Subset_B. Include in both of these data sets a variable Combined equal to .001 times WBC RBC. Subset_A should contain all observations from Blood where Gender is Female and BloodType should contain all observations from Blood where Gender is equal to AB. Subset_B should contain BloodType is equal to AB, and Combined is greater than or equal to 14.
2. Using the SAS data set Hosp, create a temporary SAS data set called Monday2002, consisting of observations from Hosp where the admission date (ADmitDate) falls on a Monday and the year is 2002. Include in this data set a variable Age, computed as the person's age of all the admission date, rounded to the nearest year.
3. Using the SAS data set Cold, create two temporary SAS data sets by selecting all subjects with cholesterol levels (Chol) below 100. Place the male subjects in Lowmale and the female subjects in Lowfemale. Do this using a single DATA step.
4. Using the SAS data set Bicycles, create two temporary SAS data sets as follows: Mountain_USA consists of all observations from Bicycles where Country is USA and Model is Mountain Bike. Road_Frame consists of all observations from Bicycles where Country is France and Model is Road Bike. Print these two data sets.
5. Print out the observations in the two data sets Inventory and NewProducts. Create a new temporary SAS data set (Updated) containing all the observations in Inventory followed by all the observations in NewProducts. Sorting the result set and print out the observations.
6. Repeat Problem 5, except this time Inventory and NewProducts (create two temporary SAS data sets for the sorted observations). Create a new, temporary SAS data set (Updated) by interleaving the two temporary, sorted SAS data sets. Print out the result.
7. Using the Gym set, create a new SAS data set (Percent) that contains all the variables in Gym plus a new variable (call CostPercent) that represents the Cost as a percentage of the average cost for all subjects. Use PROC MEANS create a SAS data set containing the mean cost (see Program 10.7 to see how to do this). Round this to the nearest percent.

Run the program to create a SAS data set called Markup:

```
data Markup;
  input Manuf : $10. Markup;
  datalines;
  Cannondale 1.05
  ;
```

Combine this data set with the Bicycles data set so that each observation in the Bicycles data set has a markup value of 1.05 or 1, depending on whether the bicycle is made by Cannondale or Trek. In this new data set (call it Markup_Prices), create a new variable (NewTotal) as TotalSales times Markup.