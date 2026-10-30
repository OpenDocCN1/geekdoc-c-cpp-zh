# Part II: Understanding Access Tables

Because an index means that Access maintains an internal sort order on the data contained in the indexed field, you can see why query performance is enhanced by an index. You should index virtually every field that is frequently involved in queries or is frequently sorted on forms or reports.

Without an index, Access must search each and every record in the database looking for matches. This process is called a table scan and is analogous to searching through each and every card in a Rolodex file to find all the people who work for a certain company. Until you reach the end of the deck, you can’t be sure you’ve found every relevant card in the file.

As mentioned earlier in this chapter, a table’s primary key field is always indexed. This is because the primary key is used to locate records in the table. Indexing the primary key makes it much easier for Access to find the required tables in either the current table or a foreign table related to the current table. Without an index, Access has to search all records in the related table to make sure it has located all the related records.

> Tip
> The performance losses due to unindexed tables can have a devastating effect on the overall performance of an Access application. Anytime you hear a complaint about the performance of an application, consider indexing as a possible solution.

# Multiple-field indexes

Multiple-field indexes (also called composite indexes) are easy to create. In Design view, click the Indexes button on the Design tab of the Ribbon. The Indexes dialog box (shown in Figure 3.17) appears, allowing you to specify the fields to include in the index.

# FIGURE 3.17

Multiple-field (composite) indexes can enhance performance.

![](bbox=[0.18, 0.9, 0.78, 0.97])