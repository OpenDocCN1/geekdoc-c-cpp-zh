# Chapter 26: Introducing the Structured Query Language 449

Figure 26.13: Listing of New_Members_Order

| Listing of Data Set New_Members_Order |
| Name | DOB | Gender | Subj |
|---|---|---|--|
| Ostermeier | 03/05/1977 | F | 010 |
| Brown | 06/07/1999 | M | 013 |

Each of the four columns of New_Members_Order has the same data type (character or numeric) as the four columns of Demographic. So, if you omit the CORRESPONDING keyword when performing a union of these two data sets, you will have the following result:

Figure 26.14: Result of Omitting the Keyword CORRESPONDING

| Listing of Data Set Complete_List With the Keyword CORRESPONDING Omitted |
| Subj | DOB | Gender | Name |
|---|---|---|--|
| 001 | 10/15/1960 | M | Friedman |
| 002 | 08/01/1955 | M | Stern |
| 003 | 12/25/1988 | F | McGoldrick |
| 005 | 05/28/1949 | F | Chien |
| Ostermeier | 03/05/1977 | F | 010 |
| Brown | 06/07/1999 | M | 013 |

You can now see why you need to choose the correct UNION operator when concatenating two data sets.

# 26.6 Using Summary Functions

You can use these functions as MEAN and SUM to create new variables that represent means or sums of other variables. You can also create new variables within the query.

The following program shows one of the strengths of PROC SQL, which is the ability to add a summary variable to an existing table.

Suppose you want to express each person's height in the Health data set as a percentage of the mean height of all the subjects. You would first use PROC MEANS to create a data set containing the mean height. You would then combine this with the original data set and perform the calculation. (See the section about combining detail and summary data in Chapter 10 for an example.) PROC SQL makes this task much easier. Let's take a look.