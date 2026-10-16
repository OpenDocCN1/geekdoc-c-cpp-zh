# Exploring Macro Variables and Values

Macro variables and their values provide PROC SQL users with a convenient way to store text strings in SAS code. Whether user-defined macro variables are created or automatic macro variables supplied by SAS are referenced, macro variables can be defined and used to improve a program’s efficiency and usefulness. A number of useful techniques are presented in this section to illustrate the capabilities afforded users when interfacing PROC SQL with macro variables.

# Creating a Macro Variable with %LET

The %LET macro statement creates a single macro variable and assigns or changes a text string value. It can be specified inside or outside a macro and used with PROC SQL. In the next example, a macro variable called PRODTYPE is created with a value of SOFTWARE assigned in a %LET statement. The PRODTYPE macro variable is referenced in the TITLE statement and enclosed in quotation marks in the PROC SQL WHERE clause. This approach of assigning macro variable values at the beginning of a program makes it easy and convenient to make changes because the values are all at the beginning of the program.

# SQL Code

```
%LET PRODTYPE=SOFTWARE;
TITLE "Listing of &PRODTYPE Products";
PROC SQL;
    SELECT PRODNAME,
           PRODCOST
    FROM PRODUCTS
    WHERE UPCASE(PRODTYPE) = "&PRODTYPE"
    ORDER BY PRODCOST;
QUIT;
```

# Results

![](bbox=[0.17, 0.6, 0.48, 0.77])

In the next example, a macro named VIEW creates a macro variable called NAME and assigns a value to it with a %LET statement. When VIEW is executed, a value of PRODUCTS, MANUFACTURERS, or INVENTORY is substituted for the macro variable. The value supplied for the macro variable determines what view is referenced. If the value supplied to the macro