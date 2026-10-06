# 6.2 Writing Your Own Functions

For example, a salesperson with $16,000 in monthly sales will earn a 14 percent commission ($2,240). Another salesperson with $20,000 in monthly sales will earn a 16 percent commission ($3,200). A person with $30,000 in monthly sales will earn an 18 percent commission ($5,400).
Because the staff gets paid once per month, Hal allows each employee to take up to $2,000 per month in advance. When sales commissions are calculated, the amount of each employee's advance is subtracted from the commission. If any salesperson's commission is less than the amount of his or her advance, the salesperson must reimburse Hal for the difference. To calculate a salesperson's monthly pay, Hal uses the following formula:
Pay = Sales × Commission rate – Advanced pay

Hal asked you to write a program that makes this calculation for him. The following algorithm outline outlines the steps the program must take:

+   1. Get the salesperson's monthly sales.
2. Get the amount of advanced pay.
3. Use the amount of monthly sales to determine the commission rate.
4. Calculate the salesperson's pay if the amount is negative, indicate that the salesperson must reimburse the company.

Program 6-8 shows the pseudocode for the program, which is modularized with numerous functions. Rather than presenting the entire program at once, let's first examine the main module and each function separately. Here is the main module:

# Program 6-8 Commission rate program: main module

```
1 Module main()
2 // Local variables
3 Declare Real sales, commissionRate, advancedPay
4
5 // Get the amount of sales.
6 Set sales = getSales()
7
8 // Get the amount of advanced pay.
9 Set advancedPay = getAdvancedPay()
10
11 // Determine the commission rate.
12 Set commissionRate = determineCommissionRate(sales)
13
14 // Calculate the pay.
15 Set pay = sales * commissionRate - advancedPay
16
17 // Display the amount of pay.
18 Display "The pay is $", pay
19
20 // Determine whether the pay is negative.
21 If pay < 0
22 Display "The salesperson must reimburse
23 Display "the company.\"
24 End If
25 End Module"
```