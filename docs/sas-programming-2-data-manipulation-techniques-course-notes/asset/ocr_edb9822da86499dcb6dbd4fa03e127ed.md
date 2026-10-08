# 5.03 Multiple Choice Poll

Which SUBSTR function can extract the group of five numbers from the middle of the Item_Code value?

| PDV Item_Code |
|---|---|
| $ 20 978-1-59994-397-8 |

+   a. substr(Item_Code,5,7)
b. substr(Item_Code,5)
c. substr(Item_Code,7,5)
d. substr(Item_Code,'mid',5)

The variable Acct_Code is in the output for learning purposes so that it can be easily compared to the ID variable. Otherwise, there is no need for it, and it could be dropped from the charities data set.

# Create the List of Charities: Step 1

> The last non-blank character in the Acct_Code value occurs in different positions for different observations.

| Partial orion.biz_list |
| Acct_Code | last character in position 4 |
| AEK3 |
| AQI2 last character in position 3 |
| ATS1 |
| CBO3 |
| CCI2 |
| ON12 |
| CS1 need some way to determine the position of the last character so that the SUBSTR function can extract it. |
| CS2 |