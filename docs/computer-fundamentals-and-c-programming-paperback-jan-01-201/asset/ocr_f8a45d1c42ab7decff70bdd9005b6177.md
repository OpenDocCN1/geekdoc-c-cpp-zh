| Enter a line of text: **fgets and sscanf form a useful combination.**<br>FGETS AND SSCANF FORM A USEFUL COMBINATION. |
|---|
| Enter a line of text: **FPUTS AND SPRINTF ARE OFTEN USED TOGETHER.**<br>fputs and sprintf are often used together. |

PROGRAM OUTPUT: `fgets_fputs.c`

# 13.5 THE sscanf AND sprintf FUNCTIONS

Sometimes, you would like to save keyboard input in a string before using a **scanf**-type function to read from the string. Because the string itself doesn’t change, you can use multiple formatting techniques on this data. **scanf** can’t do this job because it changes the buffer in every invocation, but the **sscanf** function meets our requirement.

In the same vein, you may like to use **printf**-like functionality to format a line of data and save it in a string. This gives you the chance to modify the string before or after printing. The **sprintf** function does whatever **printf** does except that it saves the formatted output in a string. Once that is done, you can use **fputs** to print the string.

# 13.5.1  sscanf: Formatted Input from a String

Consider a situation where you have the option of inputting a date in multiple formats (say, *dd-mm-yy*, *month_name-dd-yy*, or *dd-month_name-yy*). You can’t catch them all by repeatedly invoking **scanf** with different format specifiers because each invocation will fetch data from the buffer and overwrite the previous data. You need to use **sscanf** which has the following prototype:

```
int sscanf(char *str, cstring, &var1, &var2, ...);
```

Unlike **scanf** which reads standard input, **sscanf** reads the string *str* and uses the information provided in *cstring* (the control string) to format the data before saving them in variables. The function is often used in combination with **fgets**. To validate a date, read the input into a buffer with **fgets** first:

```
fgets(line, SIZE, stdin);
```

You can now use **sscanf** to match the input saved in *line* with the form *dd-mm-yyyy*:

```
sscanf(line, "%2d-%2d-%4d", &day, &month, &year);
```

If the match doesn’t succeed, you can call **sscanf** multiple times, with a different format specifier in each invocation. The following code snippet accepts 12-05-16, May-12-16 and 12-May-16 as valid date formats:

```
if (sscanf(line, "%2hd-%2hd-%2hd", &day, &month, &year) == 3)
    date_ok = 1;
else if (sscanf(line, "%3s-%hd-%hd", month_arr, &day, &year) == 3)
    date_ok = 1;
```