+   c. Derived tables
+    d. View definitions
+    e. INSERT with SELECT clause

# Set Operators and Precedence

Set operators adhere to an order of precedence. The following precedence rules apply:

+   1. When more than one set operator is specified, each is applied in the order specified:
+      a. Top to bottom
+      b. Left to right
+   2. The default order of precedence for processing set operators follows:
+      a. INTERSECT
+      b. UNION and/or EXCEPT
+      c. When parentheses are specified, the default order of precedence can be altered.

# Accessing Rows from the Intersection of Two Queries

The INTERSECT operator creates query results that consist of all the unique rows from the intersection of the two queries. Put another way, the intersection of two queries (A and B) is represented by C, which indicates that the rows that are produced occur in both A and in B. As Figure 7.1 shows, the intersection of both queries is represented in the shaded area (C).

Figure 7.1: Intersection of Two Queries

![](bbox=[0.42, 0.505, 0.61, 0.66])

To see all products that cost less than $300.00 and product types classified as “phone”, you could construct a simple query with a WHERE clause or specify the intersection of two separate queries. The next example illustrates a simple query that specifies a WHERE clause to display phones that cost less than $300.00.