# KEY TERMS

+   - **Aggregate method**—a method that returns a single value from a group of values
+   - **Language Integrated Query**—LINQ; the new query language in Visual Basic 2008
+   - **LINQ**—Language Integrated Query
+   - **Query**—specifies the records to select in a dataset, and the order in which to arrange the records

# ANSWERS TO MINI-QUIZZES

+   **MINI-QUIZ 1**
+   
+   1. `name.LastName.ToUpper = “A*”`
+   2. `Order By name.LastName Descending`
+   3. Language Integrated Query

+   **MINI-QUIZ 2**
+   
+   1. `sales.JanSales`
+   2. `Select points.PointsEarned Into Average()`
+   3. `Min`

# REVIEW QUESTIONS

1. Which of the following LINQ statements selects all of the records in the tblStates table?

+   a. `Dim records = From state In StatesDataSet.tblStates _`
+      `Select All state`
+   
+   b. `Dim records = From state In StatesDataSet.tblStates _`
+      `Select state`
+   
+   c. `Dim records = Select state From StatesDataSet.tblStates`
+   
+   d. `Dim records = From StatesDataSet.tblStates _`
+      `Select tblStates.state`