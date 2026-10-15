# Display 1.5 (continued)

![](bbox=[0.13, 0.18, 0.82, 0.52])

Alternatively, you can use PROC SGPLOT with the REG statement or simply add a PLOT statement to PROC REG to produce this graphic. Frequently, there are multiple options for producing the same analysis or graphic. For more information about ODS graphics and the different graphs produced by statistical procedures, see Chapter 6.

Both Display 1.4 and Display 1.5 include the default title The SAS System because no TITLE statement is included in the program. The ODS GRAPHICS statement produces a scatter plot that has a title associated with the FITPLOT option.

# 1.4 What Is a SAS Data Set?

A SAS data set can be thought of as a rectangular object (or data table) where rows are different observations and columns are different variables. In some cases, such as with longitudinal or repeated measures data, rows can be the same subject measured at different times. Data can be entered as part of a SAS program using DATALINES (or CARDS if you like using statements from ancient SAS history).