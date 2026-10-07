# Enhancing Your Table: It is fairly easy to add information to your table. For example, suppose you want to report more than one statistic, say N and MEAN. You can combine statistics by placing them in parentheses such as

(N MEAN)

Or to include the label being put into the table, you could use

```
(N="" MEAN="" )
```

Another enhancement is to put some information in the box that appears at the upper of your table. You can do this by including a /BOX="label" option. For example,

```
TABLE(AREA="" ALL=By Area), (SITE="" ALL=By Site)*TYPE=""
* (N="" MEAN="")*SALES_K=""*F=DOLLAR6.2
/ BOX="Fall Sales;
```

# HANDSON EXAMPLE

Make sure the code is within the semicolon of the TABLE statement. Submit the code. Observe how the text appears in the box.

+   4. To save the table as a Word document using ODS, add the following lines. Before the TABULATE STYLE add the line

```
ODS RTF STYLE=BANKER;
Your PROC TABULATE;
RUN;
ODS RTF CLOSE;
```

Resubmit the code. The final result with these changes is given in Table 19.12.