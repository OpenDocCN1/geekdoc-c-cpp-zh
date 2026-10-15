```
c1 = shape(1,3,1)
c3 = T({1 1 1})
c4 = T({[3] 1})
```

Vector c1 uses the shape function to define a 3×1 vector of value 1. Vector c3 defines a 1×3 vector of value 1, and then transposes it with the SAS/IML function T. Vector c4 uses the repetition factor [3] for the value 1 to define a 1×3 vector that is then transposed. There is an order in which matrix operations are evaluated, and parentheses can help avoid confusion in coding.

# 11.4 Importing a Data Set into SAS/IML and Exporting Matrices from SAS/IML to a Data Set

Up to now, you have entered matrices directly in PROC IML. You can imagine that it would be painful to enter and manipulate a large matrix in SAS. The SAS/IML functions USE and READ can be used to construct a matrix from a SAS data set. And, the SAS/IML functions CREATE and APPEND can be used to construct a SAS data set from a SAS/IML matrix.

# 11.4.1 Creating matrices from SAS data sets and vice versa

Suppose you have a SAS library containing a data set named nitrofen¹ that has a number of variables including total and conc. Display 11.7 illustrates importing these data into SAS/IML, and then adding three new columns. One column contains CONC², and the other two columns contain (CONC − C̄) and (CONC − C̄)², where C̄ is the average concentration. A new data set n2 is exported from SAS/IML using the create and append commands. The create command opens a new data set. The append command adds the contents of the matrix nitro2 to the n2 data set. A vector varnames that contains the names of the variables in the output data set is defined. The colname argument is specified as part of the create statement.

¹ Nitrofen data set from Bailer, A. John, and James T. Oris. 1994. "Assessing Toxicity of Pollutants in Aquatic Systems." Chapter 2 in Case Studies in Biometry. Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. Reprinted with permission of John Wiley & Sons, Inc.