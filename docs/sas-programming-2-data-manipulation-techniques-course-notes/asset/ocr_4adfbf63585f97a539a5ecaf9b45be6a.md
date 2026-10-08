# 2.07 Short Answer Poll

Open file p202a05 and submit it. The intent is to drop Country, Street_ID, and Employee_ID from every data set, and to drop State from australia. What is wrong with the program?

```
data use australia (drop=State) other;
set orion,employee_addresses
(drop=Country) Street_ID Employee_ID);
if Country='US' then output usa;
elelse if Country='AU' then output australia;
else output other;
```

# Improved Solution

Use a combination of the DROP= option and the DROP statement to achieve the desired results.

```
data use australia (drop=State) other;
set orion.employee_addresses
(drop=Street_ID Employee_ID);
drop Country;
if Country='US' then output usa;
else if Country='AU' then output australia;
elelse output other;
```

| PDV | Country | Employee_Name | Postal_Code | State | Street_Name | Street_Number |
|---|---|---|---|---|---|---||
| | | | | | | |

If a DROP or KEEP statement is used in the same step as a data set option, the statement is applied first.

Attempting to drop and keep the same variable in a data set results in a warning.