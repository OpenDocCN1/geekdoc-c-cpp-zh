# Results

| Product Number | Product Name | Manufacturer Number | Product Type | Product Cost |
| 2101 | Analog Cell Phone | 210 | Phone | $35.00 |
| 2102 | Digital Cell Phone | 210 | Phone | $175.00 |
| 2200 | Office Phone | 220 | Phone | $130.00 |

# Accessing Rows from the Combination of Two Queries

The UNION operator preserves all of the unique rows from the combination of queries. The result is the same as if an OR operator is used to combine the results of each query. Put another way, the union of two queries (A and B) represents rows in A or in B or in both A and B. As illustrated in Figure 7.2, the union represents the entire shaded area (A, B, and C).

# Figure 7.2: Union of Two Queries

![](bbox=[0.42, 0.44, 0.6, 0.61])

The UNION operator automatically eliminates duplicate rows from the results, unless the ALL keyword is specified as part of the UNION operator. The column names assigned to the results are derived from the names in the first query.

In order for the union of two or more queries to be successful, each query must specify the same number of columns of the same or compatible types. Type compatibility means that column attributes are defined the same way. Because column names and attributes are derived from the first table, data types must be of the same type. The data types of the result columns are derived from the source table(s).

To see all products that cost less than $300.00 or products that are classified as a workstation, you have a choice between using OR as shown in the following query or UNION as shown in the next query. As illustrated in the output from both queries, the results are identical no matter which query is used.