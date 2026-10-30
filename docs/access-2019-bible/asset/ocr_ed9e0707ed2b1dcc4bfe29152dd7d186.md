# CHAPTER 10

# Going Beyond Select Queries

# IN THIS CHAPTER

+   - Working with aggregate queries
+   - Using action queries
+   - Creating crosstab queries
+   - Optimizing query performance

Retrieving and displaying specific records with a select query is indeed a fundamental task when analyzing data in Access. However, it’s just a small portion of what makes up data analysis. The scope of data analysis is broad and includes grouping and comparing data, updating and deleting data, performing calculations on data, and shaping and reporting data. Access has built-in tools and functionalities designed specifically to handle each of these tasks.

In this chapter, we give you an in-depth look at the various tools available to you in Access and how they can help you go beyond select queries.

> **ON THE WEB**
> The starting database for this walkthrough, `Chapter10.accdb`, can be downloaded from this book’s website.

# Aggregate Queries

An *aggregate query*, sometimes referred to as a *group-by query*, is a type of query you can build to help you quickly group and summarize your data. With a select query, you can retrieve records only as they appear in your data source. But with an aggregate query, you can retrieve a summary snapshot of your data that shows you totals, averages, counts, and more.

# Creating an aggregate query

To get a firm understanding of what an aggregate query does, consider the following scenario: You’ve just been asked to provide the sum of total revenue by period. In response to this request, start a query in Design view and bring in the Dim_Dates.Period and Dim_Transactions.LineTotal fields, as shown in Figure 10.1. If you run this query as is, you’ll get every record in your data set instead of the summary you need.