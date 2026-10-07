
## Chapter 10: Subsetting and Combining SAS Data Sets 157

Figure 10.25: Listing of Data Set New15Dec2017

| Listing of Data Set New15Dec2017 |
| ItemCode | Price |
|--- | --- |
| 204 | 17.87 |
| 175 | 25.11 |
| 208 | - |

You want to use this data set to update the prices in data set Prices. You can use the UPDATE statement like this:

## Program 10.16: Updating a Master File From a Transaction File

```
proc sort data=Prices;
  by ItemCode;
run;

proc sort data=New15Dec2017;
  by ItemCode;
run;

data Prices_15Dec2017;
  update Prices New15Dec2017;
  by ItemCode;
run;
```

Here is the result:

Figure 10.26: Listing of Data Set Prices_15Dec2017

| Listing of Data Set Prices_15Dec2017 |
| ItemCode | Description | Price |
|--- | --- | --- |
| 150 | 50 foot hose | 19.95 |
| 175 | 75 foot hose | 25.11 |
| 200 | greeting card | 1.99 |
| 204 | 25 lb grass seed | 17.87 |
| 208 | 40 lb. fertilizer | 17.98 |

Only nonmissing values of Price in the transaction data set replaced values in the master file, as shown in this listing.

You may want to take a look at Chapter 26, “PROC SQL,” to see other ways to combine data from multiple data sets.

## 10.16 Problems

Solutions to odd-numbered problems are located at the back of this book. Solutions to all problems are available to professors. If you are a professor, visit the book's companion website at support.sas.com/codery for information about how to obtain the solutions to all problems.

- 1. Using the SAS data set, create two temporary SAS data sets called Subset_A and Subset_B. Include in both of these data sets a variable Combined equal to .001 times WBC RBC. Subset_A should contain all observations from Blood where Gender is Female and BloodType should contain all observations from Blood where Gender is equal to AB. Subset_B should contain BloodType is equal to AB, and Combined is greater than or equal to 14.
- 2. Using the SAS data set Hosp, create a temporary SAS data set called Monday2002, consisting of observations from Hosp where the admission date (ADmitDate) falls on a Monday and the year is 2002. Include in this data set a variable Age, computed as the person's age of all the admission date, rounded to the nearest year.
- 3. Using the SAS data set Cold, create two temporary SAS data sets by selecting all subjects with cholesterol levels (Chol) below 100. Place the male subjects in Lowmale and the female subjects in Lowfemale. Do this using a single DATA step.
- 4. Using the SAS data set Bicycles, create two temporary SAS data sets as follows: Mountain_USA consists of all observations from Bicycles where Country is USA and Model is Mountain Bike. Road_Frame consists of all observations from Bicycles where Country is France and Model is Road Bike. Print these two data sets.
- 5. Print out the observations in the two data sets Inventory and NewProducts. Create a new temporary SAS data set (Updated) containing all the observations in Inventory followed by all the observations in NewProducts. Sorting the result set and print out the observations.
- 6. Repeat Problem 5, except this time Inventory and NewProducts (create two temporary SAS data sets for the sorted observations). Create a new, temporary SAS data set (Updated) by interleaving the two temporary, sorted SAS data sets. Print out the result.
- 7. Using the Gym set, create a new SAS data set (Percent) that contains all the variables in Gym plus a new variable (call CostPercent) that represents the Cost as a percentage of the average cost for all subjects. Use PROC MEANS create a SAS data set containing the mean cost (see Program 10.7 to see how to do this). Round this to the nearest percent.

Run the program to create a SAS data set called Markup:

```
data Markup;
  input Manuf : $10. Markup;
  datalines;
  Cannondale 1.05
  ;
```

Combine this data set with the Bicycles data set so that each observation in the Bicycles data set has a markup value of 1.05 or 1, depending on whether the bicycle is made by Cannondale or Trek. In this new data set (call it Markup_Prices), create a new variable (NewTotal) as TotalSales times Markup.

- 9. Merge the Purchase and Inventory data sets to create a new, temporary SAS data set (Pur_Price) where the Price value found in the Inventory data set is added to each observation in the Purchase data set, based on the Model number (Model). There are some models in the Inventory data set that were not purchased (and, therefore, are not in the Purchase data set). Do not include these models in your new data set. Based on the variable Quantity in the Purchase data set, compute the
- 10. Merge the Purchase and Inventory data sets without sorting either one. Use the BY statement. Check the set.
- 11. Merge the Purchase and Inventory data sets without sorting either one. Use the BY statement. Check the set.
- 12. Merge the Purchase and Inventory data sets without sorting either one. Use the BY statement. Check the set.
- 13. Merge the Purchase and Inventory data sets without sorting either one. Use the BY statement. Check the set.
- 14. Data set Inventory contains two variables: Model (an character variable) and Price (a numeric value). The price of M567 has changed to 25.95 and the price of X999 has changed to 35.99. Create a temporary SAS data set (call it NewPrices) by updating the prices in the

## Chapter 10: Subsetting and Combining SAS Data Sets 159

## Chapter 11: Working with Numeric Functions

- 11.1 Introduction........................................................................... 161
- 11.2 Functions That Round and Truncate Numeric Values............................... 161
- 11.3 Functions That Work with Missing Values............................................... 163
- 11.4 Setting Character and Numeric Values to Missing.............................. 163
- 11.5 Descriptive Statistics Functions........................................................... 164
- 11.6 Computing Sums within an Observation............................................... 166
- 11.7 Mathematical Functions................................................................ 167
- 11.8 Computing Some Useful Constants............................................................... 168
- 11.9 Generating Random Numbers............................................................... 168
- 11.10 Special Functions....................................................................... 172
- 11.11 Functions That Return Values from Previous Observations.............................. 174
- 11.12 Sorting Within an Observations—a Game Changer........................... 177
- 11.13 Problems...................................................................... 179

### 11.1 Introduction

SAS functions are essential tools in DATA programming. They perform tasks such as running numbers, computing dates from month-day-year values, summing and averaging the values of SAS variables, and hundreds of other tasks. This chapter describes some of the functions that operate on character data. Date functions were discussed separately in Chapter 9.

There is so much to say about SAS functions that one could write a whole book on the subject. As a matter of fact, someone did. Please check out SAS Functions by Example, 2nd edition* by this author. Information about SAS functions can be found on the SAS Help Center at http://go.documentation.sas.com. These two chapters touch only the surface of the enormous power of SAS functions.

### 11.2 Functions That Round and Truncate Numeric Values

Three of the most useful functions in this category are the ROUND, INT, and CEIL functions. As the names suggest, ROUND is used to round numbers, either to the nearest integer or to other values such as 10ths or 100ths. The INT function returns the integer portion of a numeric value. (That is different
