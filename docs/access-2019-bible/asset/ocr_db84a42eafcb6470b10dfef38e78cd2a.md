# CHAPTER 13

# Performing Conditional Analyses

# IN THIS CHAPTER

+   - Using parameter queries
+   - Using conditional functions
+   - Comparing the `IIf` and `Switch` functions

Until now your analyses have been straightforward. You build a query, you add some criteria, you add a calculation, you save the query, and then you run the query whenever you need to. What happens, however, if the criteria that governs your analysis changes frequently or if your analytical processes depend on certain conditions being met? In these situations, you would use a conditional analysis: an analysis whose outcome depends on a predefined set of conditions. Barring VBA and macros, there are several tools and functions that enable you to build conditional analyses; some of these are parameter queries, the IIf function, and the Switch function.

In this chapter, you learn how these tools and functions can help you save time, organize your analytical processes, and enhance your analyses.

> **ON THE WEB**
> The database for this walkthrough, `Chapter13.accdb`, can be downloaded from this book’s website.

# Using Parameter Queries

You’ll find that when building your analytical processes, anticipating every single combination of criteria that may be needed will often be difficult. This is where parameter queries can help.

A parameter query is an interactive query that prompts you for criteria before the query is run. A parameter query is useful when you need to ask a query different questions using different criteria each time it’s run. To get a firm understanding of how a parameter query can help you, build the query shown in Figure 13.1. With this query, you want to see all the purchase orders logged during the 201205 period.