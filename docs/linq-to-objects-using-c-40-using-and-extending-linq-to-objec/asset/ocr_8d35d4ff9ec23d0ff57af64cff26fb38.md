# CHAPTER 3

# WRITING BASIC QUERIES

Goals of this chapter:

+   - Understand the LINQ syntax options.
- Introduce how to write basic queries.
- Demonstrate how to filter, project, and order data using LINQ queries.

The main goal of this chapter is to introduce the basics of writing queries. These basics include the syntax options available for writing queries, how to filter data, how to order data, and how to return the exact result set you want. By the end of this chapter, you will understand how to write the most common query elements and, in the following chapter, you will expand this understanding into the more advanced query features of grouping and joining with other sources.

# Query Syntax Style Options

Most previous examples in this book have used the query expression syntax, but there are two styles for writing LINQ queries. Not all operators are available through the query expression syntax built into the C# compiler, and to use the remaining operators (or to call your own operators), the extension method query syntax or a combination of the two is necessary. You will continually need to know both styles of query syntax in order to read, write, and understand code written using LINQ.

+   - Extension method format (also known as the dot notation syntax)—The extension method format is simply where multiple extension methods are cascaded together, each returning an IEnumerable<T> result to allow the next extension method to flow from the previous result and so on (known as a fluid interface).