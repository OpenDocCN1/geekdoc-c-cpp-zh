+   2.5.5 Using Preloaded Formats 72
+   2.5.6 Using the SPARSE Option with PROC FREQ 73
+   **2.6 Some General Concepts**  **73**
+   2.6.1 Shorthand Variable Naming 73
+   2.6.2 Understanding the ORDER= Option 77
+   2.6.3 Quotes within Quotes within Quotes 79
+   2.6.4 Setting the Length of Numeric Variables 81
+   **2.7 WHERE Specifics**  **82**
+   2.7.1 Operators Just for the WHERE 83
+   2.7.2 Interaction with the BY Statement 86
+   **2.8 Appending Data Sets**  **88**
+   2.8.1 Appending Data Sets Using the DATA Step and SQL UNION 88
+   2.8.2 Using the DATASETS Procedure’s APPEND Statement 90
+   **2.9 Finding and Eliminating Duplicates**  **90**
+   2.9.1 Using PROC SORT 91
+   2.9.2 Using FIRST. and LAST. BY-Group Processing 92
+   2.9.3 Using PROC SQL 93
+   2.9.4 Using PROC FREQ 93
+   2.9.5 Using the Data Component Hash Object 94
+   **2.10 Working with Missing Values**  **97**
+   2.10.1 Special Missing Values 97
+   2.10.2 MISSING System Option 98
+   2.10.3 Using the CMISS, NMISS, and MISSING Functions 99
+   2.10.4 Using the CALL MISSING Routine 100
+   2.10.5 When Classification Variables Are Missing 100
+   2.10.6 Missing Values and More Variables 101
+   2.10.7 Imputing Missing Values 101

In SAS the data set is central to most of our analyses and reporting. This means that it is crucial that we have the power to know all sorts of things about our data. The power that we need comes from a multitude of SAS tools and techniques. This chapter is a fairly random collection of these tools and techniques that can help us accomplish our goals of working with our data sets.

# 2.1 Data Set Options

Data set options can be used to modify how a data set is either read or written. There are over three dozen of these options, and while you will generally only make use of a hand full of them, you should have a good idea of their scope.