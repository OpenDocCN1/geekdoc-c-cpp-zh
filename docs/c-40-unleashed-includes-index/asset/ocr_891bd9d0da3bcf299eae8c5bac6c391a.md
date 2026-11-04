![](bbox=[0.05, 0.08, 0.45, 0.28])

FIGURE 19.17 Execution of a filter.

Although I've made this general remark before, I should emphasize the lazy execution nature of query expressions. It's not until you start enumerating over the resulting query object that the query executes. This can be illustrated by setting a breakpoint on the where clause's predicate expression and executing the code. You won't see the breakpoint being hit before you start iterating over the result.

See Figure 19.18 for this situation illustrated for the even numbers filter. Notice how the in keyword in the foreach loop is highlighted, indicating we're executing the loop, and as a result of doing so the filter predicate gets evaluated. Hovering over n reveals the value for which the filter is currently being evaluated. A similar experiment can be conducted for a selection clause's (nontrivial) projection expression.

![](bbox=[0.15, 0.64, 0.48, 0.78])

FIGURE 19.18 Lazy execution of a query expression.

# Horizontal Partitioning

In contrast to the select clause's vertical partitioning, the where clause's filter applies a form of horizontal partitioning, only retaining certain elements (rows) from the queried data source. Figure 19.19 shows this on our well-known products table.

# Ordering Using the orderby Keyword

Sorting elements by one or more criteria is another commonly used querying action, which is supported through the orderby keyword. The basic idea is to specify a key selector function that selects an ordering key for each element in the input sequence. Upon enumerating over the query result object, the ordering key is obtained for all elements and