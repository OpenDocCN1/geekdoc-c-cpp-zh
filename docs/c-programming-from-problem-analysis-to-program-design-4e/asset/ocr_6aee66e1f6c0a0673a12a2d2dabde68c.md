> Create an application that can be used by a temporary job placement office that provides staffing for sales positions. The agency places people in positions for a four month trial period. At the beginning of the placement, an initial sales goal baseline is established for the salesperson. It is expected that each of the temporary salesmen will increase their sales by at least 5% each month over the four month period. After the second month, it is expected the sales will increase 10% from the previous month, the third month sales should increase by 15% from the previous month, and during the fourth month sales should increase by 20% over the previous month. At the end of the trial period, salesmen who met all projected sales are hired.
> 
> For testing purposes, allow the user to enter four salesmen. After asking the user for the person's name, use the entered first name as part of the prompt for requesting the initial projected sales goal. Display a table showing the person's name with last name listed first, followed by a comma, and then their first name. Show the projected sales figures for the upcoming four month period so that management may use the report for planning purposes.
> 
> Design a modularized solution (with methods) to display the table.

# FIGURE 8-8 Problem specification for TempAgency example

# ANALYZE THE PROBLEM

You should review the problem specification in Figure 8-8 and make sure you understand the problem definition. Values will be entered into the program to represent each salesman's name and his projected sales goal. The name is stored in a string array. The initial sales goal is stored in a two-dimensional array that is also used to hold the target sales for the following four months. Each row stores sales for a different salesperson. The columns store the initial sales and subsequent monthly goals.

# DATA

Table 8-3 lists the data field members needed for the temp agency problem.

# TABLE 8-3 Instance field members for the TempAgency class

| Data item description | Type | Identifier |
|---|---|---|
| Names of new salespersons | string[ ] | salesman |
| Sales with projected goals | double[ , ] | sales |