row in the result contains the information about a book, together with the publisher name and web page URL. Note that the publisher names and URLs are duplicated across several rows because we have several books with the same publisher.

![](bbox=[0.107, 0.233, 0.806, 0.566])

Figure 5.3  Sample table containing books

The benefit of joining tables is avoiding unnecessary duplication of data in the database tables. For example, a naive database design might have had columns for the publisher name and URL right in the *Books* table. But then the database itself, and not just the query result, would have many duplicates of these entries. If a publisher’s web address changed, all entries would need to be updated. Clearly, this is somewhat error-prone. In the relational model, we distribute data into multiple tables so that no information is unnecessarily duplicated. For example, each publisher’s URL is contained only once in the publisher table. If the information needs to be combined, the tables are joined.

In the figures, you can see a graphical tool to inspect and link the tables. Many vendors have tools to express queries in a simple form by connecting column names and filling information into forms. Such tools are often called *query by example (QBE)* tools. In contrast, a query that uses SQL is written out in text, using SQL syntax, for example: