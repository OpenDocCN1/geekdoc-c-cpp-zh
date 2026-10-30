# Subqueries and Domain Aggregate Functions

# IN THIS CHAPTER

+   - Enhancing your analyses with subqueries
+   - Using domain aggregate functions

Often, you’ll carry out your analyses in layers, each layer of analysis using or building on the previous layer. This practice of building layers into analytical processes is actually very common. For instance, when you build a query using another query as the data source, you’re layering your analysis. When you build a query based on a temporary table created by a make-table query, you’re also layering your analysis.

All these conventional methods of layering analyses have two things in common:

+   - **They all add a step to your analytical processes.** Every query that has to be run in order to feed another query, or every temporary table that has to be created in order to advance your analysis, adds yet another task that must be completed before you get your final results.
+   - **They all require the creation of temporary tables or transitory queries, inundating your database with table and query objects that lead to confusing analytical process, as well as a database that bloats easily.** This is where subqueries and domain aggregate functions can help.

Subqueries and domain aggregate functions allow you to build layers into your analyses within one query, eliminating the need for temporary tables or transitory queries.

> The topic of subqueries and domain aggregate functions requires an understanding of SQL. Most beginning Access users don’t have the foundation in SQL. If you fall into this category, press the pause button here and review Chapter 14 of this book. There, you’ll get enough of a primer on SQL to continue this chapter.

**On the Web**
The starting database for this walkthrough, Chapter15.accdb, can be downloaded from this book’s website.